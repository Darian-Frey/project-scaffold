# Skeletons

Copy-paste-ready starter files for the document types defined in [`../development_documentation.md`](../development_documentation.md).

## How to use

For each document you want to create in a new project:

1. Copy the relevant `*.skeleton.md` file to your project root.
2. Rename it to drop the `.skeleton` segment (e.g. `FEATURES.skeleton.md` → `FEATURES.md`).
3. Fill in the `{placeholder}` values.
4. Delete the HTML comment block at the top once you've consulted it.

For example, to scaffold a new project's Tier 1 documents:

```bash
cp skeletons/README.skeleton.md      myproject/README.md
cp skeletons/FEATURES.skeleton.md    myproject/FEATURES.md
cp skeletons/ROADMAP.skeleton.md     myproject/ROADMAP.md
cp skeletons/CHANGELOG.skeleton.md   myproject/CHANGELOG.md
cp skeletons/CLAUDE.skeleton.md      myproject/CLAUDE.md
```

Then add Tier 2 and Tier 3 skeletons as the project warrants — see the **Quick Decision Guide** at the end of `development_documentation.md`.

## What's here

| Skeleton | Tier | When to use |
|----------|------|-------------|
| `README.skeleton.md` | 1 | Every project. |
| `FEATURES.skeleton.md` | 1 | Every project. |
| `ROADMAP.skeleton.md` | 1 | Every project. |
| `CLAUDE.skeleton.md` | 1 | Every project using AI-assisted development. |
| `CHANGELOG.skeleton.md` | 1 | Every project. |
| `DECISIONS.skeleton.md` | 2 | Most non-trivial projects — add from day one if you expect more than one or two significant design choices. |
| `BUGS.skeleton.md` | 2 | Projects that want bug history in-repo rather than (or alongside) an external tracker. Especially valuable for solo-dev and AI-partner workflows. |
| `IMPROVEMENTS.skeleton.md` | 2 | Projects that want a tracked list of candidate refactors and code-quality improvements distinct from features and decisions. Pairs with `BUGS.md` under Maintenance Rule 8. |
| `CLAIMS.skeleton.md` | 3 | Research projects making empirical, theoretical, or mathematical assertions. |
| `ATTACK_VECTORS.skeleton.md` | 3 | Projects with well-defined failure modes worth enumerating. |

Skeletons for `ARCHITECTURE.md`, `SPEC.md`, `BUILD.md`, and Tier 3 docs not listed above are not included because their content is too project-specific to template usefully — start from a blank file referring to the specification in `development_documentation.md` for those.
