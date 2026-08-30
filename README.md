# .github

Community health files for every repository this account owns.

**Editing a file here changes every repository this account owns, public
and private, that has no copy of its own.** GitHub reads these files and
shows them in place. Nothing is copied — a clone of another repository
still contains none of this.

This repository must stay public. GitHub does not support a private
repository for default files.

## What inherits, and what does not

| File | Inherited |
|---|---|
| `SECURITY.md` | yes |
| `CONTRIBUTING.md` | yes |
| `CODE_OF_CONDUCT.md` | yes |
| `.github/ISSUE_TEMPLATE/` | yes, all or nothing |
| `README.md` | no — this page only |
| `LICENSE` | **never** |

A repository with its own copy of a file uses that one and ignores this one.
That is the only way to opt out.

Issue templates are all or nothing: a repository with any file in its own
`.github/ISSUE_TEMPLATE/` ignores every template here.

`LICENSE` cannot be inherited, by GitHub's design — *"License files must be
added to individual repositories so the file will be included when a project
is cloned, packaged, or downloaded."* Every repository needs its own.

## The rule for anything added here

> The files that inherit apply to every repository this account owns —
> including ones that do not exist yet. So nothing here may describe what
> those repositories **are**. State only what is true of any repository: how
> to report something, what a good bug report contains, what a pull request
> should look like.
>
> Anything true of a language, a runtime or a subject belongs in the
> repository it is true of.

A future repository might be a library, a web application, a font, a
dataset. A sentence that reads oddly on any of those does not belong here.
That is the whole test.

## What is deliberately absent

`FUNDING.yml` would advertise sponsorship, but this account accepts none.
`SUPPORT.md` is a second door saying what `CONTRIBUTING.md` already says. A
pull request template, with one maintainer, would only nag its author.
Discussion category forms describe what a repository discusses, which is
what nothing here may do.

The tick beside "Code of conduct" on GitHub's community profile is also
absent, and stays absent. GitHub awards it only for a stock template,
and every stock template names a contact and promises a reporting
process. This account runs neither, so `CODE_OF_CONDUCT.md` is written
here instead and forgoes the tick.

`.github/workflows/` held a shared shell test workflow once. Nothing
inherits a workflow — a caller names it — so it may name a language or a
runtime, which is what nothing here may do. `.github/dependabot.yml` went
with it. That file existed only to keep the workflow's action pins
current.
