> **Status:** Active
> **Provenance:** Shane Hartley (maintainer); Claude (multiple sessions, drafting and revision 2026-05-07 to 2026-05-13)
> **Last reviewed:** 2026-05-13
> **Why this status:** Initial public release of the standard. Updates expected as conventions mature through use.

# project-scaffold

Standardized development documentation — tiered conventions and skeletons for software and research projects.

This repo holds [`development_documentation.md`](development_documentation.md), a standard defining the core set of structural documents every project should have, regardless of language or domain. The standard separates concerns across files (features, claims, decisions, architecture, attack vectors, etc.), assigns each a tier (always / strongly recommended / conditional), and prescribes stable ID conventions so commits, reviews, and AI-assisted sessions can reference specific entries unambiguously across the lifetime of a project.

The standard is designed to serve two audiences simultaneously: humans returning to a project after a gap, and tooling (AI development partners, critic tools) reading the project to act on it.

## How to use this

The fastest path: open [`PROMPTS.md`](PROMPTS.md), pick the prompt that matches your situation (new project, audit an existing repo, or revive a Dormant project), and paste it into a chat session along with `development_documentation.md`.

For more control, drop [`development_documentation.md`](development_documentation.md) into a chat session at the start of work on any project to give Claude (or any collaborator) the conventions to follow. The standard's **Creation Order** section tells you which document to write first; the **Quick Decision Guide** at the end tells you which Tier 2 and Tier 3 documents are worth adding based on the project's nature.

For specific document types, the [`skeletons/`](skeletons/) directory holds copy-paste-ready starter files — copy the relevant `*.skeleton.md`, drop the `.skeleton` segment, and fill in the placeholders.

## Documentation

- [Development Documentation Standard](development_documentation.md) — the standard itself (and the spec for this repo, per the Documentation-as-deliverable Workflow Variation)
- [Starter prompts](PROMPTS.md) — three cold-start prompts for new sessions
- [Skeletons](skeletons/) — copy-paste-ready starter files for each document type
- [Decisions](DECISIONS.md) — design decisions for this repo
- [Changelog](CHANGELOG.md) — version history
- [CLAUDE.md](CLAUDE.md) — handoff for AI-assisted contributions to this repo

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) — see [LICENSE](LICENSE).

Any code added to this repo in future (e.g. validation scripts, scaffolding tools) will be released under MIT and noted in the relevant directory.
