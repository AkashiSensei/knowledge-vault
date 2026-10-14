# LongBench

## 2026-05

- [[paper-vault/papers/wang2025jenga]]
  - Title: JENGA: Enhancing LLM Long-Context Fine-tuning with Contextual Token Sparsity
  - Use in paper: Downstream long-context benchmark after LongAlign-10k instruction tuning.
  - Why listed here: Checks whether JENGA's training savings preserve quality across long-text tasks rather than only improving system metrics.

## 2026-09

- [[paper-vault/papers/fu2025c2c]]
  - Title: Cache-to-Cache: Direct Semantic Communication Between Large Language Models
  - Use in paper: Sequence-length scaling study (LongBenchV1/LongBench-E), training and testing fusers on disjoint splits across input-length intervals.
  - Why listed here: Shows C2C keeps its accuracy advantage over text-to-text communication as input length grows from 0-4k to 8k+.
