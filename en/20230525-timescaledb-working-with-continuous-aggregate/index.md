# TimescaleDB working with continuous aggregate


<!--more-->
**What is continuous aggregates**

....

**Working with continuous aggregates**
- Create a materialized view:
    ```sql
        CREATE MATERIALIZED VIEW daily_revenue_sum_by_reseller WITH (timescaledb.continuous) AS
        select time_bucket('1 day', "time") as timebucket,
            reseller_namespace, 
            sum(interval_amount) as daily_amount
        from billing_items bi
        group by timebucket, reseller_namespace
        WITH NO DATA;
    ```
    Use `WITH NO DATA;` so you can create view instancely, don't need to wait for refresh data. (With very large table, this will make problem with performace)
       
- Manually refresh the view:
    ```sql
        CALL refresh_continuous_aggregate('daily_revenue_sum_by_reseller', '2021-07-17', '2021-07-20');
    ```
	
	
- Add the policy:
    ```sql
        SELECT add_continuous_aggregate_policy('daily_revenue_sum_by_reseller',
            start_offset => INTERVAL '1 week',
            end_offset   => INTERVAL '1 hour',
            schedule_interval => INTERVAL '30 minutes');
    ```

- List all table and views
    ```sql
        SELECT * FROM information_schema.tables WHERE table_schema = 'public';
    ```

- List all jobs
    ```sql
        SELECT * FROM timescaledb_information.jobs;
    ```
- Enable of disable job by id
    ```sql
        SELECT alter_job(<JOB_ID>, scheduled => false);
        SELECT alter_job(<JOB_ID>, scheduled => true);
    ```

- Delete job
    ```sql
        SELECT delete_job(1000);
    ```
	  
- Automatically created indexes
	if you define a continuous aggregate view with GROUP BY device, location, bucket, two composite indexes are created: one on {device, bucket} and one on {location, bucket}.

- Turn off automatic index creation
    ```sql
        CREATE MATERIALIZED VIEW conditions_daily
        WITH (timescaledb.continuous, timescaledb.create_group_indexes=false)
        AS
        ...
    ```
	  
- Manual create index
    ```sql
        CREATE INDEX avg_temp_idx ON _timescaledb_internal._materialized_hypertable_2 (avg_temp);
    ```
    With **TimescaleDB < 2.7** you can't create an index on an aggregated column.

- How to find hypertable table name?
    ```sql
        SELECT view_name, format('%I.%I', materialization_hypertable_schema,
            materialization_hypertable_name) AS materialization_hypertable
        FROM timescaledb_information.continuous_aggregates;
    ```
	
- Drop view:
    ```sql
	    DROP MATERIALIZED VIEW daily_revenue_sum_by_reseller;
    ```

- For an existing table, at the psql prompt, disable real time aggregation:
    ```sql
	    ALTER MATERIALIZED VIEW table_name set (timescaledb.materialized_only = true);
    ```
	
- Re-enable real time aggregation:
    ```sql
	    ALTER MATERIALIZED VIEW table_name set (timescaledb.materialized_only = false);	
    ```

- Compress continuous aggregates
    ```sql
        ALTER MATERIALIZED VIEW cagg_name set (timescaledb.compress = true);
        ALTER MATERIALIZED VIEW cagg_name set (timescaledb.compress = false);
    ```
