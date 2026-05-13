---
layout: default
title: PostgreSQL Queries
parent: Database
last_modified_date: 10:00 12.02.2026
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

## Generate UUID with timestamp

PostgreSQL 18 and later (built-in UUIDv7):

```sql
select
  uuidv7(),
  uuid_extract_version(uuidv7()),
  uuid_extract_timestamp(uuidv7()),
  current_timestamp as now_ts
```

Older versions (UUIDv1):

```sql
select
  v1,
  uuid_extract_version(v1),
  uuid_extract_timestamp(v1),
  current_timestamp as now_ts
from (
  select (
    lpad(to_hex( ts & x'ffffffff'::bigint), 8, '0') || '-' ||
    lpad(to_hex((ts >> 32) & x'ffff'::bigint), 4, '0') || '-' ||
    lpad(to_hex(((ts >> 48) & x'fff'::bigint) | x'1000'::bigint), 4, '0') || '-' ||
    lpad(to_hex((trunc(random() * 2^30)::bigint << 32 | trunc(random() * 2^32)::bigint) | x'8000000000000000'::bigint), 16, '0')
  )::uuid as v1
  from (
    select trunc((extract(epoch from current_timestamp) + 12219292800) * 1e7)::bigint as ts
  ) _
) t;
```

**Use cases:**

- Generate unique identifiers with embedded timestamps
- Track creation time of records without separate timestamp columns
- Facilitate time-based queries and sorting on UUIDs
