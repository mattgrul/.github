# Working in this repository

This is the `.github` repository of `mattgrul`. Every file the README
lists as inherited shows on every repository of the account that has no
copy of its own, including repositories that do not exist yet. The
README says what inherits and how the release workflow is called. This
file says how to write here.

## Write for the repository that shows the file

A reader sees an inherited file on one repository's page. Write it as
if it lived there.

- Say "this repository" and mean the one that shows the file.
- State only what holds for any repository: how to report something,
  what a good bug report contains, what a pull request looks like.
- Put a fact about a language, a runtime or a subject in the repository
  it is true of.
- Keep the file silent about this repository and the account. The one
  exception is the security link in `.github/ISSUE_TEMPLATE/config.yml`,
  which GitHub requires as an absolute URL.

The test: a future repository may be a library, a web application, a
font or a dataset. A sentence that reads oddly on any of those comes
out.

## Settings that hold these files true

`mattgrul/personal-infra` configures every repository of the account as
code. Five things in this repository depend on it, and a change there
falsifies them without warning.

- The issue forms set `labels:` on a new issue. `personal-infra` gives
  every repository `bug`, `enhancement` and `needs-triage`. GitHub drops
  a missing label from the form without a warning, and also requires
  each label to exist in this repository.
- "Every pull request lands squashed, named after the pull request
  title" in `CONTRIBUTING.md` is the merge setting: squash only, title
  from the pull request.
- "A reason in the commit message" holds because the squashed commit
  keeps the branch's commit messages as its body.
- "Use the Discussions tab" holds because `personal-infra` turns
  Discussions on for every public repository unless its entry says
  otherwise. A private repository keeps Issues only.
- The caller example in the README grants `contents: write` because
  `personal-infra` defaults the workflow token to read.

No setting chooses the branch a pull request targets. The ruleset
protects `main` and each `N.x` from a direct push and a force push, and
that is all. So "Which branch?" in `CONTRIBUTING.md` asks for judgement
and promises no check.

## Files that stay absent

Each of these was considered and left out. Add one only when its reason
stops being true.

- `FUNDING.yml`: the account accepts no sponsorship.
- `SUPPORT.md`: it would repeat `CONTRIBUTING.md`.
- `.github/DISCUSSION_TEMPLATE/`: every repository keeps the categories
  GitHub creates, and a form would describe what one repository
  discusses.
- `.github/dependabot.yml`: nothing inherits it, and the release
  workflow pins no action.
- `workflow-templates/`: a starter workflow is copied once and drifts
  from here. A repository calls a workflow here instead.
- A test workflow: it must name a runtime.
- A stock code of conduct: GitHub awards its community-profile tick only
  for a stock template. Every stock template names a contact and
  promises a reporting process, and the account has neither.
  `CODE_OF_CONDUCT.md` is written here instead and forgoes the tick.

## The release workflow

`.github/workflows/release.yml` is allowed here because it names no
language and no runtime. Keep it that way.

A caller pins it by commit SHA, so an edit here reaches no repository
until that caller moves its SHA. The workflow drafts a release and
commits nothing, because the ruleset on a protected branch lets only an
admin push and the workflow token is not one. A tag is outside the
branch ruleset, so the version lives in the tag, and publishing the
draft creates it.

## Conventions

- Wrap prose at 76 columns and code at 80.
- Open a pull request against `main`. The branch rules in
  `CONTRIBUTING.md` apply here.

## Agent skills

### Issue tracker

Issues live in this repository's GitHub Issues, through the `gh` CLI.
See `docs/agents/issue-tracker.md`.

### Triage labels

The five default triage labels, each named for its role. See
`docs/agents/triage-labels.md`.

### Domain docs

Single-context: one `CONTEXT.md` and `docs/adr/` at the root, created
lazily. See `docs/agents/domain.md`.
