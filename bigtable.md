## Cloud Big Table

Fully managed NoSQL, wide-column DB for terabyte apps

- petabyte scale with very low latency
- accessed using HBase API
- native compatibility with big data, Hadoop ecosystems
- in flight/at rest encryption
- same DB used in maps/gmail/etc
- single-row transactions
- 10Mb/cell, 100Mb/row max size

> The table is composed of rows, each of which typically describes a single entity, and columns, which contain individual values for each row.
> Each row is indexed by a single row key and columns that are related to one another are typically grouped together into a column family.

Data ingestion:
- Application API
- Streaming: Spark/Dataflow streaming/Storm
- Batch processing: Hadoop MapRecude, Dataflow, Spark


---
### Time seires / schema design

see https://cloud.google.com/bigtable/docs/schema-design-time-series#time-series-cloud-bigtable

>Storing time-series data in Cloud Bigtable is a natural fit.

There are two commonly used ways to retrieve data from Cloud Bigtable:
- You can get a single row by specifying the row key.
- You can get multiple rows by specifying a range of row keys.
