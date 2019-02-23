# Postgres Playground for PG Partitions

## Overview

Leaen how to implement postgres partitioned tables in PG 10. 

Goals:

1. Creating tables with partitions
2. Dropping partitioned tables.
3. 

## SQL

### Creating Database and Table w. Partitions

```sql
create database markets;

drop table if exists epic_metadata;

create table epic_metadata (
	id int not null,
	data json,
	created_at date not null
) partition by range (created_at);

create table epic_metadata_201802 partition of epic_metadata for values from ('2018-02-01') to ('2018-03-01');
create index epic_metadata_201802_created_at on epic_metadata_201802 (created_at);
create table epic_metadata_201803 partition of epic_metadata for values from ('2018-03-01') to ('2018-04-01');
create index epic_metadata_201803_created_at on epic_metadata_201803 (created_at);
create table epic_metadata_201804 partition of epic_metadata for values from ('2018-04-01') to ('2018-05-01');
create index epic_metadata_201804_created_at on epic_metadata_201804 (created_at);
create table epic_metadata_201805 partition of epic_metadata for values from ('2018-05-01') to ('2018-06-01');
create table epic_metadata_201806 partition of epic_metadata for values from ('2018-06-01') to ('2018-07-01');
create table epic_metadata_201807 partition of epic_metadata for values from ('2018-07-01') to ('2018-08-01');
create table epic_metadata_201808 partition of epic_metadata for values from ('2018-08-01') to ('2018-09-01');
create table epic_metadata_201809 partition of epic_metadata for values from ('2018-09-01') to ('2018-10-01');
create table epic_metadata_201810 partition of epic_metadata for values from ('2018-10-01') to ('2018-11-01');
create table epic_metadata_201811 partition of epic_metadata for values from ('2018-11-01') to ('2018-12-01');
create table epic_metadata_201812 partition of epic_metadata for values from ('2018-12-01') to ('2019-01-01');
create table epic_metadata_201901 partition of epic_metadata for values from ('2019-01-01') to ('2019-02-01');
create table epic_metadata_201902 partition of epic_metadata for values from ('2019-02-01') to ('2019-03-01');
```

### Fill with 10m records

```sql
insert into epic_metadata (id, created_at)
select 
generate_series(1, 100000-0)
,NOW() - (random() * (interval '1 year'));
```

### Testing Counts cross partititons.

```sql
select count(*) from epic_metadata where created_at > '2018-05-22' and created_at < '2018-10-15'
```