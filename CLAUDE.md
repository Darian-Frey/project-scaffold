# CLAUDE.md

## Project

`project-scaffold` is the home of the Development Documentation Standard — a single normative document (`development_documentation.md`) defining the structural docs every project should carry, plus supporting material that helps users adopt it. Status: Active, first public release.

Per the standard's Documentation-as-deliverable Workflow Variation, the repo deliverable is documentation itself; there is no code, build, or test infrastructure.

## Current state

- `development_documentation.md` — the standard. Active and load-bearing. Edit only as a material revision; refresh its Provenance log inline and update its Last reviewed date.
- `README.md` — front door. Status header tracks repo state.
- `DECISIONS.md` — repo's own design log. Three entries (D-001 standard format, D-002 skeletons directory, D-003 PROMPTS.md).
- `CHANGELOG.md` — Keep a Changelog format, version 0.1.0.
- `PROMPTS.md` — three cold-start prompts for users adopting the standard.
- `skeletons/` — eight starter files plus directory README. The skeleton files mirror the **Minimal File Skeletons** section of the standard and must stay in sync with it.
- `LICENSE` — CC BY 4.0. Any future code (validation scripts, scaffolding tools) will be MIT and noted in its own directory.

## Active task

No active task at present. The next likely work item is one of:

- Acting on findings from a self-audit run (the audit prompt in `PROMPTS.md` applied to this repo).
- A material revision to the standard, triggered by drift caught during use or by a follow-up audit.
- A user-reported friction in adoption.

When working, reference any feature-equivalent IDs (D-NNN for decisions; the standard's own document types) explicitly. Acceptance criteria for any edit: the standard remains internally consistent (no contradictions between sections); the host repo follows the standard (with documented exemptions where it doesn't); cross-references between docs remain accurate.

## Invariants

These must not be violated:

- **Append-only IDs.** D-NNN entries in `DECISIONS.md` are never deleted or renumbered. Withdrawn entries get a status flag.
- **Status vocabulary fidelity.** The standard's status vocabularies (project / decision / claim) are fixed; do not introduce new values without a corresponding D-NNN.
- **Skeletons mirror the standard.** When the **Minimal File Skeletons** section of `development_documentation.md` changes, the corresponding `skeletons/*.skeleton.md` file must be updated to match in the same commit.
- **Self-application.** The repo follows its own standard; legitimate Tier 1 exemptions (currently `FEATURES.md`, `ROADMAP.md`) are recorded in `DECISIONS.md` and revisited if friction signals fire.
- **Provenance log discipline.** Material revisions to `development_documentation.md` append an entry to its Provenance line and refresh its Last reviewed date.
- **Cross-references may be stale.** No tooling enforces bidirectional cross-references (per the standard's Maintenance Rule 6). Authors are responsible for keeping them current; when in doubt, search.

## Build & test

No build or test commands. This is a documentation-only repo.

Reasonable manual checks before committing a material edit:

```bash
# Render markdown locally if helpful
grip README.md      # or any other markdown viewer

# Search for references to renamed or moved sections
grep -rn "section name" .

# Confirm DECISIONS IDs remain sequential and unique
grep -n "^### D-" DECISIONS.md
```

## Conventions

- **Markdown style.** Prose paragraphs over bullet lists for explanation; bullets for enumerable items. Code fences for shell commands and skeleton excerpts. ATX-style headers (`#`, `##`, `###`).
- **DECISIONS entries** follow the format in the standard's §Per-Document Specifications → `DECISIONS.md`. Every entry must include reversal conditions; an entry without one is a belief, not a decision.
- **CHANGELOG entries** reference D-NNN IDs for traceability.
- **Commit messages.** Imperative mood, short summary line, followed by a paragraph if the change is non-trivial. Reference D-NNN in the body when applicable.
- **Dates** in ISO 8601 (YYYY-MM-DD).
- **Cross-references** within the repo use relative markdown links (e.g. `[Decisions](DECISIONS.md)`).

## Pitfalls

- The standard's `ATTACK_VECTORS.md` section is the canonical list of failure modes for projects using the standard. This repo does not have its own `ATTACK_VECTORS.md` yet (no drift incidents to date), but the standard's known failure modes apply meta-recursively to this repo too: skeleton drift, Provenance log staleness, status vocabulary drift, cross-reference rot.
- **Skeleton drift** is the most likely real failure mode. When editing the **Minimal File Skeletons** section of the standard, the matching `skeletons/*.skeleton.md` file in the directory must be updated in the same commit. Forgetting this produces silent divergence.
- **Retroactive CHANGELOG modification.** The standard treats version history as append-only. Once a release is tagged (v0.1.0 etc.), do not modify its CHANGELOG entry. Add new entries under `[Unreleased]` or the next version, not the released one.
- **The standard prescribes tooling it does not provide.** Maintenance Rule 6 names a cross-reference checker as illustrative, not as part of this repo's deliverables. Do not silently add such tooling here without a D-NNN entry deciding where the reference implementation belongs.

## Out of scope

The AI partner should not change these without asking:

- The choice of license (CC BY 4.0 for documentation; future MIT for code).
- The repo's overall organisation (root-level docs + `skeletons/` directory). Reorganisations are D-NNN decisions.
- The standard's stable IDs and append-only conventions — these are load-bearing for backward compatibility.
- The reserved document names listed in the standard's project-specific-extensions clause.
- This `CLAUDE.md` file's structure — refresh its content, but don't reorder its sections without a D-NNN entry.
