Cassandra Installation on ak-skynet
===================================

## What is this?
This repo houses the cassandra setup on my development machine. I like version controlling *everything*!

## Commands
### Starting the server
    {cassandra_home}/bin/cassandra

### Opening a cqlsh session against a running server
    {cassandra_home}/bin/cqlsh
    
### Create a new Keyspace
    CREATE KEYSPACE {keyspace_name} WITH REPLICATION = {'class' : 'SimpleStrategy', 'replication_factor' : 1};    

## Setup Info
### Data dir
    {cassandra_home}/data

### Logs dir
    {cassandra_home}/logs
    
