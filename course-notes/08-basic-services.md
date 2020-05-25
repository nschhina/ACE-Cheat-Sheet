# Google Cloud Storage Bucket Setup

* Buckets must have globally unique names (across all GCP)
    * Storage class (Multi-regional -> USA, Europe, etc, Dual-regional or Regional -> us-central, us-west1, etc)
    * Can choose  Standard, Nearline, Coldline, Archive (goes from most to least frequently accessed)
    * Fine-grained (object-level) vs uniform (only IAM) access permissions
    * Encryption can be a google or customer-managed key
    * Can also add retention policy to protect bucket objects from deletion for time period, as well as labels
* To make object publicly visible, add permission user with name ‘allUsers’ and access ‘reader'
* ‘Edit Bucket’ changes storage class or retention policy for new objects (location cannot be changed)
* Can also add users to the entire bucket

# Google Cloud Storage CLI with `gsutil` (Enabled by default)

* `gsutil ls` lists all buckets (formatted as ‘gs://bucket-name')
    * `gsutil ls gs://bucket-name` lists all object in the bucket root 
    * `gsutil ls -a gs://bucket-name` lists archival objects in bucket (with versioning, only visible from CLI)
    * `gsutil ls gs://bucket-name/folder-name` for everything in folder 
    *  `gsutil ls gs://bucket-name/**` for everything in bucket as flat list
* `gsutil mb gs://bucket-name` makes a bucket
* `gsutil label`:
    * `gsutil label get gs://bucket-name` outputs json with the labels for the bucket
    * `gsutil label set labels.json gs://bucket-name` adds labels in ‘labels.json’ to bucket
    * `gsutil label set labels.json gs://bucket-name` adds labels in ‘labels.json’ to bucket
    * `gsutil label ch -l “label:value" gs://bucket-name` adds label to bucket
* `gsutil versioning`: 
    * Versioning basically keeps files archived even if deleted 
    * `gsutil versioning get gs://bucket-name` checks if versioning is supported for bucket
    * `gsutil versioning set on|off gs://bucket-name` turns versioning on/off for bucket
* `gsutil cp`:
    * `gsutil cp file gs://bucket-name` copies local file to bucket object
    * `gsutil cp gs://bucket1/file1 gs://bucket2` copies file1 on bucket1 to bucket2
* `gsutil rm gs://bucket-name/object-path` removes object from bucket
* `gsutil acl ch -u AllUsers:R gs://bucket-name/object-path` makes object on bucket publicly visible

## GCE VM Setup With Google Compute Engine (Disabled by default)
* `gcloud services:` shows all the enabled API’s for the current project
    * `gcloud services list` shows all the enabled API’s for the current project (Storage enabled by default)
    * `gcloud services list —-available` shows all the API’s that can be enabled for the current project
    * `gcloud services enable|disable service-url` enables/disables the given service
    * Must run `gcloud services enable compute.googleapis.com` to enable and use the Compute Service 
        * Also enables:
        * Cloud OS Login API
        * Compute Engine default service account
        * Google API’s Service Agent
        * Compute Engine Service Agent
* `gcloud compute instances`:
    * `gcloud compute instances list` shows all the Compute VM's
    * `gcloud compute instances create vm-name` creates VM
    * `gcloud compute instances delete vm-name` delete VM

# gcloud Overview

* Command-line tool to interact with GCP
* Shares config set by gcloud storage with gsutil and bq 
* In general more powerful than console but less powerful by REST API
* Alpha + beta versions available through gcloud alpha|beta
* `gcloud <global flags> <service/product> <group/area> <command> <flags> <params>`
    * Example: `gcloud —-project myprojid compute instances list`
* Global flags:
    * `-h|—-help`
    * `—-project <ProjectID>`
    * `—-account <Account>`
    * `—-filter`
    * `—-format` (json, yaml, csv, etc)
    * `—-quiet|-q` (don’t prompt user to confirm)
    
## Config properties
* Values entered once and used by any command that needs them
* Can be overriden on a specific command with corresponding flag
    * core/account or account -> —-account
    * core/project or project -> —-project
    * compute/region -> —-region
    * compute/zone -> —-zone
* `gcloud config set <property> <value>` to set 
* `gcloud config get get-value <property>` to get 
* `gcloud config unset <property>` to unset

## Configurations
* Can maintain groups of settings and switch between them (useful for multiple projects
* `gcloud init` to interactively create a config with common config properties
* `gcloud config list` lists config properties for current config
* `gcloud config configurations list` lists all configs (active shown with IS_ACTIVE)
* `gcloud config configurations create NAME` creates config
* `gcloud config configurations activate NAME` switches config (or just use global flag `—configuration=NAME`)

# GCE In and Out

* `gcloud compute machine-types list` shows all GCE instance types
    * i.e. `gcloud compute machine-types list —filter=“NAME:f1-micro AND ZONE~us-west"` shows all free GCE instance types
* `gcloud compute instances create —machine-type=TYPE vm-name` creates VM with specified type
* `gcloud compute ssh vm-name` SSH’s into VM and creates SSH keys in local dir
* Service account for Compute API automatically linked to VM to authenticate GCP API requests

# GCE via Console

* gcloud config linked to gcloud only and not the GCP console
* Can set default region & zone in Compute Engine Settings
* SSH Keys viewable in ‘Metadata’ settings
* Instance settings:
    * Region & zone (default)
    * Machine type (shows how many vCPU’s and RAM, can customize) as well as CPU platform
    * Can deploy container automatically to VM instance
    * Boot disk can select OS image, app image, custom image, image snapshot, existing disk
    * Identity and API access (choose service account, GCP API access)
    * Firewall, Management, security, disks, networking, sole tenancy, labels etc
    * Can run a startup script to install software/updates and set metadata for VM
* In instance details can ‘Create Similar’ which populates new instance with same settings
* Preemptible instance costs much less and lasts at most 24 hours
* Can SSH into VM from console from ‘Connect’ tab
* IMPORTANT: Everything than happens from SSH is done by the SERVICE account, while CLI & console is done by user