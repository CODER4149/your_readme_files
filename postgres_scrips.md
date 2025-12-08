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
## dead tupple rows in mb
```



SELECT
    schemaname,
    relname AS table_name,
    pg_total_relation_size(relid) / 1024 / 1024 AS size_mb,
    n_live_tup AS live_rows,
    n_dead_tup AS dead_rows,
    ROUND((n_dead_tup::numeric / NULLIF(n_live_tup + n_dead_tup, 0)) * 100, 2) AS dead_pct,
    last_autovacuum,
    last_vacuum
FROM pg_stat_all_tables
ORDER BY size_mb DESC;


```
## full vacume 
```
-- 1. for table
VACUUM FULL  table_name;

-- 2.  entire db 

VACUUM FULL;


```
## create view 
```
-- DROP  VIEW IF EXISTS mv_live_instock_inventory;
-- DROP MATERIALIZED VIEW IF EXISTS mv_live_instock_inventory_v2;
-- DROP MATERIALIZED VIEW IF EXISTS live_instock_inventory_type;
-- DROP FUNCTION IF EXISTS refresh_mv_live_instock_inventory();
-- DROP FUNCTION IF EXISTS refresh_and_get_mv_live_instock_inventory();
-- DROP FUNCTION IF EXISTS refresh_and_get_live_instock_inventory();
-- DROP TYPE IF EXISTS live_instock_inventory_type;
-- DROP VIEW IF EXISTS live_instock_inventory;

CREATE OR REPLACE VIEW  live_instock_inventory AS
SELECT
    es.epc,
    es.product_code,
    pb.box_number,
    pd.doc_no,
    pm.c25 AS brand_name,
    pm.c20 AS size,
    pm.c66 AS short_description,
    b.bin_no AS current_bin,
    osz.zone_name AS current_zone,
    es.mrp,
    es.mfg_date,
    es.expiry_date,
    es.batch_number,
    es.created_time AS created_datetime,
    es.updated_time AS updated_datetime,
    o.site_code AS store_code,
    o.site_name AS store_name
FROM epc_status es
LEFT JOIN process_document pd ON es.doc_id = pd.doc_id
LEFT JOIN process_box pb ON es.box_id = pb.box_id
LEFT JOIN product_master pm ON es.product_code::text = pm.product_code::text
LEFT JOIN bins b ON es.bin_id = b.bin_id
LEFT JOIN o_site o ON es.site_id = o.site_id
LEFT JOIN o_site_zone osz ON es.sz_id = osz.sz_id
WHERE es.site_id = 8
  AND es.status = 'INSTOCK'
  AND es.product_code is not null;

CREATE USER user WITH PASSWORD 'user';
GRANT USAGE ON SCHEMA public TO user;
GRANT SELECT ON live_instock_inventory TO user;



```
