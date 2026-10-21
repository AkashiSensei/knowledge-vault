# Distributed Storage Reliability

Reusable concepts from the Ceph learning notes; implementation details belong in the [[knowledge/distributed-systems/ceph/README|Ceph notes]].

## I. Redundancy and Placement

### 1. Replication

**Core idea: Keep multiple complete copies of the same logical data.**

Splitting a file into different chunks distributes its contents; copying each chunk adds redundancy. Three copies of each of three chunks produce nine chunk copies, not three different chunks with one copy each. See [[knowledge/distributed-systems/ceph/data-placement#3. Replica Placement|Ceph replica placement]]. [Reference: Ceph replicated pools](https://docs.ceph.com/en/tentacle/rados/operations/pools/).

### 2. Erasure Coding

**Core idea: Encode data into data and parity shards so some missing shards can be reconstructed.**

A typical `k+m` code stores `k` data shards and `m` parity shards, with ideal space overhead `(k+m)/k`. Reconstruction requires enough valid shards; actual availability also depends on system policy and failure placement. See [[knowledge/distributed-systems/ceph/data-placement#4. Erasure-Coded Placement|Ceph encoding]]. [Reference: Ceph erasure coding](https://docs.ceph.com/en/tentacle/rados/operations/erasure-code/).

### 3. Failure Domain

**Core idea: Separate redundant data across resources that can fail together.**

Different disks on one host do not protect against losing that host. Host, rack, and other topology levels express different correlated-failure boundaries. See [[knowledge/distributed-systems/ceph/data-placement#5. CRUSH Failure Domain|CRUSH failure domains]]. [Reference: CRUSH topology](https://docs.ceph.com/en/tentacle/rados/operations/crush-map/).

## II. Coordination

### 1. Quorum

**Core idea: Require a sufficient set of participants to agree before advancing shared state.**

The threshold and protocol depend on the system. Ceph MON uses majority agreement: three monitors need two for quorum. This control-service quorum is separate from a data pool's replica count or `min_size`. See [[knowledge/distributed-systems/ceph/architecture#1. MON|MON]]. [Reference: Ceph monitor consensus](https://docs.ceph.com/en/tentacle/architecture/#high-availability-monitors).
