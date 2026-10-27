# Reports Module Instructions

These instructions apply to `reports/` and its descendants, together with the
repository-wide rules in the root `AGENTS.md`.

## Organization

- Keep one directory per report directly under `reports/`. Use descriptive
  English directory names, including coverage years when they define its scope.
- Use each report's `REPORT.md` as the report body. Add `evidence/` for supporting
  material when needed. Reserve `README.md` for navigation when needed.
- Keep preliminary research-background notes and personal advice outside the
  repository; do not include them as `context.md` or reproduce them elsewhere.
- Maintain the report list in `reports/README.md`. Do not create empty
  directories for planned reports.

## Content and Privacy

- Preserve existing content languages, source dates, scope limitations, and
  distinctions between evidence and interpretation.
- Keep report files focused on their research content. Do not add migration
  logs, import-status fields, or metadata naming private source collections.
- Do not include machine-specific paths, local account names, cloud-sync
  locations, or private source-folder names in report content or metadata.
  Retain public bibliographic sources and source URLs.
- Do not infer writing dates from folder names or present unverified claims
  as verified. Substantive revisions should be grounded in relevant sources.
- Briefly explain unfamiliar technical routes at their first substantive use:
  identify the object, action, and purpose. Reuse established terms later;
  avoid repeated definitions or lengthy explanations in every table cell.
- Name concrete research objects and evaluated workloads for every domain,
  including within mixed-domain technique tables. For learning workloads,
  identify the supported model family, task, and training/inference stage;
  for other systems, identify the component or managed state. Do not stop at
  generic labels such as AI, model, system, or workflow when evidence supports
  a more precise description. Distinguish an optimization tool from its target,
  and general applicability from the workloads actually evaluated. Do not infer
  a model family or scale from an absent label; mark unconfirmed scope explicitly.
- Keep PDFs, exported reports, downloaded full text, caches, and temporary
  extraction artifacts outside tracked report content.

## Evidence and Cross-Module Links

- Treat venue catalogs under a report's `evidence/` as scoped evidence
  snapshots. They are not canonical paper notes or maintained literature indexes.
- Keep canonical paper notes and maintained literature indexes in `paper-vault/`;
  keep reusable technical concepts in `knowledge/`. Follow those modules'
  instructions when creating or changing their content.
- Use relative Markdown links for navigation within a report. Use root-relative
  Obsidian paths for cross-module note links, and only link existing notes.
- Link paper citations in report prose to their corresponding evidence entries
  when available. Use stable entry anchors and retain the public paper URLs in
  the evidence catalogs.
- Check local link targets after moving content. Retain original source URLs;
  do not replace them with machine-specific paths.
