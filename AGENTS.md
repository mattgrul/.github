# Working in this repository

This is the `.github` repository of `mattgrul`. Every file the README
lists as inherited shows on every repository of the account that has no
copy of its own, including repositories that do not exist yet. The
README says what inherits, how a repository calls the release workflow
and the gitleaks scan, and how this repository releases. This file says
how to change it.

## Write for the repository that shows the file

A reader sees an inherited file on one repository's page. Write it as
if it lived there.

- Say "this repository" and mean the one that shows the file.
- State only what holds for any repository: how to report something,
  what a good bug report contains, what a pull request looks like.
- Put a fact about a language, a runtime or a subject in the repository
  it is true of.
- Keep the file silent about this repository and the account.

The test: a future repository may be a library, a web application, a
font or a dataset. A sentence that reads oddly on any of those comes
out.

## Settings that hold these files true

A private settings repository configures every repository of the
account as code. Each item below depends on it, and a change there
falsifies the item without warning.

- The issue forms set `labels:` on a new issue. The settings
  repository gives every repository `bug`, `enhancement` and
  `needs-triage`. GitHub drops a missing label from the form without a
  warning, and also requires each label to exist in this repository.
- "Every pull request lands squashed, named after the pull request
  title" in `CONTRIBUTING.md` is the merge setting: squash only, title
  from the pull request.
- "A reason in the commit message" holds because the squashed commit
  keeps the branch's commit messages as its body.
- "Use the Discussions tab" holds because the settings repository
  turns Discussions on for every repository, public or private, unless
  its entry says otherwise.
- The caller examples in the README grant `contents: write` because
  the settings repository defaults the workflow token to read.
- The job name `checks` in `.github/workflows/checks.yml` is a
  required check. The settings repository names it in the ruleset of
  this repository, next to `gitleaks-scan`. GitHub names a check after
  its job, so a pull request with a renamed job waits for a check that
  never reports.
- `.github/dependabot.yml` labels its pull requests `dependencies`
  alone. The settings repository gives every repository that label and
  deletes any label it does not name, which would include the
  ecosystem label Dependabot adds by default.

No setting chooses the branch a pull request targets. The ruleset
protects `main` and each `N.x` from a direct push and a force push, but
no rule names a target branch. So "Which branch?" in `CONTRIBUTING.md`
asks for judgement and promises no check.

## Files that stay absent

Each of these was considered and left out. Add one only when its reason
stops being true.

- `FUNDING.yml`: the account accepts no sponsorship.
- `SUPPORT.md`: it would repeat `CONTRIBUTING.md`.
- A feature request form: an idea starts in Discussions and becomes an
  issue only once accepted. The issue chooser cannot link to it either.
  GitHub drops a relative contact link, and an absolute one would send
  every repository to the Discussions of one.
- `.github/DISCUSSION_TEMPLATE/`: every repository keeps the categories
  GitHub creates, and a form would describe what one repository
  discusses.
- `workflow-templates/`: a starter workflow is copied once and drifts
  from here. A repository calls a workflow here instead.
- A test workflow for callers: it must name a runtime. The gitleaks
  scan's own test names none.
- A stock code of conduct: GitHub awards its community-profile tick only
  for a stock template. Every stock template names a contact and
  promises a reporting process, and the account has neither.
  `CODE_OF_CONDUCT.md` is written here instead and forgoes the tick.

## The release workflow

`.github/workflows/release.yml` is allowed here because it names no
language and no runtime. Keep it that way.

README lists the jobs a caller may add: one that reads its version from
a file, and one that attaches its artifacts. Keep the workflow general
enough that a caller needs no third.

The workflow drafts a release and commits nothing. The header of
`release.yml` says why. When the account owner asks for a release of
this repository, choose the part to raise from the list in README.

## The gitleaks scan

`gitleaks-scan/` is allowed here for the same reason: gitleaks is one
image, and it reads a file of any kind. Keep it that way.

The shared rules live here because they hold for any repository. A
caller's own `.gitleaks.toml` replaces them, so the action takes no
input for rules.

It is an action, not a reusable workflow, because an action can read
its own files: the rules, and the Dockerfile that pins gitleaks. A
reusable workflow sees only the caller's checkout. A caller calls it by
the folder's path, so renaming the folder is a major release.

`gitleaks-scan/test` makes each fake secret when it runs. Make a new
fake secret the same way, so the repository holds only safe text.

Dependabot reads an `action.yml` only in a folder that an entry in
`.github/dependabot.yml` names. A new action folder gets its own
`github-actions` entry after the shared text, in the same pull request.
A folder that holds a Dockerfile also gets a `docker` entry.

