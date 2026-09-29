# Release Map

This map ties each verified release tag to the immutable commit used for the deployment record. Dates are the commit dates in Git history.

| Version (tag) | Commit (short hash) | Date | What Shipped |
| --- | --- | --- | --- |
| `v1.0.0` | `ff1fb9a` | 2026-06-06 | Deployment record: initial complete checkout-service exercise scaffold, including the service placeholder and release documentation baseline. |
| `v1.1.0` | `c17d4c4` | 2026-06-06 | Deployment record: first checkout-service implementation with the `checkout-service` name and version output. |
| `v1.1.1` | `82535d9` | 2026-06-06 | Deployment record: patch revision that standardizes startup output and records the placeholder service version as `0.0.0-placeholder`. |

## Traceable rollback

Use the sortable release history to identify the newest known release, then inspect the map and release notes for its previous known-good version:

```sh
git tag --sort=-v:refname        # the sortable release history
git show --summary v1.1.1        # inspect the current release commit and annotation
git checkout v1.1.0              # roll back to the last known-good tag, then redeploy
```

Because every release tag uses the same sortable format and points to an annotated immutable commit, the rollback target is an exact source snapshot rather than a mutable label. The map and release notes also explain what was deployed and why `v1.1.0` is the previous known-good target; the original names such as `latest-good` and `release_2` provided neither guarantee.