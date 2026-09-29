# Versioning Convention

## Semantic versioning

Production releases use `MAJOR.MINOR.PATCH`:

- **MAJOR** increases for an incompatible or breaking change. Example: `v1.4.2 -> v2.0.0`.
- **MINOR** increases for backwards-compatible functionality. Example: `v1.0.0 -> v1.1.0`.
- **PATCH** increases for backwards-compatible fixes or small corrections. Example: `v1.1.0 -> v1.1.1`.

When MAJOR increases, MINOR and PATCH reset to zero. When MINOR increases, PATCH resets to zero.

## Tag format

The exact production tag format is `vMAJOR.MINOR.PATCH`, for example `v1.1.1`. Every release tag must point to the commit that was built and deployed.

## Annotated release tags

The team uses annotated tags for releases because they store the tagger, date, release message, and target commit in Git. Create one with:

```sh
git tag -a v1.1.0 -m "Release 1.1.0: add checkout service"
```

Lightweight tags are not used for production releases because they do not carry the release metadata needed for audit and incident response.

## Pre-releases

Release candidates and betas use a prerelease suffix such as `v1.5.0-rc.1` or `v1.5.0-beta.1`. Prereleases sort before the corresponding final release: `v1.5.0-rc.1 < v1.5.0`. A final `v1.5.0` is created only after validation and promotion.