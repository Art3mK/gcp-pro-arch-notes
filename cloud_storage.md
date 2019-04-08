# Cloud Storage

## Cloud storage

**Not a file system!**

- global uniq name for buckets, buckets are regional resources
- blob storage
- encrypts data by default
- immutable objects
- 4 storage classes
    - multi-regional (web site CDN, etc)
        - geo redundant, stores data in at least two geographic locations separated by at least 160km.
    - regional
    - nearline
        - access fee per GB of data read.
    - coldline
        - 90 days min. storage duration
        - costs for data access
        - higher per operation costs
- simple pricing model
    - ingress, data transfer within a region is free
    - egress costs $$, vary by destination
- data encryption at rest and in transit (HTTPS)
- lifecycle management policies
- 5Tb per object max size

![alt](./images/cloud_storage_classes.png)

### Import services

- online transfer
- storage transfer service
    - batch transfers from other region, other cloud providers, from HTTPS endpoints
- transfer appliance (offline, like snowball)

### ACLs

- permissions
    - READ/WRITE/FULL_PERMISSIONS
- scope or grantee
    - User or group
- each bucket or object ACL can hold up 100 entries
- predefined project roles
    - owner
    - editor
    - viewer
    - storage.admin
    - storage.objectAdmin (storage.objects.*)
    - storage.objectViewer (storage.objects.get, storage.objects.list)
    - storage.objectCreator (storage.object.create)

### Signed URLs

- ticket is cryptosigned URL
- TTL
- operations specified in ticket

`gsutil signurl -d 10m path/to/privatekey.p12 gs://bucket/object`

## Cloud Big Table

Fully managed NoSQL, wide-column DB for terabyte apps

- accessed using HBase API
- native compatibility with big data, Hadoop ecosystems
- in flight/at rest encryption
- same DB used in maps/gmail/etc
- single-row transactions
- 10Mb/cell, 100Mb/row max size

Data ingestion:
- Application API
- Streaming: Spark/Dataflow streaming/Storm
- Batch processing: Hadoop MapRecude, Dataflow, Spark

## CLoud SQL / amanged RDBMS

- MySQL
- PostgreSQL

Features:
- automatic replication and failover
- vertical/horizontal scaling (via read replicas)


## Cloud Spanner

Cloud Spanner can scale to petabyte database sizes, while Cloud SQL is limited by the size of the database instances you choose.

- strong transactional global consistency
- schemas
- automatic synchronous replication for HA
- SQL queries ANSI 2011 with extensions
- 10G/row max size

![alt](./images/storage-options-compare.png)
![alt](./images/storage-options-compare-2.png)
