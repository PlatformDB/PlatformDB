# PlatformDB

A DB technology empowering developers with best practices from the top successful tech companies around the world

## What is it exactly 

PlatformDB has a few key components : 
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
- We expose common high level operations:
  - Append-only operations with common and efficient locking tricks
  - Explicit 2 phase commmit operations
  

## Why postgreSQL? 

PostgreSQL is an incredibly successful technology. Its performance has improved dramatically in the last 10 years and it is now widely used in production in many startups. 
