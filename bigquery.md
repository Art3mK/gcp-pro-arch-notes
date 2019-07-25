## BigQuery

It's Google's fully manage petabyte scale, low cost analytics data warehouse

BigQuery is fast for wide-range queries, but it is not as well-optimized for narrow-range queries as Cloud Bigtable is. Latency will be an order of magnitude shorter with Cloud Bigtable for this use.

- You can load it from cloud storage or cloud data store, or stream it into Big Query at up to 100,000 rows per second
- SQL2011 queries on massive data sets
- separate billing for storing and processing data
    - shared data set, you will not be billed for other ppl queries
- discount after storing data for 90 days
    - If you have a table that is not edited for 90 consecutive days, the price of storage for that table automatically drops by 50 percent to $0.01 per GB, per month. This is the same cost as Cloud Storage Nearline.
    - Each partition of a partitioned table is considered separately for long-term storage pricing. If a partition hasn't been modified in the last 90 days, the data in that partition is considered long term storage and is charged at the discounted price.
- partitioned tables on date, clustering on column to colocate related data
    - clustering is supported only on partitioned tables
    - Maximum number of partitions per partitioned table: 4000
    - Maximum number of partitions modified by a single job: 2000
    - Maximum number of partition modifications per day per table: 5000
    - Maximum rate of partition operations: 50 partition operations every 10 seconds

## Quotas

https://cloud.google.com/bigquery/quotas#streaming_inserts

## data expiration

You can update a dataset's default table expiration time by:

- Using the GCP Console or the classic BigQuery web UI
- Using the bq update CLI command
- Calling the datasets.patch API method

You can set a default table expiration time at the dataset level, or you can set a table's expiration time when the table is created.
If you set the expiration when the table is created, the dataset's default table expiration is ignored'

You can update a dataset's default partition expiration by:
- Using the bq update CLI command
- Calling the datasets.patch API method

Setting or updating a dataset's default partition expiration is **not currently supported** by the GCP Console or the classic BigQuery web UI. Currently, you cannot apply different expiration times to different partitions in the same table.
