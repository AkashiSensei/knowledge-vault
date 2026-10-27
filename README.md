# knowledge-vault

A personal knowledge vault for research, engineering, and technical learning.
Open the repository root as one Obsidian vault so notes across modules can link
to each other.

Repository content is written in English by default unless the user or an
explicit workflow configuration specifies another language.

## Current Contents

- [Paper vault](paper-vault/README.md): canonical paper notes, literature
  indexes, discovery records, and recurring intake configuration.
- [Research reports](reports/README.md): research surveys and direction analyses,
  starting with the [2024–2026 systems landscape](reports/systems-landscape-2024-2026/REPORT.md).
- AI infrastructure knowledge: [training concepts](knowledge/ai-infra/training.md),
  [inference concepts](knowledge/ai-infra/inference.md), and
  [parallelism and state sharding](knowledge/ai-infra/parallelism.md).
- [CUDA knowledge](knowledge/cuda/README.md): execution, memory and data movement,
  instructions, and performance analysis, with question-wall provenance.
- [Distributed systems knowledge](knowledge/distributed-systems/README.md):
  shared concepts and system-specific notes, starting with [Ceph](knowledge/distributed-systems/ceph/README.md).
- [Interview preparation](interview-prep/README.md): concise Chinese questions
  and answers organized by technical direction.
- [Shared skills](skills/README.md): AI-assisted workflows for maintaining the
  knowledge base.

## Paper Workflows

Run paper workflows from the Git repository root. Their content lives under
`paper-vault/`; shared skills remain under `skills/`.

Create the ignored personal intake configuration with:

```sh
cp paper-vault/paper-intake-config-example.md paper-vault/paper-intake-config.md
```

For one intake cycle:

```text
Use $paper-intake with paper-vault/paper-intake-config.md to run one intake
cycle in this repository. Leave all generated files unstaged and uncommitted.
```

See the [paper module guide](paper-vault/README.md) for workflow details.
