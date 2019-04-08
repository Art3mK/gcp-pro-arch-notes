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

# Roles

- primitive roles
    - viewer
    - editor
        - deploy apps
        - modify code
        - configure services
        - remove members
    - owner
        - CRUD on members
        - delete projects
        - permissions to set up billing administrator
    - billing administrator
- predefined roles, more fine grained role for specific roles
    - instanceAdmin role for compute engine
- custom roles
    - only at project or organization level, not at folder level

# IAM and admin

Identities:
- google accounts
    - ppl personal accounts
- service accounts
    - named with email address, `project_id@appspot.gserviceaccount.com`, `project_number-compute@developer.gserviceacount.com`
    - google manages keys for computer engine and app negine
    - service account is also resource
        - Alice can have an editor role in a service account and Bob can have the viewer role? WTF
    - app accounts
- google groups
    - collection of ppl and service accounts
- google app domains or cloud identity (example.com)
    - virtual group of all the members in an organization

**Who** _can do what_ `on which resources`

## Permissions

```
<service>.<resource>.<verb>
pubsub.subscriptions.consume
```

Can't assign permissions to users, only to roles

# Accessing GCP

## web shell

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

## Cloud Console Mobile App

- dashboards, etc
