# SQL Query Optimization

Techniques for writing efficient SQL queries and implementing strategic indexing.

---

## Index Strategy

### Index Types

| Index Type | Use Case | Example |
|-----------|----------|---------|
| B-Tree (default) | Equality, range, sorting, prefix | `CREATE INDEX idx_users_email ON users(email)` |
| Hash | Equality only | `CREATE INDEX idx_users_id ON users USING HASH(id)` |
| GIN | Full-text, arrays, JSONB | `CREATE INDEX idx_posts_tags ON posts USING GIN(tags)` |
| GiST | Geometric, range types, full-text | `CREATE INDEX idx_locations_geo ON locations USING GIST(coordinates)` |
| BRIN | Large tables with natural ordering | `CREATE INDEX idx_logs_created ON logs USING BRIN(created_at)` |
| Partial | Subset of rows | `CREATE INDEX idx_active ON users(email) WHERE active = true` |

### Composite Index Design

**Column Order Matters:** Place columns in order of selectivity and query patterns.

```sql
-- Query: WHERE status = 'active' AND created_at > '2024-01-01' ORDER BY name
CREATE INDEX idx_users_status_created_name 
  ON users(status, created_at, name);
```

**Rules:**
1. Equality columns first, range columns last
2. Include columns used in WHERE, JOIN, ORDER BY
3. Consider covering indexes to avoid table lookups
4. Maximum 3-4 columns per composite index

### Index Anti-Patterns
- Indexing every column individually
- Indexing low-cardinality columns alone (e.g., boolean)
- Too many indexes on write-heavy tables
- Not analyzing index usage (`pg_stat_user_indexes`)

---

## Query Optimization Techniques

### EXPLAIN ANALYZE

Always analyze query plans before optimizing:
```sql
EXPLAIN (ANALYZE, BUFFERS, FORMAT TEXT) 
SELECT u.name, COUNT(p.id) 
FROM users u 
JOIN posts p ON p.user_id = u.id 
WHERE u.status = 'active'
GROUP BY u.name;
```

**Key Indicators:**
| Indicator | Good | Bad |
|-----------|------|-----|
| Seq Scan on large table | Never | Index missing |
| Nested Loop with large outer | Rare | Consider hash join |
| Sort with high memory | Only if needed | Add index for ORDER BY |
| Rows (estimated vs actual) | Close match | Statistics outdated |

### Common Optimizations

**Replace subqueries with JOINs:**
```sql
-- Slow: Correlated subquery
SELECT * FROM orders WHERE customer_id IN (
  SELECT id FROM customers WHERE status = 'premium'
);

-- Faster: JOIN
SELECT o.* FROM orders o
JOIN customers c ON o.customer_id = c.id
WHERE c.status = 'premium';
```

**Use EXISTS instead of IN for large sets:**
```sql
-- Better for large subquery results
SELECT * FROM orders o
WHERE EXISTS (
  SELECT 1 FROM customers c 
  WHERE c.id = o.customer_id AND c.status = 'premium'
);
```

**Avoid functions on indexed columns:**
```sql
-- Bad: Index on created_at won't be used
WHERE EXTRACT(YEAR FROM created_at) = 2024

-- Good: Range scan uses index
WHERE created_at >= '2024-01-01' AND created_at < '2025-01-01'
```

---

## Connection Pooling

### PgBouncer Configuration

| Setting | Transaction Mode | Session Mode |
|---------|-----------------|--------------|
| `pool_mode` | `transaction` | `session` |
| `default_pool_size` | 20-50 | Match max connections |
| `max_client_conn` | 1000+ | Lower |
| `reserve_pool_size` | 5 | 5 |
| Use case | Web apps (recommended) | Prepared statements, LISTEN |

### Pool Sizing Formula
```
Optimal connections = (CPU cores * 2) + effective_spindle_count
```
For most cloud databases: **10-20 connections per application instance**.

---

## Performance Monitoring

### Key Queries to Monitor

```sql
-- Find slow queries (PostgreSQL)
SELECT query, calls, mean_exec_time, total_exec_time
FROM pg_stat_statements
ORDER BY total_exec_time DESC
LIMIT 20;

-- Find unused indexes
SELECT indexrelname, idx_scan, pg_size_pretty(pg_relation_size(indexrelid))
FROM pg_stat_user_indexes
WHERE idx_scan = 0 AND indexrelname NOT LIKE '%pkey%'
ORDER BY pg_relation_size(indexrelid) DESC;

-- Table bloat estimation
SELECT relname, n_dead_tup, n_live_tup,
  round(n_dead_tup::numeric / NULLIF(n_live_tup, 0) * 100, 2) as dead_pct
FROM pg_stat_user_tables
WHERE n_dead_tup > 1000
ORDER BY n_dead_tup DESC;
```
