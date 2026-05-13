> **Status:** Active
> **Provenance:** Shane Hartley (maintainer); Claude (multiple sessions, drafting and revision 2026-05-07 to 2026-05-13)
> **Last reviewed:** 2026-05-13
> **Why this status:** Initial public release of the standard. Updates expected as conventions mature through use.

# project-scaffold

Standardized development documentation — tiered conventions and skeletons for software and research projects.

This repo holds [`development_documentation.md`](development_documentation.md), a standard defining the core set of structural documents every project should have, regardless of language or domain. The standard separates concerns across files (features, claims, decisions, architecture, attack vectors, etc.), assigns each a tier (always / strongly recommended / conditional), and prescribes stable ID conventions so commits, reviews, and AI-assisted sessions can reference specific entries unambiguously across the lifetime of a project.

The standard is designed to serve two audiences simultaneously: humans returning to a project after a gap, and tooling (AI development partners, critic tools) reading the project to act on it.

## How to use this

Drop [`development_documentation.md`](development_documentation.md) into a chat session at the start of work on any project. It gives Claude (or any collaborator) the conventions to follow when creating or updating project documentation.

For a new project, the standard's **Creation Order** section tells you which document to write first; the **Quick Decision Guide** at the end tells you which Tier 2 and Tier 3 documents are worth adding based on the project's nature.

## Documentation

- [Development Documentation Standard](development_documentation.md) — the standard itself
- [Decisions](DECISIONS.md) — design decisions for this repo
- [Changelog](CHANGELOG.md) — version history

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) — see [LICENSE](LICENSE).

Any code added to this repo in future (e.g. validation scripts, scaffolding tools) will be released under MIT and noted in the relevant directory.
