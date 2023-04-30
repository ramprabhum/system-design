# Functional Requirements
- Use cases
- Scenarios that will not be covered 
- Consumer and consuming patterns

# Non-Functional Requirements & Design Goals
- How many will use
- Latency and Throughput requirements
- Consistency vs Availability

## Estimations
- Throughput (QPS for read and write queries)
- Latency expected from the system (for read and write queries)
- Number of servers/shards required for Appliction/Datasources
- Read/Write ratio
- Traffic estimates
  - Write (QPS, Volume of data)
  - Read  (QPS, Volume of data)
- Storage estimates 
- Memory estimates
  - If we are using a cache, what is the kind of data we want to store in cache
  - How much RAM and how many machines do we need for us to achieve this ? 
  - Amount of data you want to store in disk/ssd

# System View /System Anatomy / Microservices
## Breath Problem
- Systems required to build the solution
- Integration Pattens of the systems
## Depth Problem
- System in detail
- Algorithms used in solving the problem


# Design Deep Dive
## Design Considerations
## Detailed view
- The algorithm
- Individual components
  - Availability, Consistency and Scale story for each component
  - Consistency and availability patterns 
  - Integration Patterns
- APIs
- Database Schema
- Risks & Tradeoffs
## Think about the following components, how they would fit in and how it would help
- DNS 
- CDN [Push vs Pull] 
- Load Balancers [Active-Passive, Active-Active, Layer 4, Layer 7] 
- Reverse Proxy 
- Application layer scaling [Microservices, Service Discovery] 
- DB [RDBMS, NoSQL]
  - RDBMS
  - Master-slave, Master-master, Federation, Sharding, Denormalization, SQL Tuning
  - NoSQL
  - Key-Value, Wide-Column, Graph, Document 
- Fast-lookups:
  - RAM  [Bounded size] => Redis, Memcached
  - AP [Unbounded size] => Cassandra, RIAK, Voldemort
  -CP [Unbounded size] => HBase, MongoDB, Couchbase, DynamoDB
- Caches
  - Client caching, CDN caching, Webserver caching, Database caching, Application caching, Cache @Query level, Cache @Object level
  - Eviction policies:
    - Cache aside
    - Write through
    - Write behind
    - Refresh ahead
- Asynchronism 
  - Message queues 
  - Task queues 
  - Back pressure
- Communication
  - TCP
  - UDP
  - REST
  - RPC
# Reliability/ Fault tolerance / Scaling / Performance / Security 
## Scale
- Scale for Storage (DB/Cache)
- Scale for through puts(CPU/IO)
- Scale for API paralleization 
- Hotspots possible?
- Availability of Geo Distribution
