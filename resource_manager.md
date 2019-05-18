# Resource manager

## Labels

- Attached to resources: VM, disk, snapshot, image
- console, gcloud, API
- max length of keys: 63 chars
- max 64 labels per resource
- values can be empty
- propagated through billing

labels != tags
- tags are applied to instances only
- used-defined strings
- tags are primarily used for networking (applying firewall rules)
