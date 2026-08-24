# Security policy

Report a vulnerability through GitHub's private reporting, on the repository
it affects: open its **Security** tab and choose **Report a vulnerability**.
That opens a private thread with the maintainer. Do not open a public issue
for a vulnerability.

Tell us what you can:

- The repository and the version or commit you tested.
- What an attacker reaches, and what they need first.
- The steps that reproduce it.

We answer within seven days. If a report is valid, we agree a disclosure
date with you before we publish anything.

These repositories are shell installers that run on your own computer, under
your own account. The risks worth reporting are the ones that cross that
line: a path a script writes outside the folders it declares, a file it
takes from the network without checking, or a way a third party changes what
it runs.
