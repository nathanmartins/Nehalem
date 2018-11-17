
# Setup instructions for local development 

## Required software: 
- go (https://golang.org/doc/install)
- dep (https://golang.github.io/dep/docs/installation.html)
- Docker (https://docs.docker.com/install/)

--- 

### 01. Run inside the desired package 'rest_api, web_app, ect.'
`dep ensure`

### 02. Start the cassandra cluster:
` docker run --name dev_cassandra -d -p 9042:9042 -p 7000:7000 -p 7001:7001 -p 7199:7199 -p 9160:9160 cassandra`

### Wait 30s for db to start 

### 03. Them start the cli session:
` docker run -it --link dev_cassandra:cassandra --rm cassandra cqlsh cassandra`

### 04. Run the following commands in the db cli session to create database and tables:
```sql
CREATE KEYSPACE nehalem WITH replication = {'class':'SimpleStrategy', 'replication_factor' : 1};
USE nehalem;
CREATE TABLE users(
    id UUID PRIMARY KEY,
    username text,
    password text,
 ); 
```
