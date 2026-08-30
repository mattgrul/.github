# Contributing

Thank you for looking.

This file serves every repository this account owns, so it says nothing
about any one of them. What a repository is, and how to check your work
in it, belongs in its README.

## Bug reports

Open the **Bug report** form on the repository it affects. The form asks
what happened, what you expected instead, and how to reproduce it. Answer
all three.

A bug report starts a conversation, not a fix. Write it in the hope that
somebody with the same problem solves it with you. That somebody may be
you: where the source is public, fork it and send a pull request.

## Support questions

Do not open an issue to ask how something works. Use the Discussions tab
on the repository it concerns. If the repository has no Discussions tab,
open an issue instead.

An issue tracker records defects and agreed work. A question posted
there sinks under them and gets no better answer for the wait.

## Proposing a change

Open the **Feature request** form on the repository it affects. Say what
problem it solves, not only what it adds. Wait for an answer before you
write the feature. This saves you from writing something we then decline.

Use an issue, not a discussion. An accepted proposal becomes work, and
work is tracked on the issue tracker.

Be ready to write some of the code you propose. A proposal nobody
implements stays a proposal.

A bug fix, a typo or a broken link needs no proposal. Send the pull
request.

## Which branch?

Branch from `main`, and open your pull request against it. For almost
every change that is the whole answer.

A repository may also carry a branch named `N.x` — `1.x`, `2.x` — one for
each released major version. A repository grows one only when it has to
patch an older major after a newer one starts, so most repositories here
have none. Where one exists, send a bug fix for that major to its branch.
Send a feature, and anything that breaks compatibility, to `main`.

If you cannot tell which branch your change belongs on, open the pull
request against `main` and say so in it. We would rather move it than
lose it.

## Pull requests

Run the repository's checks first. Its README says how, and the commands
differ from one repository to the next. Where continuous integration
runs, it runs those same checks, so a green run on your computer is a
good sign rather than the whole answer.

Every pull request lands squashed. Your commits become one commit on the
target branch, named after the pull request title, and that title is the
line the release notes carry. Write it as the sentence you want a reader
to find there.

We look for these:

- **One change per pull request.** A fix and a rename in one branch take
  twice as long to read.
- **A test that fails without your change**, where the repository has
  tests. For a bug, write it first.
- **A reason in the commit message.** The diff says what changed. The
  message says why.
- **Source, not output.** Do not commit a generated or compiled file.
  Nobody can review one, and it can carry code that is not in the
  source.
- **Allow edits by maintainers.** Leave the box ticked. It lets us
  rebase your branch or fix a typo without asking you to push again.
- **The receiving repository's license.** Your contribution uses the terms
  in that repository's `LICENSE`.

## Releases

We release when a change is worth releasing. There is no schedule and no
release day.

A version follows semver, tagged `vMAJOR.MINOR.PATCH`. A workflow cuts
the tag and writes the release notes from the pull request titles it
contains. Nobody tags by hand.

## Security vulnerabilities

Never open a public issue for a vulnerability. Report it through the
repository's **Security** tab, which opens a private thread with the
maintainer. `SECURITY.md` says what to include and how fast we answer.

## Coding style

Match the file you are editing. Follow its wrapping, its names, and the
shape of its comments. Consistency inside one file beats any rule from
outside it.

Where a repository documents a style or carries a formatter, that wins.
Its README says so.

## AI-assisted contributions

Use whatever tools help you. Review, test and understand every line
before you send it.

We do not accept a contribution that is mostly generated and never
thought about. We close a bulk run of generated issues or pull requests
without review, and we may block the account that sent it.

Read the code first. Send work that shows your own understanding of the
problem you solve.

## Code of conduct

`CODE_OF_CONDUCT.md` holds the standard. It applies wherever you reach
us: an issue, a pull request, a discussion or a review.
