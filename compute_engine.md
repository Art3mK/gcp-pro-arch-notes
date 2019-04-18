# Compute engine

## Pricing

- 1 minute minimum, per-second billing, sustained use discounts
- preemtible instances (up to 80% discount)
- custom machine types
- recommendation engine
- commited use discounts
- usage of VMs of the same machine type in the same zone is combined as if they were one machine (inferred instances)
- no charge for stopped VM (still chardeg for attached disks and IPs)

## Lifecycle

![alt](./images/vm_lifecycle.png)

## Machine types

- high CPU/MEM
- standard
- shared-core

---
features:
- vCPU == 1 hyperthreaded core
- 2 vCPU == 1 physical core
- network scales at 2 Gbit/s for each CPU core up to a max 16 GB/s (8 vCPUs)

## Preemptible VMs

- Live at most 24 hours
- no charge if terminated in the first 10 minutes
- can be pre-empted with a 30-second notification via API
- up to 80% discount
- no live migrate, no auto restart

## Persistance storage

- standard (up to 64 Tb per instance)
- SSD (up to 64 Tb per instance)
- local SSDs (max 3Tb per instance, 8 partitions x 375 Gb)
- can be attached in read-only mode to multiple VMs
- checksums built-in, automatic encryption

![alt](./images/vm-disks.png)

### Local SSD disks

- not available on shared core
- up to 8 local disks, 375Gb each == 3TB
- data survives a reset, but not a VM stop or terminate (cannot be reattached to a different VM)
- can use your own encryption keys

### Snapshots

- not available for local SSDs
- incremental backup to cloud storage
- snapshots can be restored to a new persistent disk

## Availability policies

- live migration (default)
- terminate + automatic restart (default, could be disabled)

## Images

- premium images (p)

# Instance groups

- Allows to manage groups of compute engine instances
- simple mgmt tasks:
    - monitor CPU, disk, network IO across the group
    - reboot all instances in the group

## Types

- managed groups
    - use template to define properties for every instance in the group
    - deployes identical instances based on **instance template**
    - group can be resized
    - manager ensures all instances are in running state
    - typically used with an autoscaler
- unmanaged groups
    - collection of instances not necessarily identical

## Autoscaling

- in a managed instance group
- reduce costs by shutting down extra instances
- create one autoscaler per managedd instance group
- autoscalers can be used with zone-based or regioanal managed instance groups

### policices

- CPU
    - threshold for group avg CPU usage
- http reqs per seconds/instances
    - LB specifies max req per seconds
- stackdriver metrics
    - gauge
    - delta/min
    - delta/second
- multiple metrics options
    - up to 5 policies based on those three metric options
    - autoscaler selects policy with most amount of available servers

## Load balancing

![alt](./images/lbs.png)

- no pre-warming required

### Network

- TCP
- UDP
- HTTP(S)
- SSL

allows packet inspection, point to target pool if instances in region

forwarding rules:
- to pools
- to target instances
- optional health checks
- session affinity
- auto scaling

### HTTP

- distributes traffic among groups of instances based on
    - proximity to the user
    - request URL

requires instance groups (managed/unmanaged)
- session affinity
- auto scaling
- connection draining

# TODO
- create instance group with autoscaler
- network/http load balancer

# Links

- https://cloud.google.com/compute/docs/vpc/
- https://cloud.google.com/compute/docs/
