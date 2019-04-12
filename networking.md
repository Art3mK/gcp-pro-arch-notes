# Networking

- VPC networks have global scope, subnets can span the zones that make up a region.
- you can have resources in different zones on the same subnet
- you can dynamically increase the size of a subnet in a custom network by expanding the range of IP addresses allocated to it, without affecting already configured VMs.

## Network

- max 5 per project
- Has no IP address range
- is global and spans all available regions
- contains subnetworks
    - subnet can extend across zones in the same region
    - single firewall rule can apply to both VMs even though tehy are in different zones
    - two VMs could be on the same subnet but in differente zones
    - first address is reserved for router
- can be of type:
    - default
    - auto mode
    - custom mode

You can convert auto mode network to custom mode network, but "once custom, always custom"

## IP addresses


## VPC

- built-in route tables
- global distributed firewall
- shared VPCs
- VPC peering

### VPNs and stuff

![alt](./images/networking-interconnect.png)

- cloud router (BGP) for VPN connections
- direct peering with Google (shared DC in AWS terms?)
- private dedicated interconnect (DC in AWS?)
