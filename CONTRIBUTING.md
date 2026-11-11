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

Start a discussion in the **Ideas** category of the Discussions tab. Say
what problem the idea solves, not only what it adds. Wait for an answer
before you write the feature. This saves you from writing something we
then decline.

Do not open an issue for an idea. An accepted idea becomes an issue, and
the work is tracked there.

Be ready to write some of the work you propose. A proposal nobody
implements stays a proposal.

A bug fix, a typo or a broken link needs no proposal. Send the pull
request.

## Which branch?

Branch from `main`, and open your pull request against it. For almost
every change that is the whole answer.

This repository may also carry a branch named `N.x` — `1.x`, `2.x` — one
for each released major version. That version can be the current stable
release or an older one, while `main` holds the work toward the next
release. Where one exists, send a bug fix for that major to its branch.
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

We look for these in every pull request.

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

AI tools are welcome here. Use an agent, a code assistant or anything
else that helps you do good work. Your name is on the contribution, so
you answer for all of it, whoever wrote it.

You need not read every line a tool writes. You must know what the
change does and why, and you must check that it works. Before you send
it:

- Say in your own words what problem it solves and how.
- Run the checks, and try the change yourself where you can.
- Remove what the change does not need: unrelated edits, extra layers,
  comments that repeat the code.
- Be ready to answer questions about it. "The tool wrote it" is not an
  answer.

We close without review an issue or pull request that nobody checked,
that solves a problem nobody has, or that buries its point in generated
text. We may block an account that sends a bulk run of them.

## Code of conduct

`CODE_OF_CONDUCT.md` holds the standard. It applies wherever you reach
us: an issue, a pull request, a discussion or a review.
