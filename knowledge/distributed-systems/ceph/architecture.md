# Ceph Architecture and Access

Distinguish storage interfaces, service processes, deployment tools, and logical placement. They are cooperating layers, not a serial `CSI → MON → MDS → PG → OSD` pipeline.

## I. Storage Interfaces

### 1. CephFS

**Core idea: Expose files and directories over RADOS.**

MDS coordinates metadata and client capabilities; clients normally transfer file contents directly with OSDs. Valid cached state can avoid some MDS round trips. See [[knowledge/distributed-systems/ceph/cephfs|CephFS metadata and consistency]]. [Source: CephFS metadata cache](https://docs.ceph.com/en/tentacle/cephfs/mdcache/).

### 2. RBD

**Core idea: Expose a virtual block device backed by RADOS objects.**

Image layout maps block offsets to objects. Files inside a filesystem placed on that image are interpreted by that filesystem, not by CephFS MDS. Image metadata and data can use the same pool or configured separate pools. [Source: RBD images and striping](https://docs.ceph.com/en/tentacle/man/8/rbd/).

### 3. RGW

**Core idea: Provide an object-storage gateway that translates requests into RADOS operations.**

RADOS Gateway supports S3/Swift APIs. An upper-level object can involve several RADOS objects, plus index and metadata objects; sharing a pool does not make it appear as a CephFS file. Application payloads pass through RGW. [Source: RGW data layout](https://docs.ceph.com/en/tentacle/radosgw/layout/).

### 4. RADOS

**Core idea: Supply the common distributed object-storage foundation.**

Reliable Autonomic Distributed Object Store underlies CephFS, RBD, and RGW. The common object model does not require these services to share one pool or understand one another's layouts. See [[knowledge/distributed-systems/ceph/data-placement|objects and placement]]. [Source: Ceph architecture](https://docs.ceph.com/en/tentacle/architecture/).

## II. Service Roles

### 1. MON

**Core idea: Maintain authoritative cluster maps and authentication through a monitor quorum.**

MON serves the whole cluster, not only CephFS. Clients obtain maps and authentication information, then contact the relevant services; MON does not relay normal file contents. [[knowledge/distributed-systems/reliability#1. Quorum|Quorum]] concerns control-state agreement, not file replication. [Source: Ceph monitor architecture](https://docs.ceph.com/en/tentacle/architecture/#the-ceph-storage-cluster).

### 2. MGR

**Core idea: Provide management modules, metrics, and orchestration integration.**

Manager functionality includes dashboard and monitoring endpoints. A functioning MGR or dashboard does not establish that every data path works. MGR and MON have different responsibilities despite both appearing in cluster status. [Source: Ceph daemon roles](https://docs.ceph.com/en/tentacle/architecture/#the-ceph-storage-cluster).

### 3. OSD

**Core idea: Run object storage, replication or encoding, recovery, and scrubbing on local storage.**

An Object Storage Daemon is a service instance, not a server. One host commonly runs several OSDs; each OSD can hold data for many PGs from multiple pools. Device layouts need not be one physical disk per OSD. [Source: Ceph OSD architecture](https://docs.ceph.com/en/tentacle/architecture/#storing-data).

### 4. BlueStore

**Core idea: Store an OSD's objects and metadata on local block devices.**

BlueStore manages object data directly rather than representing each object as an ordinary host file. Its main block device can have separate DB/WAL devices, so an I/O error must be traced through the actual device mapping. [Source: BlueStore devices](https://docs.ceph.com/en/tentacle/rados/configuration/bluestore-config-ref/).

### 5. MDS

**Core idea: Coordinate the shared namespace and cached metadata of CephFS.**

Metadata Server responsibilities include directories, inode state, layouts, and capabilities. Persistent metadata lives in RADOS; active MDS ranks divide authority rather than each serving as an interchangeable copy of the entire namespace. [Source: multiple active MDS daemons](https://docs.ceph.com/en/tentacle/cephfs/multimds/).

## III. Deployment and Client Access

### 1. Ceph CLI

**Core idea: Query a remote cluster using a configured management client.**

The `ceph` command needs reachable services, configuration, and credentials; it need not run on an OSD host. `sudo` changes local privileges, not the Ceph identity's authorization. `ceph --version` describes the local client; `ceph versions` queries daemon versions. [Source: cluster monitoring and client configuration](https://docs.ceph.com/en/tentacle/rados/operations/monitoring/).

### 2. CephX

**Core idea: Authenticate clients and daemons and authorize their service access.**

Keys, tickets, and service authorizations govern access to MON, OSD, MDS, and other services. These identity-level authorizations are distinct from the per-inode [[knowledge/distributed-systems/ceph/cephfs#2. Capability|CephFS capabilities]] used for caching and consistency. [Source: CephX architecture](https://docs.ceph.com/en/tentacle/architecture/#high-availability-authentication).

### 3. Rook

**Core idea: Manage Ceph services with a Kubernetes operator.**

Rook reconciles Ceph resources and daemon workloads in Kubernetes. A toolbox Pod is one management-client environment, not the only possible way to query Ceph. Running Pods alone do not prove storage health. [Source: Rook overview](https://rook.io/docs/rook/latest/Getting-Started/intro/).

### 4. cephadm

**Core idea: Deploy and manage containerized Ceph daemons across hosts.**

cephadm integrates with Ceph's orchestrator and does not require Kubernetes. A Kubernetes workload can consume a separately managed Ceph cluster; finding a working `ceph` CLI does not identify the deployment method. [Source: cephadm](https://docs.ceph.com/en/tentacle/cephadm/).

### 5. CSI

**Core idea: Connect a container orchestrator's volume lifecycle to a storage system.**

Container Storage Interface drivers prepare, publish, and mount volumes. After mounting, normal application I/O uses the established client path, rather than passing through the CSI controller. Installing Ceph CSI does not mean Ceph daemons themselves run in Kubernetes. [Source: CSI introduction](https://kubernetes-csi.github.io/docs/introduction.html).
