<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Introduction](#introduction)

<!-- /TOC -->

# Introduction

* Small data
* Medium data
  * Fits on one machine
  * Handles several hundred concurrent users
  * Using RDBMs like MySQL, PostgreSQL
    * ACID guarantees
    * Typically scale vertically
    * Third NF doesn't scale
    * Denormalize for performance
    * Sharding is a nightmare
      * Querying secondary indexes requires hitting every shard
      * Adding shards requires moving data, typically manually
      * Schema changes are difficult to manage
    * HA (multi-DC) is complicated and requires additional operational overhead
  * Lessons learnt from RDBMs - Features in the dream DB
    * Consistency is not practical - so give it up. Eventual consistency instead
    * Manual sharding and rebalancing is hard - so build it in
    * Moving parts makes systems complex - simplify: no more master/slave
    * Scaling up is expensive - commodity hardware should be ok
    * Scatter / gather no good - data modeling goal should be to hit a single
    machine to answer a query
* Cassandra
  * No master-slave; no SPOF
  * Multi-DC
  * HA
  * Linear scalability
  * Hash ring
    * Location of data is determined by partition key
    * Any node can answer read/write queries
  * AP system, in context of CAP theorem
  * Replication determined by replication factor configuration
    * RF per key space per datacenter
    * missing data is replayed via hinted handoff if a machine is down
  * Per query consistency
    * All
    * Quorum
    * One
* Choosing a distribution
  * The write path
    * Writes are written to an append only commit log
    * Merges mutation to in-memory representation called `memtable`, which is flushed to disk periodically (`sstable`)
      * memtable to sstable happens behind the scenes, asynchronously
    * Cassandra is a write optimized database
    * Every write includes a timestamp
    * Deletes via tombstones
  * The read path
    * Data is pulled from SSTables and merged, using timestamps where the most
    recent timestamp wins
    * Read heavy load should use a SSD as choice of disk impacts read
    performance
    * Consistency < All performs a read repair in background
    (read_repaid_chance)
  * Distributions
    * Apache Cassandra
      * OSS support - jira, distribution lists
    * DataStax Enterprise
      * Lags behind the bleeding edge version
      * Extra QA, support etc
      * Multi-DC search, Lucene queries  
