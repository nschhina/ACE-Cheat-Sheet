# Kubernetes App Theory

* Service can act as an external load balancer or as an internal component to be accessed by other components in the cluster
* Deployments can scale pods which wrap containers to serve things like web frontends
    * Similarly, stateful sets can manage pods that wrap backend containers
* Secrets are used to help deployments talk to each other
* Persistent Volume and Persistent Volume claim (requests for storage) can be used for storage (i.e. databases)
* Resources can hook into other services outside the cluster