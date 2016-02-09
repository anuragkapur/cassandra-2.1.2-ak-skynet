Cassandra Installation on ak-skynet
===================================

## What is this?
This repo houses the cassandra setup on my development machine. I like version controlling *everything*!

## Commands
### Starting the server
    {cassandra_home}/bin/cassandra

### Opening a cqlsh session against a running server
    {cassandra_home}/bin/cqlsh

### Check version
Simply login to CQLSH and the version number is displayed      
Example: 

    -sh-4.1$ cqlsh -u admin -p '********'
    Connected to CassandraCluster at localhost:9160.
    [cqlsh 4.1.1 | Cassandra 2.0.15 | CQL spec 3.1.1 | Thrift protocol 19.39.0]
    Use HELP for help.
    cqlsh>
    
### Create a new keyspace
    CREATE KEYSPACE {keyspace_name} WITH REPLICATION = {'class' : 'SimpleStrategy', 'replication_factor' : 1};
        
### List all keyspaces
    describe keyspaces;   
         
### Use a keyspace
    use {keyspace_name};
         
### Describe a keyspace (to view schema of all tables)         
    describe keyspace {keyspace_name};
    
### Drop keyspace
    drop keyspace {keyspace_name}         

### Simple select
    select * from {table_name} where {column_name}={value} limit 10;

## Setup Info
### Data dir
    {cassandra_home}/data

### Logs dir
    {cassandra_home}/logs
    
### Auth details for local setup
    admin/admin
    
    
