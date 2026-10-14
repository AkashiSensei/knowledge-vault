# Cache-to-Cache (C2C)

## 2026-09

- [[paper-vault/papers/fu2025c2c]]
  - Title: Cache-to-Cache: Direct Semantic Communication Between Large Language Models
  - Role in paper: The paper's central method—direct semantic communication between LLMs by fusing a Sharer's KV-Cache into a Receiver's cache.
  - Mechanism: A trained neural Cache Fuser projects and fuses the Sharer's per-layer KV-Cache with the Receiver's, adds it back via residual connection, and a learnable per-layer gate selects which layers are injected; both LLMs stay frozen and only the fuser is trained.
  - Why listed here: Establishes cache-level fusion (with token/layer alignment across heterogeneous models) as an alternative to text-to-text communication.
