# PlatformDB

A DB technology empowering developers with best practices from the top successful tech companies around the world

## What is it exactly ?  

PlatformDB is mostly an abstraction layer on top of existing technologies (PosgreSQL) and embedding common best practices

It has a few key components : 
- **PlatformDB middleware**: a server exposing a new query language and implementing high level platform features:
  - Traditional CRUD operations, schema manipulation
  - A gRPC interface for OLTP operations 
  - Append Only and Immutability features
  - Connection pooling
  - Declarative transactions
  - A **read-only** SQL proxy to perform OLAP queries on the underlying back-end
- **PostgresQL** as the backend: your data ultimately goes to a PostgresQL. Easy install, backup, upgrade, hosting, etc. SQL is a fantastic  language for complex analysis and aggregations
- Client libraries in Go, JavaScript, Ruby, Python
- The `platform` cli: used for administration and interactive querying

## We optimize for best practices

Our mission to help developers integrate best practives from successful companies in an opiniated way. So we strongly encourage and discourage behaviors: 
- We add a 1000ms latency into the OLAP SQL interface to discourage using it for application code
- Transactions are only possible in a declarative way: this prevents stale transactions to be created (a major source of Db downtimes) from code
- We don't allow join queries: you are almost always better off not using them in production 
- We use UUIDv4 primary keys by default in all tables 
- We expose common high level strategies:
  - Append-only operations with common and efficient locking tricks
  - Explicit 2 phase commmit operations
  - Slow queries real time detection (issuing warnings about potential missing indices)
  

## Why use an existing DB as the back-end? Why PostgreSQL?

PostgreSQL is an incredible technology. Its performance has improved dramatically in the last 10 years and it is now widely used in production in many startups. There are many solutions available for:

- Cloud hosting
- SaaS Back-office solutions (Forest Admin, Retool)
- BI tools
- Back-up and replication tools
- etc. 

99% of tech companies only need 1 database. Our idea is to make PlatformDB gradually adopted, even in large codebases, without needing to manage another database server.
