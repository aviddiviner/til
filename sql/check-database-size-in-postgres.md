# Check database size in Postgres

```
database=> SELECT pg_size_pretty(pg_database_size(current_database()));
 pg_size_pretty
----------------
 4035 MB
(1 row)
```

## Schema size

This function will return the size of a schema. Note: this returns `0` if the given schema doesn't exist.

```plpgsql
CREATE OR REPLACE FUNCTION pg_schema_size(text) RETURNS BIGINT AS $$
SELECT SUM(pg_total_relation_size(quote_ident(schemaname) || '.' || quote_ident(tablename)))::BIGINT
  FROM pg_tables WHERE schemaname = $1
$$ LANGUAGE SQL;
```

```
database=> SELECT pg_size_pretty(pg_schema_size('myschema'));
 pg_size_pretty
----------------
 4027 MB
(1 row)
```
