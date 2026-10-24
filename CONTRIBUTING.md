# Contributing to ApiSentinel

This guide describes the current development setup and the workflow for proposing changes. For product scope and component responsibilities, see [Architecture](docs/ARCHITECTURE.md).

## Development setup

### Prerequisites

The current repository and CI configuration use:

| Tool    | Version                                                                        |
| ------- | ------------------------------------------------------------------------------ |
| Rust    | `1.99.0`, pinned in [app/rust-toolchain.toml](app/rust-toolchain.toml).        |
| Node.js | `26.8.1`, recorded in [frontend/.node-version](frontend/.node-version) and CI. |
| pnpm    | `12.14.0`, selected in CI.                                                     |

Install [Git](https://git-scm.com/downloads), [Rust](https://rustup.rs/), [Node.js](https://nodejs.org/en/download), and [pnpm](https://pnpm.io/installation).
When changing tool versions, update the corresponding repository and CI configuration together.

The following commands work in PowerShell and common Unix shells. Each section states its starting directory.

### Clone the repository

```sh
git clone https://github.com/pythonsogood/api-sentinel.git
cd api-sentinel
```

### Build and run the Rust scaffold

From the repository root:

```sh
cd app
rustup show
cargo build --workspace --locked
cargo run -p apisentinel --locked
```

The current CLI prints `Hello, world!`. Run Rust workspace commands from `app/` so the local toolchain selection applies.

Return to the repository root:

```sh
cd ..
```

### Run the frontend

From the repository root:

```sh
cd frontend
pnpm install --frozen-lockfile
pnpm run dev
```

Open the local URL printed by Vite. Stop the development server before running the checks below in the same terminal.

For type checking and a production build, run inside `frontend/`:

```sh
pnpm run check
pnpm run build
```

To preview the current frontend build locally:

```sh
pnpm run preview
```

Development and preview servers are tooling for contributors. Successful preview does not verify the planned standalone HTML report requirement.

## Checks and continuous integration

From the repository root, run Rust checks:

```sh
cd app
cargo fmt --all -- --check
cargo clippy --workspace --all-targets --locked -- -D warnings
cargo test --workspace --locked
cd ..
```

Then run frontend checks:

```sh
cd frontend
pnpm install --frozen-lockfile
pnpm run check
pnpm run build
cd ..
```

The [CI workflow](.github/workflows/ci.yml) runs these checks for pushes to `main` and pull requests targeting `main`. A passing scaffold build does not establish rule correctness, consumer evidence accuracy, or offline report behavior; those checks will be added with the relevant implementations.

Commit `app/Cargo.lock` and `frontend/pnpm-lock.yaml`. When intentionally changing dependencies, regenerate the appropriate lockfile locally and include it in the same change.

## Working on a task

Use a feature branch and reference the actual YouTrack issue key in the branch, commit, and pull request. For example:

```sh
git checkout main
git pull --ff-only
git checkout -b feature/API-14-core-workspace
```

`API-14` is an illustrative issue key; replace it with the key assigned in your YouTrack project.

Use the pull request template to describe resulting behavior, verification, and satisfied acceptance criteria. Add relevant checks for implemented behavior and update documentation when public contracts or supported scope change. Mark work complete when its acceptance criteria are met and the evidence is linked.

## Pull request checklist

Use the [pull request template](.github/pull_request_template.md) and include:

- The related YouTrack issue key and the resulting behavior.
- Applicable task acceptance criteria and evidence that they are satisfied.
- Relevant automated checks and their results.
- Documentation or example updates when public behavior changes.
- Known limitations.

Add tests for the behavior you change. For compatibility rules, include examples that should trigger the rule and examples that should not. Replace scaffold tests with relevant behavior checks as those features are implemented. Keep fixture inputs and expected outcomes traceable.

## Documentation updates

Keep the README focused on an introduction and a working quick start. Put contributor instructions here, component and scope details in [Architecture](docs/ARCHITECTURE.md), intended command behavior in [CLI](docs/CLI.md), and milestones in [Roadmap](docs/ROADMAP.md).
