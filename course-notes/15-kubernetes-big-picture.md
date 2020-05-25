# Kubernetes Primer

* Platform for cloud-native apps
    * Built from small, interactive, pre-defined services to form an app
    * Often containerized, can scale and update easily
* Consists of VM’s in control plane and workers
    * Control plane consists of apiserver, scheduler, controllers and persistent store (etcd)
    * Etcd the only stateful aspect of the controle plane
        *  tough to scale in production
    * All requests to update stuff are done through apiserver
        * Scheduler and controller take care of the mechanics of executing requests
        * Apps run on the worker nodes

# Kubernetes API

* RESTful API that supports CRUD operations through the `kubectl` CLI
    * Define app components in YAML files
    * Authenticate properly
    * Use `kubectl` to send a POST to the kube-apiserver
    * Creates a record of intent in the etcd store which changes the desired cluster state
* Kubernetes uses a declarative configuration
    * Control plane constantly compares the desired cluster state and actual cluster state 
    * Components of the control plane update the actual state to match the desired
* API separated into four groups: core, apps, authorization, storage
    * Each group developed and versioned independently 
        * Alpha versioning: take extreme caution (i.e. v1alpha1)
        * Beta versioning: becoming more stable (i.e. v2beta1)
        * Prod ready (i.e. v1, v2)

# Kubernetes Objects

* Pod
    * Wraps one or more containers
    * Atomic unit of scheduling in the cluster
    * Defined in the v1 API group
* Deployment
    * Defined in the apps/v1 API group
    * Wraps pods to make them scalable, updatable
* DaemonSet
    * Ensure that exactly one pod runs on each node in cluster
* StatefulSets
    * For pods that have stateful components