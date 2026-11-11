# .github

[Default community health files][docs] for the repositories of
`mattgrul`. A file here shows on every repository of the account, public
and private, that has no copy of its own. GitHub reads the file from
here and shows it in place. Nothing is copied, so a clone of another
repository contains none of this.

[docs]: https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file

This repository must stay public. GitHub reads default files from a
public `.github` repository only.

## Inherited files

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
| `gitleaks-scan/` | no |

No other file here is inherited.

### Opting out

A repository with its own copy of a file uses that one and ignores this
one. That is the only way to opt out. A local copy stands on its own and
says everything the file here says. A repository either shows the file
here or carries a complete one of its own.

Issue templates are one set. A repository with a valid template or a
`config.yml` in its own `.github/ISSUE_TEMPLATE/` ignores every
template here, the forms and `config.yml` alike. A repository that
wants one local form carries the whole set.

### The license

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
refuses any other. On `1.x` it reads the highest `v1.Y.Z` tag instead.
There it refuses a major release, and it refuses to run at all until
the branch has a `v1.Y.Z` tag. It refuses a version that already has a
release, a draft too. It commits nothing.

A caller may add two jobs of its own: one that reads its version from a
file, and one that attaches its artifacts. The next two sections show
each. Neither job may compute a version, create a release or write
notes, because those live here and move by the SHA.

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
belongs to the calling repository. A change to the version goes into
the file in a pull request, like any other change.

The workflow refuses a version that is not above the highest tag it
reads, so raise the version in the file before you run it. On an `N.x`
branch, the version must also start with `N.`.

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

Uploading to a draft is safe: the release stays unpublished until a
person publishes it, and publishing is what creates the tag.

## The gitleaks scan

`gitleaks-scan/` is an [action][composite] that runs [gitleaks][gitleaks]
on the files of the commit, and on a pull request on the commits it
adds and their messages. A repository runs it as the one step of a job,
by path and commit SHA:

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
    runs-on: ubuntu-latest
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
`.gitleaksignore`, keeps the shared rules. An entry names a finding in
a file as `path:rule:line`. It names a finding in a commit message as
`commit:rule:line`, with the full SHA of the commit.

gitleaks runs from its own image, pinned by digest in
`gitleaks-scan/Dockerfile`.

Two workflows prove the scan here. `.github/workflows/gitleaks-scan.yml`
runs the action on this repository, as a caller does, but from the
checkout and not from a release.
`.github/workflows/checks.yml` runs `gitleaks-scan/test`,
which shows what the rules catch and what they pass.

## Pins and updates

A caller pins the release workflow and the scan by commit SHA, so it
runs one version of each. A change here reaches a repository only when
its caller moves to the new SHA. A `dependabot.yml` in the calling
repository that watches the `github-actions` ecosystem opens that pull
request. Dependabot finds a new version through this repository's
`vX.Y.Z` tags. It finds the caller's version from the tag that points
at the pinned SHA, and it changes the version in the comment after the
SHA when it moves the pin. So write the tag of the pinned commit there,
as the examples show.

Dependabot moves the pins inside this repository too: the gitleaks
image and the actions the scan uses. A release carries them to each
caller.

## Releasing this repository

This repository releases with its own release workflow. One tag covers
the release workflow and the scan. Run Release from the Actions tab
here and choose the part to raise:

- major: a caller must change, such as a removed or renamed input, or
  a renamed folder.
- minor: a caller gains something, such as a new input.
- patch: a fix or a dependency update in the release workflow or the
  scan.

No caller pins an inherited file, so a change to one needs no release.

Publish the draft as for any release. Dependabot offers the new tag to
each caller.
