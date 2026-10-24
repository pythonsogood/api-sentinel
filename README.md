# ApiSentinel

> developer tool being built to detect breaking changes between OpenAPI contracts and explain their relevance to declared consumer dependencies

[![Rust](https://img.shields.io/badge/Rust-%23000000.svg?e&logo=rust&logoColor=white)](#) [![Svelte](https://img.shields.io/badge/Svelte-%23f1413d.svg?logo=svelte&logoColor=white)](#) [![OpenAPI](https://img.shields.io/badge/OpenAPI-6BA539?logo=openapiinitiative&logoColor=white)](#) [![License: CC-BY-SA](https://img.shields.io/badge/LICENSE-CC--BY--SA%204.0-blue.svg)](https://creativecommons.org/licenses/by-sa/4.0/) [![CI](https://github.com/pythonsogood/api-sentinel/actions/workflows/ci.yml/badge.svg)](https://github.com/pythonsogood/api-sentinel/actions/workflows/ci.yml)

## 🏗️ Status

**Early development.** The Rust workspace, SvelteKit frontend, and CI checks are in place. The CLI currently prints `Hello, world!`, and the core contains a starter test. Contract analysis, consumer matching, and report generation are planned work.

## ❔ Why ApiSentinel

A contract diff identifies a changed endpoint or field. ApiSentinel aims to connect that change to explicit consumer declarations while showing the limits of incomplete or stale evidence. Consumer manifests describe declared dependencies. They do not prove that a consumer will fail at runtime.

The initial release targets local OpenAPI 3.0.x contracts in YAML or JSON, explainable compatibility rules, optional consumer YAML manifests, and an offline HTML report. See the [architecture and scope](docs/ARCHITECTURE.md) for details.

## 🚀 Quick start

Install Rust through rustup, Node.js, and pnpm. Use the versions recorded in the [development prerequisites](CONTRIBUTING.md#prerequisites).

```sh
git clone https://github.com/pythonsogood/api-sentinel.git
cd api-sentinel
```

Run the Rust scaffold from the repository root:

```sh
cd app
cargo run -p apisentinel --locked
cd ..
```

Run the frontend from the repository root:

```sh
cd frontend
pnpm install --frozen-lockfile
pnpm run dev
```

Open the URL printed by Vite. The current frontend is a SvelteKit scaffold. Packaging a single HTML report that opens offline remains an implementation milestone.

## 📋 Project tracking

Tasks, priorities, dependencies, and acceptance criteria are tracked in
[YouTrack](https://apisentinel.youtrack.cloud/projects/API).

The project is available for read-only review without signing in.

## 📚 Documentation

| Document                                       | Contents                                                                                 |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------- |
| [Contributing](CONTRIBUTING.md)                | Tool versions, setup, checks, task workflow, and pull requests.                          |
| [Architecture and scope](docs/ARCHITECTURE.md) | Components, technology direction, boundaries, evidence semantics, and repository layout. |
| [Planned CLI](docs/CLI.md)                     | Intended commands, output behavior, and exit policy.                                     |
| [Roadmap](docs/ROADMAP.md)                     | Development milestones, open decisions, and evaluation goals.                            |
| [Pre-defense report](docs/Report.docx)         | Project rationale, requirements, architecture, prototype, and evaluation plan.           |
