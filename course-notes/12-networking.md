# Routing to Google’s Network

* Google’s routing is cold potato, meaning that it takes responsible for tunneling data at different
    * Makes data routing more predictable
    * Reduces exposure to the rest of the internet
    * Also benefits because Google can choose nearest destination to access, instead of specific resource like standard networking
* Opposed to hot potato, routing, meaning that it tries to make data someone else’s problem

# Load Balancing

* Cross-region load balancing 
    * Global Anycast IP points to Google network, load balancer points traffic to closest site
    * reduces latency
* Cloud Load Balancer 
    * All types, internal + external
* HTTP(S) Load Balancer

## Routing Schemes
* Unicast - There is only one unique device in the world that can handle traffic
* Anycast - There are multiple devices to handle traffic, send to any one but prefer closest

## OSI Model
* TCP of TCP/IP is Layer 4
    * Works solely with IP addresses
* HTTP(S) is Layer 7
    * Know about URLs/Paths
* Higher levels are built upon lower levels, Layer 7 needs to route based on info at Layer 4

# Routing Among Resources (VPC)

* VPC (Virtual Private Cloud) - your private SDN space in GCP
* Subnets (regional) create logical spaces to contain resources
    * All subnets can reach all others globally
* Routes (global) define ’next hop’ for traffic based on destination IP
    * Global and apply by instance-level tags, not by subnet
* Firewall rules (global) further filter data flow
    * Apply by instance-level tag or service account
    * By default are restrictive inbound and permissive outbound
    
## IPs and CIDRs
* IP address is abc.def.ghi.jkl where each piece is 0-255
* CIDR block is group of IP addresses specified in <IP>/xy notation
    * Turn IP addresses into 32-bit binary number
    * /xy in CIDR notation locks leftmost xy bits in IP address
    * abc.def.ghi.jkl/32 is single IP because all 32 bits are locked
    * abc.def.ghi.jkl/24 is 256 because last 8 bits (jkl) can vary and 2^8 = 256
    * 0.0.0.0/0 means any IP 
* RFC1918 defines private (non-Internet) address ranges you can use:
    * 10.0.0.0/8, 172.16.0.0/12 and 192.168.0.0/16

# Creating VPCs

* Navigation Menu -> Networking -> VPC networks
* Default VPC has auto mode with a subnet in every GCP subnet
* Can specify firewall rules as well to allow/deny ingress/egress for IP addresses, service accounts, protocols and ports

# Custom-Mode VPCs

* Can also have custom subnet creation mode with new subnets in specified regions
* Each custom subnet specified IP address ranges as well
* When creating instances, can specify VPC, subnets and network tags