# Rubric: is this a good first issue?

Seven required checks and three preferred ones. The required checks are the
four failure families from the lecture (maintainer alive, repo in use, scope
fits a newcomer, nobody else is on it) plus the contribution-policy surface,
which can kill an otherwise perfect issue before a maintainer reads a line of
code.

**Measuring dates.** Every "within N days" threshold below is measured against
the bundle's `captured:` date in eval mode, and against today's date in live
mode. Never against the date the repo looks busy.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `repo-alive` | Repo facts: the `archived:` flag on the repo line, and the newest date in the `last 5 default-branch commits` list. | `archived: no` **and** the newest default-branch commit is dated within **90 days** of the capture date. An archived repo fails outright: read-only cannot take a pull request. A bot-authored commit counts only if it merged a human's pull request. | required |
| `unclaimed` | Repo facts `this issue: assignees:` and `linked PRs:` (with each PR's state), plus every comment in the thread and its date. | All three hold: (a) `assignees: none`; (b) no linked PR is in the `open` state, from this repo or a fork; (c) no comment claiming the work ("I'll take this", "working on this", "can I pick this up") is dated within **90 days** of capture *unless* a maintainer (OWNER / MEMBER / COLLABORATOR) has since told other contributors to go ahead. A claim older than 90 days is stale and does not block. Closed or merged linked PRs are not claims. | required |
| `bounded-scope` | The issue title and body, and any maintainer comment describing the size of the fix. | The issue asks for **one deliverable**, even if that deliverable touches several files. It fails only when: the body is an explicit tracking, umbrella, meta or "mega" issue (a list of other issue numbers or sub-items meant to become separate pull requests); or the ask is a codebase-wide campaign with no endpoint ("incrementally add X wherever it makes sense", "PRs welcome big and small"); or a maintainer states the fix requires reworking core internals; or the issue is a pure usage/support question rather than a change. **A terse body is not a scope failure.** A one-line bug report, a short enumerated list of related cases inside one subsystem, or an unpolished writeup all pass - grade the size of the work being asked for, not the polish of the writeup. | required |
| `settled-spec` | The comment thread (count and content), and the states of the linked PRs. | No sign the work is contested or has already defeated people: **fewer than 2 linked PRs in the `closed` (unmerged) state**, **and** not both of (more than **20** comments) and (no maintainer comment settling the design). A long thread that ends in a maintainer decision passes; a long thread still arguing about what the right behavior is does not. | required |
| `maintainer-endorsed` | The issue's `opened by` line with its author association, its labels, and any maintainer comment in the thread. | This check applies **only to issues asking for new user-facing functionality** (a feature or enhancement). Bug reports and documentation tasks pass automatically. A feature request passes if **at least one** of: it was opened by an OWNER, MEMBER or COLLABORATOR; or it carries a maintainer-applied triage label (`good first issue`, `help wanted`, `accepted`, or an equivalent); or a maintainer has endorsed it in the thread. An unlabelled feature wish opened by a non-member with no maintainer reply is a product decision that has not been made yet: fail. | required |
| `ai-policy-allows` | Repo facts: the `contribution policy` line (CONTRIBUTING.md, any doc it links to, and any `AI_POLICY.md` / `AGENTS.md` it mentions). | The policy does not **ban** AI-assisted contributions. A ban is a refusal with no compliant path - "we do not accept AI-generated code or documentation". **Conditions are not bans**: requirements to disclose, to personally understand, to test, to human-review, or a rule against *fully* AI-generated work all pass, because this course's workflow can meet them. **Silence passes**: most repos state nothing, and that is not a restriction. | required |
| `first-response-known` | Repo facts: the `maintainer first-response sample` block. | The block is present in the evidence, whatever it says. This check exists so the grader must look at response latency rather than skip it; the latency itself is scored by `maintainer-responsive` below and never gates the verdict. | required |
| `maintainer-responsive` | Repo facts: the `maintainer first-response sample` (5 recently updated issues, days to first owner/member/collaborator comment). | At least 2 of the 5 sampled issues got a maintainer comment, and the fastest of those was within **30 days**. | preferred |
| `release-recency` | Repo facts: the `latest release` line. | A release published within **365 days** of capture. A repo with no published releases does not fail the verdict on this: some healthy projects ship from the default branch only, which is why this check is preferred and `repo-alive` carries the liveness. | preferred |
| `newcomer-signposted` | The issue's labels. | The issue carries at least one label a maintainer uses to signpost newcomer work: `good first issue`, `help wanted`, `easy`, `documentation`, or an equivalent. | preferred |

## Verdict rule

**Accept if and only if every `required` check grades `pass`.** A single
required `fail` produces `reject`; there is no third verdict and no
compensation - a preferred check cannot rescue a required failure.

`unclear` counts as `fail` on required checks. If the evidence a required
check names is genuinely absent from the bundle, the issue is not verifiable
and therefore not a first issue to take. The one deliberate exception is
written into `ai-policy-allows`, where a repo stating no policy is silence,
not absence: grade that `pass`.

Preferred checks never change the verdict. Report their grades, and on an
accepted issue use them to rank it against the other accepted candidates:
more preferred passes ranks higher, and among equals the fit profile in
`scope.md` breaks the tie.
