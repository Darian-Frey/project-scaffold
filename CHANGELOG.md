# Changelog

All notable changes to this project will be documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
This project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- `skeletons/` directory with eight copy-paste-ready starter files (`README`, `FEATURES`, `CLAIMS`, `DECISIONS`, `ATTACK_VECTORS`, `ROADMAP`, `CLAUDE`, `CHANGELOG`) plus a directory `README.md` explaining the copy-rename-fill workflow and tier mapping.
- `PROMPTS.md` with three narrow cold-start prompts: bootstrap a new project, audit an existing repo, revive a Dormant project.
- `CLAUDE.md` for this repo, adapted per the Documentation-as-deliverable Workflow Variation. Documents the repo's invariants, conventions, pitfalls (notably skeleton drift), and out-of-scope items.
- `.gitignore` covering `SELF_AUDIT.md`, `audit-*.md`, editor cruft, and pre-emptive Python entries for future scaffolding scripts.
- `D-002` recording the skeletons-vs-usage-guide decision.
- `D-003` recording the choice of three narrow prompts in `PROMPTS.md` over an exhaustive prompts file.
- `D-004` recording the five-edit package of standard revisions following the first self-audit.
- `D-005` recording the Tier 1 exemption for `FEATURES.md` (this repo's deliverable is a standard, not a tool with capabilities).
- `D-006` recording the Tier 1 exemption for `ROADMAP.md` (the standard is revised inline, not in phases).
- Documentation-as-deliverable Workflow Variation in the standard, covering the meta-level case where the project's deliverable is documentation itself. Spells out which Tier 1 documents adapt and which are legitimate exemptions.
- Recursive-application paragraph in the standard's Evolution section, explicitly stating that the host repo follows the standard with documented exemptions.
- Project-specific-extensions clause in the Evolution section, listing reserved names and the conditions under which projects may add document types beyond those the standard names.

### Changed
- **Tier 1 framing reconciled with the cost note.** Header changed from "Tier 1 — Always (every project, no exceptions)" to "Tier 1 — Default minimum (every project, with narrow documented exemptions)." Body text now requires Tier 1 omissions to be recorded as `DECISIONS.md` entries with reasoning. The cost note section was extended to explicitly cover Tier 1 with the same friction test plus the documented-exemption requirement. Fixes the internal contradiction identified by the first self-audit (2026-05-13).
- ATTACK_VECTORS Maintenance Rule 4 softened from "Detection is not optional" to "Detection is defined, not necessarily automated." Manual / structural review is now explicitly named as a valid detection method, matching the spec's existing examples. Documentation-style projects benefit most; the rule's intent (no undefined detection) is preserved.
- Standard's Provenance log appended with the 2026-05-13 revision entry; Last reviewed refreshed to 2026-05-13.

## [0.1.0] — 2026-05-13

### Added
- Initial release of the development documentation standard (`development_documentation.md`).
- Tier 1 (always), Tier 2 (strongly recommended), and Tier 3 (conditional) document classifications.
- Stable ID conventions: `F-NNN` (features), `C-NNN` (claims), `D-NNN` (decisions), `AV-NNN` (attack vectors).
- README status header standard with five-value status vocabulary (Active / Dormant / Complete / Archived / Superseded).
- Project lifecycle transition procedures.
- Integration patterns for critic tools and AI development partners.
- Repo scaffolding: `README.md`, `LICENSE` (CC BY 4.0), `CHANGELOG.md`, `DECISIONS.md`.
- `D-001` recording the chosen standard format (tier system, stable IDs, lifecycle vocabulary).
