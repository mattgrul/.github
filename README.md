# .github

Community health files for every repository this account owns.

**Editing a file here changes every repository, public and private, with no
way to opt out.** GitHub reads these files and shows them on any repository
that has none of its own. Nothing is copied — a clone of another repository
still contains none of this.

## What inherits, and what does not

| File | Inherited |
|---|---|
| `SECURITY.md` | yes |
| `CONTRIBUTING.md` | yes |
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

> Everything here is inherited by every repository this account owns —
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

`CODE_OF_CONDUCT.md` names a contact and promises a process, so it waits
until there is a public repository with contributors to have conduct.
`FUNDING.yml` would put a Sponsor button on private repositories.
`GOVERNANCE.md` describes decision-making among several maintainers.
`SUPPORT.md` is a second door saying what `CONTRIBUTING.md` already says. A
pull request template, with one maintainer, would only nag its author.

## Reusable workflows are not here

They live in [`workflows`](https://github.com/mattgrul/workflows).

Nothing inherits a workflow — a caller names it — so those files may be
specific about a language or a runtime, which is exactly what nothing here
may be. `shell-tests.yml` lived here once and left for that reason.
