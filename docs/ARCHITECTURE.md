# Architecture and scope

This document describes the intended product architecture. The current implementation is a scaffold; implemented features and development instructions are summarized in the [README](../README.md) and [Contributing guide](../CONTRIBUTING.md).

## Purpose

An API specification comparison can identify a changed endpoint or field. Developers also need to understand which consumers declare a dependency on that element and how much confidence the available evidence supports.

For example, removing a previously required `email` property from a response removes a contract guarantee. A consumer manifest that explicitly records `/email` can establish a declaration match. An endpoint-only declaration provides less specific evidence, while an incomplete manifest with no matching field cannot establish that the consumer is unaffected.

ApiSentinel will keep contract compatibility and consumer evidence separate. A dependency match describes declared exposure; **it does not establish an observed runtime failure**.

### Intended users

- API maintainers and backend developers reviewing contract evolution.
- Consumer developers investigating changes relevant to their integrations.
- QA and platform engineers adding compatibility checks to CI/CD.
- Reviewers inspecting a portable analysis report.

## Planned capabilities and scope

The initial release targets:

- Two local OpenAPI **3.0.x** contracts in YAML or JSON.
- Structural comparison of operations, parameters, and supported nested schemas.
- A documented, direction-sensitive compatibility rule set covering supported requiredness, type, enum, array, and nullability changes.
- Document-local JSON Pointer references with cycle handling and explicit diagnostics.
- Optional consumer declarations with provider identity, dependency scope, coverage, and available freshness information.
- Explainable change records shared by terminal, versioned JSON, and HTML outputs.
- A standalone HTML snapshot with embedded data and assets, intended to open directly without a server or network access.
- Change exploration and declared dependency graph inspection as Should-level features.

The exact supported feature catalogue, manifest schema, and JSON report contract must be finalized before their dependent implementations are accepted.

OpenAPI 3.1+, external or remote references, GraphQL, gRPC, asynchronous contracts, automatic dependency discovery, executed consumer contract tests, hosted accounts, and a database are outside the initial scope. AI classification and automatic contract repair are also outside that scope.

Unsupported mandatory semantics must remain visible through diagnostics and an incomplete assessment. They must not silently produce a successful compatibility verdict.

## Architecture

| Component                 | Responsibility                                                                                                                               |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `apisentinel-core`        | Load and normalize contracts, resolve supported references, detect changes, apply compatibility rules, and match optional consumer evidence. |
| `apisentinel` CLI         | Parse arguments, orchestrate analysis, apply exit policy, and deliver output.                                                                |
| Versioned analysis report | Shared result format with an explicit schema version, used by terminal, JSON, and HTML outputs.                                              |
| Frontend viewer           | Display precomputed report data and support review interactions.                                                                             |
| HTML export               | Package report data and prebuilt frontend assets into a portable artifact.                                                                   |

The core must build and test independently of frontend assets. Consumer analysis is optional: contract-only analysis must still produce results. Consumer matching enriches evidence without changing contract classifications.

The browser viewer is intended to present completed analysis. Rust remains responsible for compatibility decisions and dependency matching. Node.js and frontend build tools are development dependencies; the planned released CLI must run without them on the recipient's machine.

### Technology stack

- **Rust** for the CLI and independent analysis core.
- **Svelte 5 and TypeScript** for report interactions, with **Vite** as the build tool.
- **pnpm** for frontend dependency management.

## Repository layout

| Path                           | Contents                                        |
| ------------------------------ | ----------------------------------------------- |
| `app/crates/apisentinel-core/` | Analysis library.                               |
| `app/crates/apisentinel-cli/`  | CLI package, named `apisentinel`.               |
| `frontend/`                    | SvelteKit viewer scaffold and frontend tooling. |
| `docs/`                        | Project documentation.                          |

See [Roadmap](ROADMAP.md) for decisions still to be finalized and [CLI](CLI.md) for the command and failure policy.
