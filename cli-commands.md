# CLI commands

## gcloud

- `gcloud config list`
- `gcloud config set project`
- `gcloud config set compute/region`
- `gcloud config set compute/zone`
- `gcloud compute instances move`
- `gcloud compute images create web-v1 --family=webserver --source-disk=web-1 --source-disk-zone=us-central1-a`

## gsutil

- `gsutil signurl -d 10m path/to/privatekey.p12 gs://bucket/object`

## bq

## Cloud Source Repos

- `gcloud alpha source repos create REPO_NAME`

## GKE

- resize node pool:
    - `gcloud container clusters resize project-1 --node-pool 'primary-node-pool' --size 20`
