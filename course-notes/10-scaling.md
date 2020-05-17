# Managed Instance Groups

* Instance templates are a group of predefined settings to use when creating VM (can be done for any region + zone)
* Instance templates are immutable but can be copied
* Managed instance group has identical stateless instances from a template, supports autoscaling, autohealing, rolling updates, load balancing, etc
    * Can autoscale by different things like CPU usage, can target CPU usage, min & max instances
    * Can specify zones to use for multi-region, autoscaling balances nodes across regions
    * Cool-down period is how long to wait before logging (not include startup tasks)
    * Autohealing can specify a health check
    * Deleting group deletes all managed instances
* Unmanaged can load balance dissimilar instances, autoscaling etc is not supported, multi-region not supported either
    * Can add existing instances to this group
    * Deleting group doesn’t delete instances