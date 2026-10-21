# Ceph Knowledge

Concise concepts extracted from the conversation “查看 Ceph 信息与排查命令” and checked against primary references. Start with the [[knowledge/distributed-systems/ceph/data-placement|storage mapping diagram]] when the layers are unfamiliar.

## I. Topics

- [[knowledge/distributed-systems/ceph/architecture|Architecture and access]]: CephFS, RBD, RGW, RADOS, MON, MGR, MDS, OSD, BlueStore, CephX, Rook, cephadm, and CSI.
- [[knowledge/distributed-systems/ceph/data-placement|Data placement]]: objects, pools, PGs, file layout, CRUSH, redundancy, epochs, acting/up sets, peering, and recovery.
- [[knowledge/distributed-systems/ceph/cephfs|CephFS metadata and consistency]]: metadata/data pools, MDS ranks and authority, standby/replay, journals, capabilities, caches, and inode locks.
- [[knowledge/distributed-systems/ceph/operations|Status and troubleshooting]]: health checks, request/backlog interpretation, lock-wait propagation, backend I/O, device mapping, and read-only queries.

Shared definitions: [[knowledge/distributed-systems/reliability|replication, erasure coding, failure domains, and quorum]]. Parent index: [[knowledge/distributed-systems/README|distributed systems]].

## II. Sources and Illustration

The source conversation examined Ceph 20.2.4 (Tentacle). These notes were reviewed on 2026-10-21 and use Tentacle documentation where available. The MDS locking reference is explicitly a development document; the batching reference is pinned to the conversation's Ceph source revision. Generalized examples explain mechanisms rather than assert the state or resolution of that incident. Operational usernames, host/device identifiers, and raw diagnostic logs are not reproduced.

`assets/ceph-storage-mapping.svg` is an unchanged copy of the explanatory figure approved in that conversation. It retains its Chinese labels and illustrative topology and is embedded before the concepts in [[knowledge/distributed-systems/ceph/data-placement|data placement]]. The lock-wait Mermaid schematic is a separate explanatory synthesis, with its assumptions stated beside it.
