# Dress4Win

https://cloud.google.com/certification/guides/cloud-architect/casestudy-dress4win-rev2

## Overview

- web-based wardrobe mgmt
- social networking around fashion
- monetizes vai ads

## pain points

- current infra can't keep up with company growth
- need to future-proof themselves
- innovation stified due to hardware constraints

## goals

- POC deployment to GCP
    - migrate dev/test envs
    - build DR
        - think hybrid networks (GCP connect to on-premises)
    - of successful will work toward full cloud migration
- need to map current env to GCP equivalents
- prefer managed services

## what do they care about

- manage costs
    - initial cloud investment
    - scaling down capacity during off-peak times
- competitors
- agility
    - quickly provision resources
     -have room to innovate withou waiting on hardware
- secure env
    - IAM, customer supplied encryption, firewall rules
- global footprint not a priority - cloud be a future possibility

## Business reqs

- build a reliable and reproducibel env with scaled parity of production
    - without re-engineering exisiting apps
- security
    - principle of least privilege
    - separate dev/test env into separate projects
- agility
    - automate infra creation
        - gcloud/SDK
        - deployment manager, etc
        - marketplace for easy deployments (tomcat, nginx, jenkins, etc)
- analyze and optimize architecture for performance in the cloud
    - stackdriver
        - monitoring, logging, debug/error reporting

## technical requirements

- easily create non-prod in the cloud
- implement an automation framework for provisioning resources in cloud
    - deployment manager
- CI/CD
    - jenkins, spinnaker, cloud build
- fialover to cloud
    - replication
        - MySQL -> Cloud SQL
    - DNS cutover
- encrypt data on the wire and at rest
    - CSEK
- multiple private connections DC <-> cloud
    - VPC/cloud interconnect

### Existing env

- Databases:
    - MySQL. 1 server for user data, inventory, static data, MySQL 5.7 8 core CPUs 128 GB of RAM 2x 5 TB HDD (RAID 1)
        -> Cloud SQL, lift and shift, replica in cloud -> promote to master
- Compute
    - 40 Web Application servers providing micro-services based APIs and static content.
        - managed instance group -> autoscaling
        - GKE/GAE for microservices deployment
    - 20 Apache Hadoop/Spark servers
        - cloud dataproc
            - can connect to cloud storage
    - 3 RabbitMQ servers for messaging, social notifications, and events
        - cloud pub/sub
        - exact same env on compute engine instance group
    - Miscellaneous servers:
        - Jenkins, monitoring, bastion hosts, security scanners
            - -> GCE instances, cloud marketplace
- Storage appliances:
    - iSCSI for VM hosts, Fibre channel SAN - MySQL databases
        - 1 PB total storage; 400 TB available
        - SAN/iSCSI -> block storage -> PD
    - NAS - image storage, logs, backups
        - 100 TB total storage; 35 TB available
        - Cloud storage
