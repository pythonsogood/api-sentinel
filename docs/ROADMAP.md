# Roadmap and evaluation

The following milestones describe planned development. Current implementation status is summarized in the [README](../README.md). Acceptance criteria and dependencies belong to the corresponding YouTrack tasks.

## Development milestones

1. Finalize supported semantics, consumer declarations, report contracts, and configurable limits.
2. Implement parsing, normalization, local reference handling, structural diff, and initial CLI behavior.
3. Implement compatibility rules, explanations, canonical JSON, and command exit policy.
4. Implement consumer evidence matching, coverage/freshness handling, and optional dependency relationships.
5. Build the local report viewer and single-file HTML export.
6. Complete technical evaluation, release packaging, and usage documentation.

## Decisions to finalize

- The exact supported OpenAPI feature catalogue and direction-sensitive rule set.
- The versioned consumer manifest schema, identity rules, coverage, and freshness policy.
- The versioned JSON report schema, stable identifiers, canonical ordering, and compatibility behavior.
- The offline asset packaging approach and optional graph implementation.
- Configurable input limits, counting conventions, and override syntax.
- The final visual style and which optional features to include in the first release.

The current frontend uses SvelteKit. The planned product requires an HTML snapshot. Validate the selected packaging approach against that requirement before treating the viewer as complete.

## Evaluation goals

Evaluation will include rule fixtures, CLI integration checks, deterministic outputs, safe HTML rendering, offline browser checks, independent correctness labels, a pinned `oasdiff` comparison, and measured runtime and memory costs. A participant usability study and secondary `openapi-diff` comparison are optional.

## Completion criteria

All Must requirements and supported rule expectations must pass, with no open critical defect. Critical defects include missed required breaking rules, unsupported safe verdicts, injected execution, loss of an existing output during failed export, and CI success after mandatory analysis failure.

Record each Should-level requirement as achieved, partial, or deferred with rationale. Link implementation changes, relevant checks, expected/actual outcomes, and retained evidence before closing a task.
