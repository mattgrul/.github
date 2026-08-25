# Contributing

Thank you for looking. These are small repositories, so the process is
short.

## Before you open a pull request

Run both checks from the repository root:

```bash
./tests/shellcheck.sh
./tests/all
```

Those two paths are the convention for a repository whose CI calls the
shared `shell-tests.yml` workflow: `tests/all` runs the suite and
`tests/shellcheck.sh` lints the scripts. A repository that does not call it
may name its tests differently — check its own README.

Where CI does run, the suite runs on Linux and on macOS and the linter runs
once on Linux, so a green run on your computer is a good sign but not the
whole answer.

## What we look for

- **One change per pull request.** A fix and a rename in one branch take
  twice as long to read.
- **A test that fails without your change.** For a bug, write it first.
- **The style of the file you are editing.** Match its wrapping, its comment
  shape, and its names.
- **A reason in the commit message.** The diff says what changed. The
  message says why.

## Shell scripts here target bash 3.2

macOS ships bash 3.2.57 at `/bin/bash`, and these scripts use `#!/bin/bash`,
so that is the version a Mac runs. No associative arrays, no `${x^^}`, no
`mapfile`. Linux ships bash 5, so your computer will not catch a mistake
here. Continuous integration will.

## Allow edits from maintainers

Leave **Allow edits by maintainers** ticked when you open the pull request.
It lets us rebase your branch or fix a typo without asking you to push
again.
