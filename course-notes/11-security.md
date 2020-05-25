# What is Security?

* Authentication - are you who you say you are
* Authorization - should you be able to access this
* Accounting - keep record of the access/request

## Key Security Products/Features - Authentication
* Identity
    * Humans use G Suite & Cloud Identity
    * Apps & services use Service Accounts
* Identity Hierarchy
    * Google groups
* Can use Google Cloud Directory Sync (GCDS) to pull from LDAP (no push)

## Key Security Products/Features - Authorization
* Identity Hierarchy (Google Groups)
* Resource Hierarchy (Organization, Folders, Projects)
* IAM - Permissions, Roles, Bindings
* GCS Access Control Lists (ACLs)
* Billing management
* Networking structure & restrictions

## Key Security Products/Features - Accounts
* Audit/Activity Logs (Stackdriver)
* Billing export - to BigQuery or GCS bucket (json/csv)
* GCS Object Lifecycle Management

# IAM Breakdown

## Resource Hierarchy
* Resource - something you create in GCP
* Project - container for a set of related resources
* Folder - contains any number of projects and subfolders
* Organization - tied to G Suite or cloud domain
* Organization -> Folder -> Project -> Resources
* By default, resources in projects can access each other, but not in other projects

# IAM Breakdown - Permissions & Roles

## Permissions
* Follows the form Service.Resource.Verb (example pubsub.topics.publish)
* Usually correspond to REST API methods

## Roles
* A Role is a collection of Permissions to sue or manage GCP resources
* Primitive Roles - Project-level and often too broad
    * Viewer is read-only
    * Editor can view and change things
    * Owner can also control access + billing
* Predefined roles - Give granular access to specific GCP resources
* Custom role - Project or org-level collection of predefined roles

# IAM Breakdown - Members & Groups

## Members
* A member is some Google-known identity (ID’d by unique email address)
* Types of members:
    * User: Specific google account (G Suite, Cloud Identity, Gmail, other validate email)
    * serviceAccount: service account for apps/services
    * group: Google group of users and service accounts
    * domain: Whole domain managed by G Suite of cloud identity
    * allAuthenticatedUsers: Any Google account or serviceAccount
    * allUsers: Anyone on the Internet (public)
    
# IAM Breakdown - Policy

## Policies
* A policy binds members to roles for some scope of resources
* Attached to some level in the Resource Hierarchy (org, folder, project, resource)
* Roles and members listed in policy, but resources idefntified by attachment
* Always additive and never subtractive
* Child policies cannot restrict access granted at a higher level
* One policy per resource
* Max 1500 member bindings per policy
* Max 250 group bindings per policy
* Takes <60s to apply changes

## Managing Policy Bindings
* Can use `get-iam-policy`, edit JSON/YAML, and `set-iam-policy` back (bad)
* Better approach:  
    * `gcloud <GROUP> add-iam-policy-binding <RESOURCE-NAME> —role <ROLE-ID> —member user:<email>`
    * `gcloud <GROUP> remove-iam-policy-binding <RESOURCE-NAME> —role <ROLE-ID> —member user:<email>`
    * Avoids race conditions

# Billing Access Control

## Billing Accounts
* Represents some way to pay for GCP service usage
* Resource that lives outisde of projects
* Can belong to an organization, inherits org-level IAM policies
* Can be linked to projects, but doesn’t own them (no link to project IAM)

## Billing IAM Roles
* Billing Account User - link billing accounts to project (Org or billing account scope)
* Billing Account Creator - create new self-serve billing accounts (org scope)
* Billing Account Admin - manage billing accounts (but not create) (billing account scope)
* Billing Account Viewer - view billing account cost info and transactions (billing account scope)
* Project Billing Manager - link/unlink the project to/form a billing account (project scope)

## Monthly Invoiced Billing 
* Get billed monthly and pay by invoice due date
* Can pay via check or wire transfer
* Can increase project and quota limits
* Billing admin of org’s current billing account contacts Cloud Billing Support to apply to switch over
* Eligibility depends on account age, typical monthly spend, country