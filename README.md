# Postgres Playground

An area to play with Postgres features.

## Goals

There's lot's of interesting areas and methods I'd like to dive into.

1. Query Planner
1. PG Internals/pg_catalog
1. Table Partitioning
1. DELETE Performance
1. Table Inheritance
1. Replication
4. Disaster Recovery
1. Window Functions
1. Logical Replication
1. Log Shipping
1. Failover
1. Hot Standby
1. Advanced Tuning
1. TX Wraparound Issue and Monitoring
1. General Monitoring
1. WAL
1. Advanced Indexes
1. Foreign Data Wrappers
1. Views & Materialized Views

## Services

Docker Compose is user to setup a postgres instance and pgAdmin as an interface.

	$ docker-compose up -d

- Postgres is exported on port 5432
- PgAdmin is exported on port 54321

### postgres

Postgres is exported on port 5432. You connect using any pg capable client.

Default user is postgres, password is blank?

### pgAdmin4

PgAdmin is exported on port 54321 and can be access via your web browser.

http://localhost:54321

### psql support

	$ psql postgres://postgres@localhost/dbname
