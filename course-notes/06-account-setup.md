# Free Tier - GCP Accounts

## GCP Free Trial
* Billing account that doesn’t get charged, has to be manually updated to paying account
* Still requires a credit card for verification
* $300 USD credit that lasts 12 months
* Not for business accounts, good for learning

## Free Trial Restrictions
* No more than 8 simultaneous vCPUs
* No GPUs, TPUs or quota increases
* No cryptomining or SLA’s, or premium OS licenses 
* No Cloud launcher products with extra usage fees

## Always Free
* Doesn’t count towards free trial credits
* Last beyond end of free trial
* 24h/day of f1-micro runtime in most US regions for Compute Engine
* 28h/day of App Engine in North America
* 2mil/month of cloud function invocations (with runtime/size limits)
* Always free storage averaged over the month
* 5 GB/month of regional cloud storage + some operations
* 1 GB/month of Cloud Datastore storage + some operations
* 10 GB/month of BigQuery storage with 1TB/month of query processing
* 30 GB of HDD storage on compute + app engine 
* 5 GB snapshot storage on compute + app engine
* 5 GB stackdriver logs with 7 day retention
* 1 GB/month of compute app engine egress

# Explore GCP Console
* To see billing info: Navigator -> Billing
* Can manage different billing accounts
* Can customize dashboard cards with drag + drop
* ‘Activity’ shows summary of all user activity for project
* Can change project name but not ID or number
* Can also see GCP status

# Setup Billing Export
* Navigation menu -> Billing -> Billing Export
* Must be created by billing account, not project
* Can create additional project for billing BigQuery dataset
* Can export billing data by project to BigQuery dataset (must create dataset tfirst)
* Billing delay can be hours

# Setup Billing Alert
* Navigation Menu -> Billing -> Bugets and alerts -> Create budget
* Can set alerts per project or accounts as well as a limit
* Can include credit and set percentages for alerts as well
* Can programmatically track as well using Google PubSub

# Setup Non-Admin User Access
* Billing account user role links projects to billing accounts
    * Permission can be granted at organization at billing account level
* Navigation menu -> Billing -> Info Panel -> Add members
    * Select ‘billing account user’ role
    * If billing account user creates project, admin can’t see it, even though they can see the billing account for the new project
* TLDR: Owning a project and controlling its resources is completely separate from controlling the billing account for the project