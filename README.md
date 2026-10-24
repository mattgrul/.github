# .github

[Default community health files][docs] for the repositories of
`mattgrul`. A file here shows on every repository of the account, public
and private, that has no copy of its own. GitHub reads the file from
here and shows it in place. Nothing is copied, so a clone of another
repository contains none of this.

[docs]: https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file

This repository must stay public. GitHub reads default files from a
public `.github` repository only.

## What inherits

| File | Inherited |
|---|---|
| `SECURITY.md` | yes |
| `CONTRIBUTING.md` | yes |
| `CODE_OF_CONDUCT.md` | yes |
| `.github/ISSUE_TEMPLATE/` | yes |
| `.github/PULL_REQUEST_TEMPLATE.md` | yes |
| `README.md` | no |
| `LICENSE` | no |
| `.github/workflows/` | no |

A repository with its own copy of a file uses that one and ignores this
one. That is the only way to opt out. A local copy stands on its own and
says everything the file here says. A repository either shows the file
here or carries a complete one of its own.

Issue templates are one set. A repository with a valid form or a
`config.yml` in its own `.github/ISSUE_TEMPLATE/` ignores every
template here, the forms and `config.yml` alike. A repository that
wants one local form carries the whole set.

`LICENSE` is never inherited. GitHub's page on default files says:
*"License files must be added to individual repositories so the file
will be included when a project is cloned, packaged, or downloaded."*
Every repository needs its own.

## The release workflow

`.github/workflows/release.yml` is a [reusable workflow][reuse]. A
repository that releases calls it from a workflow of its own, by path
and commit SHA. GitHub reads the body from here on every run. Nothing is
copied.

[reuse]: https://docs.github.com/en/actions/how-tos/sharing-automations/reusing-workflows

```yaml
# .github/workflows/release.yml, in a repository that releases
name: Release
on:
  workflow_dispatch:
    inputs:
      bump:
        type: choice
        options: [patch, minor, major]
jobs:
  release:
    uses: mattgrul/.github/.github/workflows/release.yml@COMMIT_SHA # vX.Y.Z
    # A called workflow holds no more than its caller grants, and the
    # default token is read only.
    permissions:
      contents: write
    with:
      bump: ${{ inputs.bump }}
```

Run it from the Actions tab and choose the part of the version to raise.
It reads the highest `vX.Y.Z` tag, raises that part, and drafts a
release with notes GitHub writes from the pull request titles merged
since. Review the draft on the Releases page and publish it. Publishing
creates the tag. It runs from the default branch or an `N.x` branch and
refuses any other. It commits nothing. A repository that also keeps a
version in a file bumps that file in a pull request, like any other
change.

### Releasing the version a file holds

A repository that keeps its version in a file passes that version
instead of a bump, so the tag always matches the file. Read the file
at the commit being released through the GitHub API:

```yaml
name: Release
on:
  workflow_dispatch:
jobs:
  version:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    outputs:
      version: ${{ steps.read.outputs.version }}
    steps:
      - id: read
        env:
          GH_TOKEN: ${{ github.token }}
          REPO: ${{ github.repository }}
          SHA: ${{ github.sha }}
        run: |
          set -euo pipefail
          version=$(gh api "repos/$REPO/contents/VERSION_FILE?ref=$SHA" \
            -H 'Accept: application/vnd.github.raw+json' | READ_VERSION)
          echo "version=$version" >>"$GITHUB_OUTPUT"

  release:
    needs: version
    uses: mattgrul/.github/.github/workflows/release.yml@COMMIT_SHA # vX.Y.Z
    permissions:
      contents: write
    with:
      version: ${{ needs.version.outputs.version }}
```

Replace `VERSION_FILE` with the file's path. Replace `READ_VERSION` with
a command that reads the version from standard input. The file's format
belongs to the calling repository. That job reads a version. It does
not compute one, create a release or write notes.

### Attaching assets to the draft

The workflow names no language, so it builds nothing and attaches
nothing. A repository that ships a binary adds one job of its own,
after the caller, that builds its artifacts and uploads them to the
draft. It reads the draft's tag from the caller:

```yaml
jobs:
  release:
    uses: mattgrul/.github/.github/workflows/release.yml@COMMIT_SHA # vX.Y.Z
    permissions:
      contents: write
    with:
      bump: ${{ inputs.bump }}

  artifacts:
    needs: release
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      # Build, then:
      - run: gh release upload "$TAG" <files> --repo "$REPO" --clobber
        env:
          TAG: ${{ needs.release.outputs.tag }}
          REPO: ${{ github.repository }}
          GH_TOKEN: ${{ github.token }}
```

The caller may carry an asset job and a version job, and nothing else.
Neither job may compute a version, create a release or write notes,
because those live here and move by the SHA. Uploading to a draft is
safe: the release stays unpublished until a person publishes it, and
publishing is what creates the tag.

The SHA pins the caller to one version of the body. A change here
reaches a repository only when its caller moves to the new SHA. A
`dependabot.yml` in the calling repository that watches the
`github-actions` ecosystem opens that pull request. Dependabot finds a
new version through this repository's `vX.Y.Z` tags, and reads the
caller's version from the comment after the SHA. So write the tag of
the pinned commit there, as the examples show. GitHub also accepts a
tag or a branch name after the `@`, and calls the SHA the safest of the
three.

### Releasing this workflow

This repository releases its workflows with the release workflow
itself. One tag covers every workflow and action here. Run Release from the
Actions tab here and choose the part to raise:

- major: a caller must change, such as a removed or renamed input.
- minor: a caller gains something, such as a new input.
- patch: a fix or a change to these documents.

Publish the draft as for any release. Dependabot offers the new tag to
each caller.

## The gitleaks scan

`gitleaks-scan/` is an [action][composite] that runs [gitleaks][gitleaks]
on the files of the commit, and on a pull request on the commits it
adds. A repository runs it as the one step of a job, by path and commit
SHA:

[composite]: https://docs.github.com/en/actions/tutorials/create-actions/create-a-composite-action
[gitleaks]: https://github.com/gitleaks/gitleaks

```yaml
# .github/workflows/gitleaks-scan.yml, in a repository that scans
name: gitleaks-scan
on:
  pull_request:
  push:
    branches: [main, "*.x"]
permissions:
  contents: read
jobs:
  gitleaks-scan:
    runs-on: ubuntu-24.04
    steps:
      - uses: mattgrul/.github/gitleaks-scan@COMMIT_SHA # vX.Y.Z
```

The action checks the repository out itself, so the job needs no other
step. GitHub names the check after the job. The caller above reports
`gitleaks-scan`, and that is the name a ruleset requires.

The rules live here, in `gitleaks-scan/gitleaks.toml`: gitleaks' own
rules for keys and tokens, and two for personal data, email addresses
and home folder paths. A repository with a `.gitleaks.toml` of its own
uses that file instead, and none of the shared rules. For one known
finding, a `gitleaks:allow` comment on its line, or an entry in a
`.gitleaksignore`, keeps the shared rules.

gitleaks runs from its own image, pinned by digest in
`gitleaks-scan/Dockerfile`. Dependabot moves that pin here, and the
pins of the actions the scan uses. A release carries them to each
caller, and the caller's pin moves as it does for the release workflow:
a Dependabot pull request in the calling repository.

`.github/workflows/test-gitleaks-scan.yml` runs the action on this
repository, then `gitleaks-scan/test` shows what the rules catch and
what they pass.
