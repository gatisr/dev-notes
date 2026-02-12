---
layout: default
title: PostgreSQL Function/Procedure Queries
parent: Database
last_modified_date: 12.02.2026 10:00
---

## Find Function Source by Name

```sql
SELECT prosrc 
FROM pg_catalog.pg_proc pr
JOIN pg_catalog.pg_namespace ns ON ns.oid = pr.pronamespace
WHERE proname = 'function_name' 
  AND nspname = 'schema_name';
```

## Search in Function Sources

```sql
SELECT
  nspname AS schema,
  proname AS function_name,
  prosrc AS source_code
FROM pg_catalog.pg_proc pr
JOIN pg_catalog.pg_namespace ns ON ns.oid = pr.pronamespace
WHERE prosrc LIKE '%search_term%'
  -- AND nspname = 'schema_name'  -- optional filter
ORDER BY nspname, proname;
```

**Use cases:**

- Find where specific function is called
- Search for table references in procedures
- Debug function dependencies
