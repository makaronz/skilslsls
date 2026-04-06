# NoSQL Database Patterns

Design patterns and best practices for document, key-value, column, and graph databases.

---

## Document Database Patterns (MongoDB)

### Schema Design Principles

**Embedding vs Referencing Decision:**

| Factor | Embed | Reference |
|--------|-------|-----------|
| Read pattern | Always read together | Read independently |
| Data size | Subdocument < 16MB | Large or growing |
| Update frequency | Rarely updated | Frequently updated |
| Cardinality | One-to-few | One-to-many or many-to-many |
| Data duplication | Acceptable | Must avoid |

### Common Patterns

**Embedded One-to-Few:**
```json
{
  "_id": "user_123",
  "name": "John Doe",
  "addresses": [
    {"type": "home", "street": "123 Main St", "city": "Austin"},
    {"type": "work", "street": "456 Tech Ave", "city": "Austin"}
  ]
}
```

**Referenced One-to-Many:**
```json
// User document
{"_id": "user_123", "name": "John Doe"}

// Order documents
{"_id": "order_1", "user_id": "user_123", "total": 99.99}
{"_id": "order_2", "user_id": "user_123", "total": 149.50}
```

**Bucket Pattern (Time Series):**
```json
{
  "_id": "sensor_001_2024_01_15_14",
  "sensor_id": "sensor_001",
  "date": "2024-01-15",
  "hour": 14,
  "readings": [
    {"minute": 0, "temp": 72.1, "humidity": 45},
    {"minute": 5, "temp": 72.3, "humidity": 44}
  ],
  "count": 12
}
```

### MongoDB Index Strategies
- Create compound indexes matching query patterns
- Use `explain()` to verify index usage
- Implement TTL indexes for auto-expiring data
- Use partial indexes to reduce index size
- Consider wildcard indexes for dynamic schemas

---

## Key-Value Store Patterns (Redis)

### Data Structure Selection

| Structure | Use Case | Commands |
|-----------|----------|----------|
| String | Cache, counters, flags | GET, SET, INCR, EXPIRE |
| Hash | Object storage, user profiles | HGET, HSET, HMGET |
| List | Queues, recent items | LPUSH, RPOP, LRANGE |
| Set | Tags, unique visitors | SADD, SMEMBERS, SINTER |
| Sorted Set | Leaderboards, rankings | ZADD, ZRANGE, ZRANK |
| Stream | Event logs, message queues | XADD, XREAD, XRANGE |

### Caching Patterns

**Cache-Aside (Lazy Loading):**
1. Check cache for data
2. On miss: query database, store in cache with TTL
3. On hit: return cached data

**Write-Through:**
1. Write to cache and database simultaneously
2. Ensures cache is always current
3. Higher write latency

**Write-Behind (Write-Back):**
1. Write to cache immediately
2. Asynchronously write to database
3. Risk of data loss on cache failure

---

## Column-Family Patterns (Cassandra)

### Data Modeling Rules
1. **Query-first design**: Model tables around query patterns
2. **Denormalize**: Duplicate data across tables for different queries
3. **Partition wisely**: Distribute data evenly, keep partitions < 100MB
4. **Cluster within partitions**: ORDER BY via clustering columns

### Partition Key Selection

| Pattern | Example | Cardinality | Distribution |
|---------|---------|-------------|-------------|
| Natural key | `user_id` | High | Good |
| Composite | `(country, city)` | Medium | Good |
| Time-bucketed | `(sensor_id, date)` | High | Good |
| Single value | `status` | Very low | Bad (hot partition) |

---

## Graph Database Patterns (Neo4j)

### When to Use Graph Databases
- Social networks (friends, followers, recommendations)
- Fraud detection (transaction chains, account linking)
- Knowledge graphs (entity relationships)
- Recommendation engines (collaborative filtering)
- Network topology (infrastructure, routes)

### Cypher Query Examples
```cypher
// Find friends of friends
MATCH (me:User {id: 'user_123'})-[:FRIENDS]->(friend)-[:FRIENDS]->(fof)
WHERE NOT (me)-[:FRIENDS]->(fof) AND fof <> me
RETURN fof.name, COUNT(friend) as mutual_friends
ORDER BY mutual_friends DESC LIMIT 10;

// Shortest path between users
MATCH path = shortestPath(
  (a:User {id: 'user_1'})-[:FRIENDS*..6]-(b:User {id: 'user_2'})
)
RETURN path;
```

---

## NoSQL Selection Guide

| Requirement | Best Choice | Example Products |
|-------------|------------|-----------------|
| Flexible schema, complex queries | Document | MongoDB, CouchDB |
| Ultra-fast caching, sessions | Key-Value | Redis, Memcached |
| Time series, high write throughput | Column-Family | Cassandra, ScyllaDB |
| Complex relationships, traversals | Graph | Neo4j, Amazon Neptune |
| Full-text search | Search engine | Elasticsearch, OpenSearch |
| Wide column + SQL | NewSQL | CockroachDB, TiDB |
