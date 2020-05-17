# GCP Context

* AWS is the biggest competitor to GCP
* Google is all about Big Data
* Published whitepapers, implemented some as open source and some in GCP
* GCP was built from dev -> infra, AWS built from infra -> dev
* GCP trying to catch up to AWS, some functionality missing
* Avoided some mistakes that AWS has 

# GCP Structure + Design

* GCP is intrinsically global vs AWS being regionally-scoped
* virtual CPU -> Physical server -> Rack -> Data center (building) -> Zones (independent) -> Region -> Multi-region -> Private global network -> Points of Presence (POPs, Network edges and CDN locations) -> Global System 

## Network Ingress & Egress
* Normal network routes via internet to edge location closest to destination
* Google routes so traffic enters from Internet at edge closest to source
    * Single global IP can load balance worldwide
    * Can opt for normal network behaviour to reduce price
    
## Pricing
* Provisioned - Resources are ready and up regardless of usage
* Usage - Charged based on usage
* Services built to charge based on either model - User can’t choose
* Network traffic - free ingress, egress charged by GB
    * Egress to GCP services sometimes free depending on service and service location

## Resource Quotas (Soft Limits)
* Regional + Global Scope
* Can be changed (automatic + by request)
* Queryable  with gcloud command

## Organization
* Projects are similar to AWS accounts
* Project owns resources (can be shared between projects)
* Projects can be grouped and controlled in hierarchy
