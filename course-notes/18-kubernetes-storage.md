# High-Level Storage Requirements

* Kubernetes volumes decouple storage from Pods
    * Allows for resiliency as pods crash or go down often
    * Can share volumes between multiple pods
* Container Storage Interface (CSI) Allows enterprise storage backends to connect to Kubernetes PV's
    * Not an official part of Kubernetes API
* Persistent Volume (PV) is the storage object
* Persistent Volume Claim (PVC) is the ticket to use PVC
* Storage Class (SC) allows for dynamic storage

# Kubenetes PV System

* Matches PV to PVC through request storage amount, access mode and storage class name 
    * 3 access modes for PV:
    * ReadWriteOnce (RWO) - can only be mounted once by a pod for read/write access
    * ReadWriteMany (RWM) - can be mounted by many pods for read/write access
    * ReadOnlyMany (ROM) - mounted by many pods for read-only access
    * PV can have multiple access modes, but pod can only access a PV in one mode at a time
    * Not all PV’s support all access modes
* Reclaim policy:
    * Delete means when a PVC is deleted, delete PV and storage object on external backend
    * Retain (default) keeps PV when PVC or pod is deleted, has to be manually deleted

# Storage Classes

* StorageClasses are given a provisioner (AWS, GCP, etc), wrap external storage objects as Kube objects
    * Each provisioner is given a plugin that providers parameter specs for the specific object
    * Give PV params like access mode and reclaim policy
    * Also give backend provisioner-specific storage params
* Can then reference StorageClassName PVC, and PVC as claimName in podSpec
* PV Subsystem runs a control loop constantly monitoring the apiserver for new PV objects and dynamically creates them
