# CephFS Metadata and Consistency

MDS authority, persistent placement, client capabilities, and internal locks describe different mechanisms. Related: [[knowledge/distributed-systems/ceph/architecture|architecture]] and [[knowledge/distributed-systems/ceph/data-placement|data placement]].

## I. Metadata Storage and MDS Roles

### 1. Metadata Pool

**Core idea: Persist filesystem structure in RADOS while MDS coordinates its interpretation.**

Directory and inode metadata require coordinated changes, not just independent object writes. MDS caches and journals these changes; persistent metadata is not stored only in its memory. CephFS metadata pools require replicated storage, including support for OMAP. [Source: filesystem pool requirements](https://docs.ceph.com/en/tentacle/cephfs/createfs/).

### 2. Data Pool

**Core idea: Store file contents and some filesystem auxiliary information.**

A filesystem can use multiple data pools. The default data pool also stores inode backtraces, used for hard-link management and recovery; data-pool trouble can therefore affect metadata operations as well as file contents. Pool and MDS-rank numbers are unrelated. [Source: default data pool](https://docs.ceph.com/en/tentacle/cephfs/createfs/#creating-pools).

### 3. MDS Rank

**Core idea: Assign one logical share of metadata service to an active daemon.**

Multiple active ranks divide metadata work, including subtrees and directory fragments. Ranks are not interchangeable full-namespace replicas, and clients are not permanently assigned to one rank. Increasing active ranks scales metadata service; it does not add RADOS replicas. [Source: multiple active MDS daemons](https://docs.ceph.com/en/tentacle/cephfs/multimds/).

### 4. Metadata Authority

**Core idea: Coordinate changes through the MDS currently authoritative for the affected metadata.**

A client can contact several ranks; requests can be forwarded, and non-authoritative MDSs can serve some reads under coordinated locks. Authority can migrate. An idle rank cannot simply take over arbitrary requests while another still owns the relevant state. [Source: distributed metadata authority](https://docs.ceph.com/en/tentacle/cephfs/mdcache/).

### 5. Standby MDS

**Core idea: Keep a daemon available to replace a failed active rank.**

A standby does not normally share the active rank's client workload. Taking over changes the daemon serving a logical rank, not where that rank's persistent data is placed; a shared PG or storage failure may remain after failover. [Source: standby roles](https://docs.ceph.com/en/tentacle/cephfs/standby/).

### 6. Standby-Replay

**Core idea: Follow one active rank's journal to prepare for takeover.**

Replaying keeps a warm metadata state but does not make the standby another active worker. A standby-replay daemon follows one rank; distinguish its cache warnings and statistics from those of the active daemon. [Source: standby-replay](https://docs.ceph.com/en/tentacle/cephfs/standby/).

### 7. MDS Journal

**Core idea: Record metadata changes durably so service can recover after a crash.**

The journal resides in RADOS and supports replay. Old segments can be trimmed after their changes are safely persisted elsewhere. Trimming lag concerns metadata-log retirement, not deletion of users' files; long replay can also affect takeover time. [Source: MDS journaling](https://docs.ceph.com/en/tentacle/cephfs/mds-journaling/).

## II. Client Capabilities and Caches

### 1. Client Session

**Core idea: Identify a filesystem client's relationship with an MDS.**

A client ID is not a human, process, or Pod ID. A mounted client may serve many processes, so paths and request counts alone do not identify the originating application. Inspect session information and client-side evidence together. [Source: client/session troubleshooting](https://docs.ceph.com/en/tentacle/cephfs/troubleshooting/).

### 2. Capability

**Core idea: Delegate per-inode data and metadata access or caching to a client.**

MDS coordinates these grants with other clients and internal locks. They are neither Unix permission bits nor the identity-level [[knowledge/distributed-systems/ceph/architecture#2. CephX|CephX authorizations]]. A valid grant can let a client use cached state without another metadata request. [Source: CephFS capabilities](https://docs.ceph.com/en/tentacle/cephfs/capabilities/).

### 3. Fsc and Fscb

**Core idea: Decode a compact set of file-class capabilities, not a single lock name.**

`F` identifies the file class; `s` permits shared metadata caching, `c` permits data read caching, and `b` permits write buffering. Thus `Fscb` adds buffering to `Fsc`. Data read/write grants use separate `r`/`w` bits; caching bits alone are not access permissions. [Source: capability abbreviations](https://docs.ceph.com/en/tentacle/cephfs/capabilities/).

### 4. Fb (Write Buffering)

**Core idea: Allow a client to buffer file writes before sending them to OSDs.**

Returning this capability can require dirty-data writeback and metadata synchronization. A pending return does not prove the client is still writing or quantify its dirty bytes. This is a client grant, not an MDS-internal mutex. [Source: file buffering capability](https://docs.ceph.com/en/tentacle/cephfs/capabilities/).

### 5. Capability Revocation

**Core idea: Withdraw conflicting grants before another operation can proceed consistently.**

Conflicting access can trigger revocation without memory pressure. Delayed release may reflect client, network, or writeback problems; it can delay lock-state transitions. Compare requested and outstanding capability sets with the deployed version's log format. [Sources: distributed cache coordination](https://docs.ceph.com/en/tentacle/cephfs/mdcache/); [late-release warnings](https://docs.ceph.com/en/tentacle/cephfs/health-messages/).

### 6. MDS Cache Recall

**Core idea: Ask clients to release cached metadata so MDS can shrink its own cache.**

Client-held state can pin MDS cache entries. `CLIENT_RECALL` concerns response to cache pressure; `CLIENT_LATE_RELEASE` concerns delayed capability release. Neither warning alone proves physical-memory exhaustion, and cache-size targets are not hard process-memory ceilings. [Sources: cache configuration](https://docs.ceph.com/en/tentacle/cephfs/cache-configuration/); [health messages](https://docs.ceph.com/en/tentacle/cephfs/health-messages/).

### 7. Client Eviction

**Core idea: Remove a client's ability to continue using its filesystem session.**

Eviction and blocklisting coordinate exclusion from MDS and OSD access. Buffered data may be lost, and the affected mount can serve many processes. It is not equivalent to canceling one stuck request or restarting one application. [Source: CephFS client eviction](https://docs.ceph.com/en/tentacle/cephfs/eviction/).

## III. Metadata Objects and Locks

### 1. Inode

**Core idea: Identify a filesystem object independently of a pathname used to reach it.**

Directories have inodes too. A directory's own attributes, its entries, and a child's attributes are different targets; a request against one does not automatically describe all three. MDS uses different locks for different portions of this state. [Source: inode and dentry locking](https://docs.ceph.com/en/latest/dev/mds_internals/locking/).

### 2. ifile

**Core idea: Protect file-related inode state such as size, timestamps, and truncation information.**

Each inode has its own lock state, so `ifile` on a child and on its parent are different locks. Directory inodes also have file-related state. Client file capabilities interact with this lock's state machine. [Source: `CEPH_LOCK_IFILE`](https://docs.ceph.com/en/latest/dev/mds_internals/locking/#lock-types).

### 3. isnap

**Core idea: Coordinate snapshot-related inode state used by ordinary metadata operations too.**

Seeing `isnap` does not imply a user is creating a snapshot. A request holding its read lock can delay another request needing an exclusive lock on the same inode. Locks on other inodes remain separate. [Source: `CEPH_LOCK_ISNAP`](https://docs.ceph.com/en/latest/dev/mds_internals/locking/#lock-types).

### 4. MDS Lock State Transition

**Core idea: Change which operations and capabilities are allowed before acquiring a requested lock.**

`excl → sync` denotes a transition, not two lock holders. Modes include `rdlock`, `wrlock`, and `xlock`; `wrlock` can permit concurrent writers under FileLock/ScatterLock rules, so it is not a generic exclusive mutex. Capabilities may need revocation before a transition finishes. [Source: MDS lock modes and states](https://docs.ceph.com/en/latest/dev/mds_internals/locking/).

### 5. getattr

**Core idea: Retrieve attributes of one filesystem object.**

For a directory, this concerns that directory's own inode attributes, not every child's attributes or its full entry list. A blocked request can retain locks obtained before its current wait; the requested attribute set and lock state matter. [Sources: metadata requests](https://docs.ceph.com/en/tentacle/cephfs/mdcache/); [MDS locking](https://docs.ceph.com/en/latest/dev/mds_internals/locking/).

### 6. readdir

**Core idea: Enumerate directory entries.**

This differs from querying the directory's own attributes. An operation whose last event says `acquired locks` can still await later work, including backend reads; that event is not a completion marker. [Source: tracing incomplete MDS operations](https://docs.ceph.com/en/tentacle/cephfs/troubleshooting/).
