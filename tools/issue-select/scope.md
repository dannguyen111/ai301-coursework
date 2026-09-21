# Scope: where to look, and who is looking

<!--
This file is the skill's field of view. The rubric (rubric.md) decides
whether an issue is GOOD; the scope decides which issues are candidates
at all, and whose hands the issue would land in. It applies in live mode
only: in eval mode the bundle is the whole world and this file is
ignored.

Two parts. Staff wrote the first; you write the second.
-->

## Where candidates come from

Only issues in the course's Path Review repository are candidates:

- Repo: `codepath/pathreview-ai301-fa26-s3`

Do not search, fetch, or grade issues from any other repository, however
promising. The wider GitHub comes later in the course; for now the field
is Path Review.

**Path Review house rule.** Path Review is a classroom, and your
classmates are not strangers. Ignore the usual claim signals here: other
students' claim comments (and there may be several on one issue) do not
block an issue, and finding some on the issue you want is normal. Claim
anyway: course credit attaches to the pull request you open, not to
whether it merges, so a shared issue costs nobody anything. Everything
else in the rubric applies as written.

## Your fit profile

Python is the language I can actually read and debug without fighting the
syntax; I can follow JavaScript when I have to, but I would not choose it.
I want a small, reproducible bug fix rather than a feature or a docs
change - a bug gives me an obvious "before and after" to verify, and
chasing one is the fastest way to learn how a codebase is wired.

I have a few hours total for Unit 2, so setup cost matters as much as the
fix does. Rank up issues that live in one or two files and run from a
plain `pip install` or `npm install`; rank down anything that needs
Docker, a database, or a multi-service local stack before the first test
can run. I would also rather avoid pixel-level CSS and visual design
calls, where "correct" is a judgement I am not yet equipped to make.

What I want out of this is confidence with the contribution loop itself -
reproduce, fix, test, open the PR - so a boring bug I can finish beats an
interesting one I stall on.
