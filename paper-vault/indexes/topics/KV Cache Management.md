# KV Cache Management

## 2026-08

- [[paper-vault/papers/kwon2023pagedattention]]
  - Title: Efficient Memory Management for Large Language Model Serving with PagedAttention
  - Topic focus: KV-cache layout, growth, sharing, and recovery.
  - Why listed here: Separates logical sequence order from physical block placement and combines on-demand allocation with copy-on-write and preemption.

## 2026-09

- [[paper-vault/papers/fu2025c2c]]
  - Title: Cache-to-Cache: Direct Semantic Communication Between Large Language Models
  - Topic focus: KV-Cache as a cross-model semantic medium rather than a single-model reuse or paging target.
  - Why listed here: Treats the KV-Cache as something to project, fuse, and gate across different models, contrasting with same-model cache paging and exact prefix reuse.