## Checks

Run these from the repository root before you push. Both need Docker.

```bash
# Prove the rules. Run it after a change to gitleaks-scan/.
gitleaks-scan/test
# Scan the files of this checkout.
docker build --quiet --tag gitleaks-scan gitleaks-scan
docker run --rm -v "$PWD:/repo:ro" -w /repo gitleaks-scan dir
```

No test covers `release.yml`. After a change to it, trace each refusal
and each path of its script by hand against the README's description.

<!-- BEGIN shared text. Change it in the template repository. Write this repository's own text outside these lines. -->

Every repository of this account has the rules below. A rule above
them is this repository's own, and it wins when the two disagree.

## Pull Requests

Open a pull request for every change. A ruleset protects `main` and
each `N.x` branch, so do not push to them. A pull request merges by
squash only, and the squash commit takes the pull request title, so
write the title as the change, in one sentence.

Merge a pull request only after every check on it passes, not only
the required ones. The ruleset requires `gitleaks-scan` in every
repository. When a check fails, fix the cause.

## Shared Text

The text between the `BEGIN shared text` and `END shared text` marker
lines is the same in every repository of this account. It is in
`AGENTS.md`, in each file in `docs/agents/` and in
`.github/dependabot.yml`.

- Write text that only this repository needs outside the markers:
  above them in `AGENTS.md`, below them in the other files.
- Change the shared text only in the template repository. In any
  other repository the next sync replaces the change, so propose it
  to the account owner instead.
- In the template repository, a change to the shared text reaches
  every repository at the next sync. Make it only when it holds true
  for all of them, and say so in the pull request. After the merge,
  the account owner runs the sync.

## Public Text

Public repositories carry the shared text. Each new repository also
starts with a copy of every file in the template repository. A later
commit cannot take text out of that history. So in the shared text and
in the template, name no private repository and no person, and give no
detail of a check or a setting that shows a way past it. Name a public
repository only where a file or its reader needs the name.

## Gitleaks Scan

The scan fails on keys, tokens, email addresses and home folder paths,
in the files and in each commit of a pull request. Write paths
relative to the repository, and keep personal data out of files and
commit messages.

- Keep the job name `gitleaks-scan`. The ruleset requires a check of
  that name.
- For one known finding that is not a secret, add a `gitleaks:allow`
  comment on its line, or add the finding to a `.gitleaksignore`.
- Add a `.gitleaks.toml` only when the shared scan rules cannot work.
  It replaces all of them.

## Checks Workflow

Run the checks of the repository's own code, such as its tests and
its linters, in `.github/workflows/checks.yml`. Name the workflow
`checks`. Keep the scan in its own workflow. A repository with no
checks of its own has no `checks` workflow.

- Name the required job `checks`. The ruleset requires a check of
  that name in each repository that has the workflow, and GitHub
  names a check after its job. Do not rename the job, because the
  ruleset then waits for a check that never reports.
- When the checks need more than one job, make `checks` the last job.
  It waits for the others and fails when one of them fails, so the
  ruleset requires one name only:

  ```yaml
  checks:
    needs: [lint, unit]
    if: always()
    runs-on: ubuntu-latest
    steps:
      - if: contains(needs.*.result, 'failure') || contains(needs.*.result, 'cancelled')
        run: exit 1
  ```

  Keep `if: always()`. Without it, a failed job does not fail
  `checks`.

## Actions

Pin each action to a full commit SHA, with its version in a comment on
the same line. GitHub refuses a workflow that names an action by tag.
Dependabot moves the SHAs.

The steps of the scan and the release workflow live in the repository
that the workflows call. Change them there.

## Dependabot

Follow `docs/agents/dependabot.md` in the same pull request when the
repository adds a package type, such as Composer, npm or Go modules,
or when an `N.x` branch starts or stops getting fixes.

Once CI tests the project, merge a dependency pull request when its
checks pass. Until then, check it by hand before you merge it.

## Releases

Draft a release with the Release workflow:
`gh workflow run release.yml -f bump=<patch|minor|major>`. It raises
that part of the highest `vX.Y.Z` tag. To release from an `N.x`
branch, add `--ref N.x`. The workflow then raises the highest
`vN.Y.Z` tag, and it refuses `major`. The account owner publishes the
draft, and publishing creates the tag.

## Agent skills

### Issue tracker

When a skill reads or writes issues, follow
`docs/agents/issue-tracker.md`.

### Triage labels

When a skill names a triage role, take its label from
`docs/agents/triage-labels.md`.

### Domain docs

Before a skill explores the code or names a domain concept, read
`docs/agents/domain.md`.

<!-- END shared text -->
