# CLI commands

## gcloud

- `gcloud config list`
- `gcloud config set project`
- `gcloud config set compute/region`
- `gcloud config set compute/zone`
- `gcloud compute instances move`
- `gcloud compute images create web-v1 --family=webserver --source-disk=web-1 --source-disk-zone=us-central1-a`
- `gcloud services enable cloudkms.googleapis.com`
- `gcloud beta compute firewall-rules list --filter="network:mynetwork"`
- `gcloud deployment-manager deployments create advanced-configuration --config nodejs.yaml`
- `gcloud compute instances create "preempt" --preemptible --no-boot-disk-auto-delete`

## gsutil

- `gsutil signurl -d 10m path/to/privatekey.p12 gs://bucket/object`
- `gsutil ls -a gs://bucket`
- `gsutil -m cp (source and target destination)` - multi-thread copy
- Upload big files parallel in chuncks, up to 32 component pieces: `gsutil -o GSUtil:parallel_composite_upload_threshold=150M cp bigfile gs://your-bucket`
- `gsutil rsync -d -r s3://my-s3-bucket gs://my-gs-bucket`

## bq

- create partitioned table: `bq mk --time_partitioning_type=DAY --time_partitioning_expiration=259200 [PROJECT_ID]:[DATASET].[TABLE]`

### expiration
- Dataset: `bq update --default_table_expiration 7200 myotherproject:mydataset`
- Table: `bq update --expiration 432000 myotherproject:mydataset.mytable`
- Partitioned table:
    - default: `bq update --default_partition_expiration [INTEGER] [PROJECT_ID]:[DATASET]`
    - `bq update --time_partitioning_expiration 432000 myotherproject:mydataset.mytable`

## Cloud Source Repos

- `gcloud alpha source repos create REPO_NAME`

## GKE

- resize node pool:
    - `gcloud container clusters resize project-1 --node-pool 'primary-node-pool' --size (или --num-nodes) 20`

## dataproc

- `gcloud dataproc clusters create [cluster_name] --zone [zone_name]`
- `gcloud dataproc clusters update [cluster_name] --num-workers [#] --num-preemptible-workers [#]`
