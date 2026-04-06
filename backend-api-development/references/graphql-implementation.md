# GraphQL Implementation Guide

Build efficient GraphQL APIs with schemas, resolvers, and performance optimization.

---

## Schema Design

### Type Definitions

```graphql
type User {
  id: ID!
  email: String!
  name: String!
  role: Role!
  posts(first: Int, after: String): PostConnection!
  createdAt: DateTime!
}

enum Role {
  ADMIN
  EDITOR
  VIEWER
}

type Post {
  id: ID!
  title: String!
  content: String!
  author: User!
  tags: [Tag!]!
  publishedAt: DateTime
  status: PostStatus!
}

type PostConnection {
  edges: [PostEdge!]!
  pageInfo: PageInfo!
  totalCount: Int!
}

type PostEdge {
  node: Post!
  cursor: String!
}

type PageInfo {
  hasNextPage: Boolean!
  hasPreviousPage: Boolean!
  startCursor: String
  endCursor: String
}
```

### Schema Design Best Practices
- Use `ID!` for all entity primary keys
- Implement Relay-style connection pagination for lists
- Use enums for fixed value sets
- Make fields non-nullable (`!`) when data is always present
- Use input types for mutations
- Add descriptions to types and fields for documentation

---

## Queries and Mutations

### Query Structure
```graphql
type Query {
  user(id: ID!): User
  users(filter: UserFilter, first: Int, after: String): UserConnection!
  me: User!
  searchPosts(query: String!, first: Int): PostConnection!
}

input UserFilter {
  role: Role
  status: UserStatus
  search: String
}
```

### Mutation Patterns
```graphql
type Mutation {
  createUser(input: CreateUserInput!): CreateUserPayload!
  updateUser(id: ID!, input: UpdateUserInput!): UpdateUserPayload!
  deleteUser(id: ID!): DeleteUserPayload!
}

input CreateUserInput {
  email: String!
  name: String!
  role: Role!
}

type CreateUserPayload {
  user: User
  errors: [UserError!]!
}

type UserError {
  field: String
  message: String!
  code: ErrorCode!
}
```

**Mutation Best Practices:**
- Use dedicated input types (not inline arguments)
- Return payload types with both result and errors
- Follow naming convention: `createX`, `updateX`, `deleteX`
- Return the modified object for cache updates

---

## Resolver Architecture

### DataLoader Pattern (N+1 Prevention)

The most critical GraphQL performance optimization:

```javascript
// Without DataLoader: N+1 queries
// 1 query for users + N queries for each user's posts

// With DataLoader: 2 queries total
const userLoader = new DataLoader(async (userIds) => {
  const users = await db.users.findByIds(userIds);
  return userIds.map(id => users.find(u => u.id === id));
});

// Resolver
const resolvers = {
  Post: {
    author: (post) => userLoader.load(post.authorId)
  }
};
```

**DataLoader Rules:**
- Create new DataLoader instances per request (to avoid cache leaks)
- Batch keys must return results in the same order as input
- Use for any field that references another entity

---

## Performance Optimization

### Query Complexity Limits

Prevent expensive queries from overwhelming the server:

| Limit Type | Configuration | Purpose |
|-----------|--------------|---------|
| Depth limit | Max 10-15 levels | Prevent deeply nested queries |
| Complexity limit | Max 1000-5000 points | Prevent wide, expensive queries |
| Field count limit | Max 100-500 fields | Prevent overly broad selections |
| Timeout | 10-30 seconds | Kill long-running queries |

### Persisted Queries

For production APIs, allow only pre-registered queries:
1. During build, extract all queries from client code
2. Hash each query and register with server
3. Client sends hash instead of full query string
4. Prevents arbitrary query execution

### Caching Strategies
- **Response caching**: Cache full query responses (CDN-friendly with GET requests)
- **DataLoader caching**: Per-request in-memory cache (automatic)
- **Entity caching**: Cache individual entities in Redis
- **Schema caching**: Cache parsed schema in memory

---

## Subscriptions

### WebSocket Implementation

```graphql
type Subscription {
  postCreated: Post!
  messageReceived(channelId: ID!): Message!
  userStatusChanged(userId: ID!): UserStatus!
}
```

**Implementation Considerations:**
- Use `graphql-ws` protocol (not deprecated `subscriptions-transport-ws`)
- Implement connection authentication via `connectionParams`
- Scale with Redis PubSub for multi-server deployments
- Add subscription filtering to prevent unnecessary broadcasts
- Implement connection timeouts and heartbeats

---

## Security

- Implement query depth and complexity limits
- Use persisted queries in production
- Disable introspection in production environments
- Validate and sanitize all input arguments
- Implement field-level authorization in resolvers
- Rate limit by query complexity, not just request count
- Log all mutations for audit trail
