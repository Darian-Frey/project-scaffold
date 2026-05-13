<!--
README.skeleton.md — copy to README.md and fill in placeholders.
See: development_documentation.md §Per-Document Specifications → README.md
Required sections (in order): status header, one-paragraph description, quick start,
build requirements, project structure, documentation map, license.
-->

> **Status:** Active
> **Provenance:** {your name} (initial commit, YYYY-MM-DD)
> **Last reviewed:** YYYY-MM-DD
> **Why this status:** Initial scaffolding.

# {Project Name}

{One-paragraph description: what the project is, who it's for, what makes it distinctive. This is the vision / BRD equivalent — keep it to a single paragraph; detailed content belongs in the linked documents below.}

## Quick Start

```bash
{exact commands — shortest path from clone to running output}
```

## Build requirements

- {Toolchain (compiler, runtime, version)}
- {OS targets}
- {Key dependencies with versions}

See [BUILD.md](BUILD.md) for detailed setup instructions.

## Project structure

```
{project-name}/
├── src/         {brief description}
├── tests/       {brief description}
├── docs/        {brief description}
└── ...
```

## Documentation

- [Features](FEATURES.md) — capabilities and acceptance criteria
- [Claims](CLAIMS.md) — research assertions and falsification conditions  <!-- research projects only -->
- [Architecture](ARCHITECTURE.md) — structure, modules, invariants
- [Decisions](DECISIONS.md) — design decisions with rationale
- [Attack Vectors](ATTACK_VECTORS.md) — project-specific failure modes  <!-- when applicable -->
- [Roadmap](ROADMAP.md) — phased plan and milestones
- [Build instructions](BUILD.md) — environment setup and build commands
- [Changelog](CHANGELOG.md) — version history

## License

{License name} — see [LICENSE](LICENSE).
