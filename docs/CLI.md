# Planned CLI interface

**The following commands describe the intended interface and are not implemented yet.** The paths are illustrative; corresponding example files will be added in the future.

```sh
apisentinel diff old.json new.json
apisentinel check old.json new.json --format json
apisentinel impact old.json new.json --provider user-service --consumers ./consumers
apisentinel report old.json new.json --provider user-service --consumers ./consumers -o report.html
apisentinel graph --consumers ./consumers --format dot
```

### Planned exit policy

| Condition                                                                                       | Exit code |
| ----------------------------------------------------------------------------------------------- | --------- |
| `check` finds at least one assessed `Breaking` change.                                          | `1`       |
| `check` finds no `Breaking` changes, including warnings classified as `PotentiallyBreaking`.    | `0`       |
| Input, execution, or output failure; invalid supplied manifests; incomplete mandatory analysis. | `2`       |
| Successful `diff`, `impact`, `report`, or `graph` output, regardless of findings.               | `0`       |

If required analysis cannot finish, return `2`, even if breaking changes have already been found. JSON mode must keep stdout parseable; diagnostics and progress belong on stderr.

The `graph` command and interactive dependency graph are Should-level features. Contract-only analysis must work without `--consumers` and explicitly report that consumer analysis was not supplied.

For the current runnable scaffold and tool versions, see [Contributing](../CONTRIBUTING.md). For evidence semantics, see [Architecture](ARCHITECTURE.md).
