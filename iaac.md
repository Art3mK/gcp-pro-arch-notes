# Deployment manager

- yaml could include templates in python/jinja2
- `gcloud deployment-manager deployments update accel --config *.yaml --preview`
- max 10Mb
- time/compute constraints
- no system/network calls for python
- templates can be nested
    - reusable assets
    - isolate specific functions
- can have properties
- can use env variables
- supports the startup script and metadata capabilities
- deployments can be updated - uses GCP API
    - add resources: default policy is to acquire or create as needed
    - remove resources: default policy is to delete the resource
- https://github.com/GoogleCloudPlatform/deploymentmanager-samples.git
