# Contributing

Thank you for looking.

This file says how to contribute. What this repository is, and how to
check your work in it, is in the repository's own documentation.

## Bug reports

Open the **Bug report** form on the Issues tab. The form asks
what happened, what you expected instead, and how to reproduce it. Answer
all three.

A bug report starts a conversation, not a fix. Write it in the hope that
somebody with the same problem solves it with you. That somebody may be
you: where the source is public, fork it and send a pull request.

## Support questions

Do not open an issue to ask how something works. Use the Discussions tab.

An issue tracker records defects and agreed work. A question posted
there sinks under them and gets no better answer for the wait.

## Proposing a change

Open the **Feature request** form on the Issues tab. Say what
problem it solves, not only what it adds. Wait for an answer before you
write the feature. This saves you from writing something we then decline.

Use an issue, not a discussion. An accepted proposal becomes work, and
work is tracked on the issue tracker.

Be ready to write some of the work you propose. A proposal nobody
implements stays a proposal.

A bug fix, a typo or a broken link needs no proposal. Send the pull
request.

## Which branch?

Branch from `main`, and open your pull request against it. For almost
every change that is the whole answer.

This repository may also carry a branch named `N.x` — `1.x`, `2.x` — one
for each released major version. One appears only when an older major
needs a patch after a newer one starts, so there is usually none. Where
one exists, send a bug fix for that major to its branch.
Send a feature, and anything that breaks compatibility, to `main`.

If you cannot tell which branch your change belongs on, open the pull
request against `main` and say so in it. We would rather move it than
lose it.

## Pull requests

Run the checks first, where this repository has them. Its own
documentation says how. Where continuous integration runs, it runs
those same checks, so a green run on your computer is a good sign
rather than the whole answer.

Every pull request lands squashed. Your commits become one commit on the
target branch, named after the pull request title, and that title is the
line the release notes carry. Write it as the sentence you want a reader
to find there.

The pull request template asks for these. Answer it in your own words.

- **One change per pull request.** A fix and a rename in one branch take
  twice as long to read.
- **A test that fails without your change.** This applies where this
  repository has tests. Write that test before you fix a bug.
- **A reason in the commit message.** The diff says what changed. The
  message says why.
- **Source, not output.** Do not commit a generated or compiled file,
  unless this repository says it tracks one. Nobody can review a
  generated file, and one can carry what is not in the source.
- **Allow edits by maintainers.** Leave the box ticked. It lets us
  rebase your branch or fix a typo without asking you to push again.
- **This repository's license.** Your contribution uses the terms in
  its `LICENSE`.

## Releases

Where this repository releases, it releases when a change is worth
releasing. There is no schedule and no release day.

A version follows semver, tagged `vMAJOR.MINOR.PATCH`. A workflow drafts
the release with notes from the pull request titles it contains.
Publishing the draft cuts the tag. Nobody tags by hand.

## Security vulnerabilities

Never open a public issue for a vulnerability. Report it through the
**Security** tab, which opens a private thread with the maintainer.
`SECURITY.md` says what to include and what happens next.

## Coding style

Match the file you are editing. Follow its wrapping, its names, and the
shape of its comments. Consistency inside one file beats any rule from
outside it.

Where this repository documents a style or carries a formatter, that
wins.

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
