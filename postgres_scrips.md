## create read user script 
````
-- 1. Create the read-only user
CREATE USER readonly_tagid WITH PASSWORD 'readonly_tagid';

-- 2. Allow user to connect to this database
GRANT CONNECT ON DATABASE "tagid_integration_queue_prod" TO readonly_tagid;

-- 3. Allow schema usage (assuming schema is 'public')
GRANT USAGE ON SCHEMA public TO readonly_tagid;

-- 4. Allow SELECT on all current tables
GRANT SELECT ON ALL TABLES IN SCHEMA public TO readonly_tagid;

-- 5. (Optional) Allow SELECT on all sequences (if needed)
GRANT SELECT ON ALL SEQUENCES IN SCHEMA public TO readonly_tagid;

-- 6. Ensure future tables are also readable
ALTER DEFAULT PRIVILEGES IN SCHEMA public
GRANT SELECT ON TABLES TO readonly_tagid;

-- 7. Ensure future sequences are also readable
ALTER DEFAULT PRIVILEGES IN SCHEMA public
GRANT SELECT ON SEQUENCES TO readonly_tagid;

````


## create insert / update/select script

```
-- 1. Create the user (if not already created)
CREATE USER admin WITH PASSWORD 'admin';

-- 2. Allow user to connect to the database
GRANT CONNECT ON DATABASE "test" TO admin;

-- 3. Allow usage of the schema (public)
GRANT USAGE ON SCHEMA public TO admin;

-- 4. Allow SELECT, INSERT, UPDATE on all existing tables
GRANT SELECT, INSERT, UPDATE ON ALL TABLES IN SCHEMA public TO admin;

-- 5. (Optional) Allow SELECT on sequences (for accessing serial/identity columns)
GRANT SELECT ON ALL SEQUENCES IN SCHEMA public TO admin;

-- 6. Set default privileges: For future tables
ALTER DEFAULT PRIVILEGES IN SCHEMA public
GRANT SELECT, INSERT, UPDATE ON TABLES TO admin;

-- 7. Set default privileges: For future sequences
ALTER DEFAULT PRIVILEGES IN SCHEMA public
GRANT SELECT ON SEQUENCES TO admin;


```
