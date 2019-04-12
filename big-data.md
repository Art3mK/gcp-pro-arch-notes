# Big Data services

![alt](./images/big-data.md)

## Dataproc

Cloud Dataproc is a fast, easy, managed way to run Hadoop, Spark, Hive, and Pig on Google Cloud Platform

- 1s billing

## Cloud dataflow

- processs data using compute engine instances
- automated instance scaling
- data pipelines
- transform-based programming model

## BigQuery

It's Google's fully manage petabyte scale, low cost analytics data warehouse

- You can load it from cloud storage or cloud data store, or stream it into Big Query at up to 100,000 rows per second
- SQL2011 queries on massive data sets
- separate billing for storing and processing data
    - shared data set, you will not be billed for other ppl queries
- discount after storing data for 90 days

## Pub/Sub

- messaging service
- many-to-many async messaging
- support for offline consumers
- at least once delivery at low latency (duplicates!)
- foundation for dataflow streaming
- push notifications for cloud-based apps
- connect apps across GCP services (push/pull betweeb compute and app engine)


## Cloud datalab

- built on jupyter
- какая-то хуевина для датасатанистов
- analyze data in bigquery, compute engine, and cloud storage using python, sql, javascript
