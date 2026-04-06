# Database Migration Patterns

Safely evolve database schemas in production with zero-downtime migrations.

---

## Migration Fundamentals

### Migration File Structure
```
migrations/
├── 001_create_users.sql
├── 002_add_email_index.sql
├── 003_create_orders.sql
├── 004_add_user_status.sql
└── 005_rename_column.sql
```

Each migration file contains:
- **Up migration**: Apply the change
- **Down migration**: Reverse the change (for rollback)

### Migration Tools

| Tool | Language | Features |
|------|----------|----------|
| Flyway | Java/CLI | Version-based, repeatable migrations |
| Alembic | Python | SQLAlchemy integration, auto-generation |
| Knex | Node.js | Promise-based, seed data support |
| golang-migrate | Go | CLI + library, multiple DB support |
| Liquibase | Java/CLI | XML/YAML/SQL, changelog tracking |
| Rails Migrations | Ruby | DSL, schema.rb generation |

---

## Zero-Downtime Migration Patterns

### Expand-Contract Pattern

The safest approach for breaking schema changes:

**Phase 1 — Expand:**
```sql
-- Add new column (backward-compatible)
ALTER TABLE users ADD COLUMN full_name VARCHAR(255);
```

**Phase 2 — Migrate:**
```sql
-- Backfill data
UPDATE users SET full_name = first_name || ' ' || last_name
WHERE full_name IS NULL;
```
Deploy code that writes to both old and new columns.

**Phase 3 — Contract:**
```sql
-- Remove old columns (after all code uses new column)
ALTER TABLE users DROP COLUMN first_name;
ALTER TABLE users DROP COLUMN last_name;
```

### Adding NOT NULL Constraints Safely

```sql
-- Step 1: Add column as nullable
ALTER TABLE users ADD COLUMN status VARCHAR(20);

-- Step 2: Backfill default values
UPDATE users SET status = 'active' WHERE status IS NULL;

-- Step 3: Add constraint (after all rows have values)
ALTER TABLE users ALTER COLUMN status SET NOT NULL;
ALTER TABLE users ALTER COLUMN status SET DEFAULT 'active';
```

### Renaming Columns Safely

1. Add new column
2. Deploy code that writes to both columns
3. Backfill new column from old
4. Deploy code that reads from new column only
5. Drop old column

---

## Large Table Operations

### Online Schema Changes

For tables with millions of rows, avoid locking:

**PostgreSQL:**
```sql
-- Create index concurrently (no lock)
CREATE INDEX CONCURRENTLY idx_users_email ON users(email);

-- Add column with default (instant in PG 11+)
ALTER TABLE users ADD COLUMN verified BOOLEAN DEFAULT false;
```

**MySQL (pt-online-schema-change):**
```bash
pt-online-schema-change --alter "ADD COLUMN status VARCHAR(20)" \
  --execute D=mydb,t=users
```

### Batch Data Migrations

For large backfills, process in batches to avoid lock contention:

```sql
-- Process 10,000 rows at a time
DO $$
DECLARE
  batch_size INT := 10000;
  affected INT;
BEGIN
  LOOP
    UPDATE users 
    SET full_name = first_name || ' ' || last_name
    WHERE full_name IS NULL
    LIMIT batch_size;
    
    GET DIAGNOSTICS affected = ROW_COUNT;
    EXIT WHEN affected = 0;
    
    PERFORM pg_sleep(0.1);  -- Brief pause to reduce load
  END LOOP;
END $$;
```

---

## Rollback Strategies

### Immediate Rollback
- Keep down migrations tested and ready
- Run rollback within minutes of detecting issues
- Only works for backward-compatible changes

### Forward-Fix
- When rollback is riskier than fixing forward
- Deploy a new migration that corrects the issue
- Preferred for data migrations (can't un-delete data)

### Blue-Green Database Pattern
1. Maintain two database instances
2. Apply migration to inactive (green) database
3. Switch application traffic to green
4. Keep blue available for rollback
5. Requires double infrastructure cost

---

## Best Practices

- **One change per migration**: Easier to track, rollback, and debug
- **Test against production-size data**: Small test databases hide performance issues
- **Always write down migrations**: Even if you think you'll never need them
- **Run migrations before deploying code**: Schema must support both old and new code
- **Never modify applied migrations**: Create new migrations to fix issues
- **Monitor during migrations**: Watch lock wait times, replication lag, CPU
- **Backup before major migrations**: Even with rollback scripts
- **Version control all migrations**: Track in git alongside application code
