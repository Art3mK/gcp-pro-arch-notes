### zones
- single point of failure
- i.e. compute engine resources

### multi-regional services:
- app engine
- cloud datastore
- cloud storage
- big query

- custom compute engine machine types

## Projects

Dev/Test/Prod projects

identifiers:
- project name (user friednly name), chosen by you, mutable
- project ID (globally uniq scope, can't be changed), chosen by you, immutable
- project number (generated automatically), assigned by GCP, immutable

user for:
- managing API
- billing
- adding/removing collaborators
- each resource belongs only to one project

Operate via:
- cloud console
- resource manager API
    - list of all projects
    - create/update/delete/recover

### Folders

One can organize projects in folders
- teams/deps/apps/etc
- use folders to assign policies
- organization node required

# Organization node

```
Organization nodes let you apply policies centrally. Organization nodes are optional, but if you want to define policies that apply to all the projects in your organization, having one is mandatory. Also required for creating folders.
```

- top of the hierarchy
- some special roles associated with organization node
- The policies implemented at a higher level in hierarchy can't take away access that's granted at a lower level.
```
if G Suite -> do not need to do anything
else { create one }
```

# Accessing GCP

## cloud shell

- tiny ephemeral VM
- CLI pre-installed
    * gcloud: for working with Google Compute Engine and many GCP services
    * gsutil: for working with Cloud Storage
- SDK APIs pre-installed
- 5Gb user data persists
- kubectl: for working with Google Container Engine and Kubernetes
- bq: for working with BigQuery
- Language support for Java, Go, Python, Node.js, PHP, and Ruby
- Web preview functionality
- Built-in authorization for access to resources and instances

> After 1 hour of inactivity, the Cloud Shell instance is recycled. Only the /home directory persists. Any changes made to the system configuration, including environment variables, are lost between sessions.

## Cloud SDK

- available is docker image

## gcloud

aws like

## gsutil

cloud storage

## bq

Biq Query stuff

## RESTful APIs

- typically use JSON as an interchange format
- use OAuth 2.0 for authn and authz
- enabled through gcp console
- many are off by default and many includes daily quoats and rates
- APIs Explorer could be used to learn APIs

## Client Libraries

- Cloud Client Libraries (community owned, hand-crafted client libraries)
- Google API client libraries (OSS, generated, support various languages)
- App APIs provide access to services, optimized for supported languages such as NodeJS and Python
- Admin APIs offer functionality for resources mgmt.

## Cloud Console Mobile App

- dashboards, etc

## Transfer appliance

the same thing as snowball

-> cloud storage, bigQuery

options:
- 100 TB
- 480 TB

Before being stored on Transfer Appliance, all captured data is deduplicated, compressed and encrypted with an industry standard AES 256 algorithm using a password and passphrase that you specify. You must specify the same password and passphrase to rehydrate — unencrypt, uncompress, and reconstruct — your data once it is uploaded to Google Cloud Platform (GCP).

To rehydrate your data, you run the Transfer Appliance Rehydrator application (VM on GCE) and specify a Cloud Storage destination bucket. Once all of your data is rehydrated to the destination bucket, run data integrity checks to make sure everything transferred completely and with no corruption.

The Transfer Appliance Rehydrator compares the CRC32C hash value of each file being rehydrated with the hash value computed when the file was captured.
