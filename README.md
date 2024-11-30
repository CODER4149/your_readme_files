# your_readme_files
#Docker Build Container
  -sudo docker build -t image_name .

#Sudo docker run 
  -sudo docker run -d --name encode-decode-ui-local -p 3005:80 encode_decode_ui:0.3 
  -local port is 80
  -your container port is 3005
  -your container name is encode-decode-ui-local
  
#dont require docker run if you are using portainer
  -simply use the portainer click on your container click on duplicate edit and change your container version and deploy
  
 
# your influx2.0 dbr mappping for running query in influx1.0
  -influx2.0 uses the flux database
  -influx1.0 uses QL database
  -so missverion he dont except the commands of v2 in v1
  -i.e why we can map using dbr mapping
  -

############################# INFLUX DB ############################
"![Screenshot from 2023-03-31 12-29-06]("https://user-images.githubusercontent.com/68800883/229046678-ade729ac-f252-44f8-8f5c-551939f1db21.png")"

influx v1 dbrp create --db people-counting --rp autogen --bucket-id a681dc0dc3d6dd31 --default --org smarti --token -PfPbsN-HEOL_rH-ydFg_UfSslXjD-ir59yV1WEBITv5SsDovNTK9GmC19CGZ93TQ6MqrDNWoVgx12kc_Qhb9Q==



ID                      Database        Bucket ID               Retention Policy        Default Organization ID
0a133836026a2000        people-counting a681dc0dc3d6dd31        autogen                 true    6f74bb30691fdd56



https://community.influxdata.com/t/how-to-connect-grafana-to-influxdbv2-by-influxql-method/17377/12?u=grant1


##################################### redis setup   ################################
 cmd :
  1. docker pull redis:6
  2. docker run -d --name redis -p 6379:6379 redis
  
 - go to the portainer and click on redis container click on duploicate button and choose option first change the port 
 *** Publish all exposed network ports to random host ports ** please unabele this option and disable *** Enable access control  ***
 









############################# INFLUX DB ################################################################

# to use ago, just now time in react js use moment 
  - moment.utc("2019-12-04 12:00:24").local().startOf('seconds').fromNow()
  - moment("20111031", "YYYYMMDD").fromNow(); // 8 years ago
  -moment("20120620", "YYYYMMDD").fromNow(); // 7 years ago
  -moment().startOf('day').fromNow();        // 16 hours ago
  -moment().endOf('day').fromNow();          // in 8 hours
  -moment().startOf('hour').fromNow();  
  
  
  # to convert query time in time format  
    -fetch time convert to string to 
    
    
    ##########################################  react ##########################
    
    npm i react-router-dom --force   or npm i anylibirary --legacy-peer-deps  // use for unable salved dependency tree error
    
    
    
        ########################################## for UML sequence diagram diagram ########################
        1. go to visual studio and install palntuml dependecies
        2. seq.uml
   
############################ postgres set maxval ################################################
purpose : to increment the default set primary key value 
reason : postgres has set default value as as starting i.e. current value so we need to told postgres please set you highest value which you not use
SELECT setval('product_master_product_id_seq',
    (SELECT MAX(product_id) FROM product_master));
    
    
=================================== create only one database access user =======================

-- Create Role First
CREATE ROLE tagid_genesis_read;
GRANT CONNECT ON DATABASE tagid_chunmun_ginesys TO tagid_genesis_read;

-- For Read/Write Access To the Above Created ROLE.
CREATE SCHEMA tagid_gen_schema;
GRANT USAGE, CREATE ON SCHEMA tagid_gen_schema TO tagid_genesis_read;
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA tagid_gen_schema TO tagid_genesis_read;
ALTER DEFAULT PRIVILEGES IN SCHEMA tagid_gen_schema GRANT SELECT,INSERT,UPDATE,DELETE ON TABLES TO tagid_genesis_read;
GRANT USAGE ON ALL SEQUENCES IN SCHEMA tagid_gen_schema TO tagid_genesis_read;
ALTER DEFAULT PRIVILEGES IN SCHEMA tagid_gen_schema GRANT USAGE ON SEQUENCES TO tagid_genesis_read;


-- Grant the Above Created ROLE to the said User.
GRANT tagid_genesis_read TO nitin;
https://www.youtube.com/watch?v=-2kYJ0gZmCo
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO nitin;

===============================================================================================================
**git vscode setup**
git fetch --all

Fetching origin
remote: Repository not found.
fatal: Authentication failed for 'https://github.com/iam-rnd/tagid-dashbord-ui.git/'
error: Could not fetch origin


git remote -v

origin  https://github.com/iam-rnd/tagid-dashbord-ui.git (fetch)
origin  https://github.com/iam-rnd/tagid-dashbord-ui.git (push)


git remote set-url origin https://token@github.com/iam-rnd/tagid-dashbord-ui.git

origin  https://token@github.com/iam-rnd/tagid-dashbord-ui.git (fetch)
origin  https://token@github.com/iam-rnd/tagid-dashbord-ui.git (push)

git remote -v


docker run -d  -p 8001:8001 redislabs/redisinsight:1.13.1
