# Quick-notes: Working with postgresql on ubuntu


<!--more-->
**Quick-notes: Working with postgresql  on ubuntu**

## Install PostgreSQL server

## Install PostgreSQL client

## PostgreSQL client with GUI

## Quick Notes
- Get all running query
  ```sql
    SELECT pid, state, query, age(clock_timestamp(), query_start) AS query_age, psa.*
    FROM pg_stat_activity psa
  ```
- Miscellaneous
  ```bash
    pg_lsclusters
    sudo pg_dropcluster 14 main --stop
    sudo pg_upgradecluster 12 main    
  ```
