# Tag Audit

## Findings

The repository currently has no Git tag refs (`git tag` returns no entries). The names below are historical labels preserved in the repository's deployment and release records, but they are not a reliable, inspectable tag history. That absence is itself a release-management failure.

| Evidence | Problem | Team impact and rollback risk |
| --- | --- | --- |
| `v1.4.2` | A version-looking label appears in the old notes and deployment history, but no Git tag or commit is present for it. | Engineers cannot resolve the label to source code, so reproducing the reported production version or checking its fix set is guesswork. |
| `version-1.0` | The `version-` naming style omits a patch component and differs from semantic version tag syntax. | Sorting and tooling cannot treat it as a normal release; a rollback request cannot be compared reliably with complete versions such as `1.5.0`. |
| `release_2` | This generic name is recorded as an emergency rollback target, but the repository contains no tag ref or annotated explanation for it. | The incident team may roll back to an unknown or unsupported commit, exactly as described in the incident log, with no reason to trust it as a known-good build. |
| `1.5.0` | The numeric label has no `v` prefix and is only mentioned in old notes, not tied to a commit or deployment record. | Humans and release tooling must guess whether it is a release tag, a document label, or a different versioning scheme; audit reconstruction is ambiguous. |
| `v2-final-FINAL` | The name contains subjective status text and no machine-sortable prerelease identifier. | There is no precise way to tell whether it precedes, replaces, or is safer than another release, making incident rollback selection error-prone. |
| `stable-build` | A branch/build status is used as a release label in deployment history without a version or immutable commit reference. | The meaning of “stable” can change over time, so the same rollback instruction may point to different code or no code at all. |
| `latest-good` | Production was reportedly deployed from this label, but it has no semantic version, release notes, or documented commit. | “Latest” is mutable and “good” is subjective; responders cannot prove what was running or reproduce the hotfix deployment. |
| `patch-new` | This label does not identify a patch number and is not tied to a deployment record. | A patch rollback cannot be selected deterministically, and auditors cannot establish which fix was promoted. |

## Conclusion

The old records cannot answer which immutable commit was deployed. The replacement policy uses annotated `vMAJOR.MINOR.PATCH` tags and a release map that records each tag, commit, date, and deployment contents.