# Kubernetes Networking Basics

* All nodes can talk to each other (Node network)
    * Port 443 (HTTPS)
    * Kubelet talks to the API server on this network
    * Not implemented by Kubernetes
* All pods can talk to each other (Pod network)
    * Pod network big + flat
    * Stretched across each node
    * Each node gets allocated to an IP address range
    * Implemented by CNI plugin
* Every pod gets its own IP address
    * Pods scheduled to nodes get an IP in the node range

# Service Basics

* Each service gets a stable, unchanging name & IP
    * Both are registered with the cluster’s native DNS service (i.e. CoreDNS)
    * So every pod in the cluster can resolve name -> IP
* Uses a Label selector to balance traffic across all pods that match label criteria
    * Creating a Service with a Label Selector creates an Endpoint object with a list of pod IP’s matching selector
    * Service watches the apiserver for new pods with label and updates endpoint

# Service Types

## ClusterIP (default)
* Gives a service its own IP address
* Only accessible from within cluster

## NodePort
* Also gets a clusterIP address
* Also gets a cluster-wide port to give access to outside cluster
    * Append port to any node IP to get access
    * Default port range is 30000-32767, can specify in YAML
    
## LoadBalancer
* Integrates with cloud platform load balancer
    * Some cloud platforms give access by way of NodePort

# Service “Network"

* Not really a network
* Every node has one pod called kube-proxy as a part of a DaemonSet
* Writes IPVS/IPTABLES rules routing traffic from service IP’s to Pod IP's
* When a pod sends traffic to a service, DNS translates name to IP
    * Pod then sends packets/data to its virtual ethernet interface 
    * Service network is separate, the internet sends the packets to its default gateway, Linux bridge called cbr0 (custom bridge 0)
    * Packets then get sent to the eth0 interface and are processed by the host kernel to use IPVS/IPTABLES rules
    * Then re-routed to the proper pod IP

* Kube-proxy in IPTABLES mode default since Kube 1.2
    * Doesn’t scale well
    * Designed for filtering for firewall, not load balancing 

* Kube-proxy in IPVS mode stable since Kube 1.11 
    * Use Linux kernel IP Virtual Server
    * Natively intended as a Layer-4 load balancer 
    * Uses hashes to scale better than IPTABLES 
    * Supports more algorithms