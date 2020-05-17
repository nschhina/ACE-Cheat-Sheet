## Compute Products
* Compute Engine - VM’s, Disks, Network, rented by second (Like EC2)
* App Engine - Managed app platform
* Cloud Functions - Event-driven serverless, rented by tenth of second (Like Lambda) - function runs when event happens
    * Events can be http, object uploaded to cloud storage, pub-sub, etc
* Kubernetes Engine (GKE) - Managed Kubernetes/Containers (Like EKS) - also creates stuff like load balancers
    
## Storage Products
* Cloud Storage - Object Storage and Serving (data not changed but can be added) (Like S3)
* Nearline + Coldline - Cloud storage priced for backups that are accessed rarely
* Persistent Disks - VM-attached disks (block storage, like a hard drive)
    * Connects only with Compute engine resources
* Cloud Filestore - Managed NFS server
 
## AI/ML Products
* Cloud TPU - Specialized Compute Engine for ML (Tensorflow Processing Unit)
* Cloud NLP, Speech-to-Text, Text-to-Speech, Cloud Vision API, Dialogflow (Pre trained)
* Cloud Machine Learning Engine - Managed Platform for ML
* Cloud Deep Learning VM Image 
* Cloud AutoML NLP, AutoML Translate, AutoML Vision - basic models set up, but can train on your own data

## Database Products
* Cloud SQL - Managed single MySQL/Postgres instance
* Cloud Spanner - Horizontally Scalable RelationalDB
* Cloud Firestore - Strongly-consistent Serverless Document (NoSQL DB)
* Cloud Datastore - Horizontally Scalable NoSQL
* Cloud Bigtable - Petabyte-scale. low-latency, NoSQL (good for high volume and predictability)
* Cloud Memorystore - Managed Redis

## Data/Analytics
* Cloud Dataproc - Managed Spark + Hadoop (Uses Compute Engine under the hood) 
* Cloud Dataflow - Managed Apache beam (stream + batch data processing) 
* Google Genomics - For specialized medical data
* Cloud Pub/Sub - Global real-time messaging topics (very flexible)
* Google BigQuery - Data Warehouse/Analytics (Serverless, Scales up with low latency)

## Networking
* VPC - Software Defined Netwokring
* Dedicated Interconnect - Private network connection between stuff like VPC and external data center
* Cloud NAT - Network Address Translation Service
* Cloud Load Balancing - Multi-region Load Distribution
* Network Service Tiers - Optimize network for performance and cost
* Cloud Armor - DDOS Proection and WAF
* Cloud CDN, Cloud DNS

## Management Tools
* Stackdriver Monitoring - Infra/Application Metrics and Monitoring
* Stackdriver Logging - Centralized Logging

## Identity and Security Products
* Cloud Identity - Manage Users, Devices and Apps
* Cloud IAM - Resource Access
* Cloud HCM - Encryption keys, certificates
* Cloud Data Loss Prevention API - ML Service that removes sensitive data from connected endpoints