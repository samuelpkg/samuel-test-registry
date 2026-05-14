# samuel-test-registry

> **Internal use only — do not depend on these plugins.**
>
> This registry exists solely to back Samuel's `e2e/live/` nightly test
> tier. Plugins listed here are unsigned, intentionally tiny, and may
> be reshaped without notice when test scenarios change. If you are
> looking for the real plugin registry, see
> [`samuelpkg/samuel-registry`](https://github.com/samuelpkg/samuel-registry).

## What this is

`index.toml` points at five fixture plugin repos under `samuelpkg/`:

| Fixture                        | Tag scheme       | Coverage                                                       |
| ------------------------------ | ---------------- | -------------------------------------------------------------- |
| `samuel-test-skill-basic`      | `v1.0.0`         | Happy path — install + manifest + lockfile                     |
| `samuel-test-skill-tagged-v`   | `v1.0.0`         | rc.6: registry says `1.0.0`, repo tags `v1.0.0`                |
| `samuel-test-skill-tagged-bare`| `1.0.0`          | rc.6 fallback: registry says `1.0.0`, repo tags bare `1.0.0`   |
| `samuel-test-skill-with-git`   | `v1.0.0`         | rc.9: ensure `.git/` is stripped on install                    |
| `samuel-test-skill-updatable`  | `v1.0.0`, `v1.1.0` | Update path: 1.0.0 → 1.1.0                                  |

## How it is consumed

Samuel's live e2e tier points its `[[registries]]` block at this repo
and runs the install/update/search/doctor/uninstall flows against the
fixtures above. The schema and publish flow are maintained in-tree at
[`samuel-test-registry/`](https://github.com/samuelpkg/samuel/tree/main/samuel-test-registry)
in the framework repo.

If you are working on Samuel and need to extend the fixture matrix,
edit the source-of-truth tree there — not this repo directly. The
framework repo's PR review keeps the schema in step with the parser.
