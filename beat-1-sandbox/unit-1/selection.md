# Unit 1 - Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60

**Verdict output**

Live-mode output of `issue-select` on the chosen issue, pasted verbatim:

```
## Summary

**Issue #60** — "Faithfulness checker crashes when a context chunk has `text: None`" in `codepath/pathreview-ai301-fa26-s3`. In scope (correct repo). Note: opened by `Aburke225`, who is a `COLLABORATOR` — the Path Review house rule on shared claims doesn't apply here since there are zero claim comments anyway.

| Check | Grade | Evidence |
|---|---|---|
| repo-alive | pass | `archived: no`; newest default-branch commit 2026-09-16, 5 days before today (2026-09-21) |
| unclaimed | pass | `assignees: []`, 0 comments, no linked/mentioned PRs found for #60 |
| bounded-scope | pass | Single deliverable: one `.get()` default-vs-`None` bug in `FaithfulnessChecker.check()`, with exact repro steps and a named failing test |
| settled-spec | pass | 0 comments, 0 linked PRs (closed or open) |
| maintainer-endorsed | pass (n/a) | Bug report (labeled `bug`), not a feature request — check auto-passes |
| ai-policy-allows | pass | `docs/CONTRIBUTING.md` covers branch naming, commits, CI, and even seeded-bug/xfail conventions, but never mentions AI-assisted contributions — silence passes |
| first-response-known | pass | Sampled 5 recently-updated issues (#67, #57, #62, #69, #68) — all comments present, block gathered |

All required checks pass → **accept**.

Preferred (rank/context only, don't gate verdict):
- `maintainer-responsive`: **fail** — the 5 sampled recently-updated issues each show only a student claim comment, no maintainer reply yet.
- `release-recency`: **fail** — no GitHub releases published (repo ships from `main`, which is why this is preferred, not required).
- `newcomer-signposted`: **pass** — carries `good first issue` and `tier-1` labels.

Fit note (scope.md): this is a Python-only, single-function bug in one file (`rag/evaluator/faithfulness_checker.py`) with a ready-made failing test — no Docker/DB spin-up needed to reproduce it once dependencies are installed, and it gives a clean before/after. Matches the stated preference well.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60",
  "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived: no; newest default-branch commit 2026-09-16, 5 days before capture (2026-09-21)"},
    {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; 0 comments on the issue; no linked or mentioned PRs for #60"},
    {"name": "bounded-scope", "grade": "pass", "evidence": "Single .get()-default-vs-None bug in FaithfulnessChecker.check(), with exact repro steps and a named failing unit test"},
    {"name": "settled-spec", "grade": "pass", "evidence": "0 comments; 0 linked PRs in any state"},
    {"name": "maintainer-endorsed", "grade": "pass", "evidence": "Bug report labeled `bug`, not a feature request — check applies only to feature requests"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md details workflow, CI, and seeded-bug conventions but is silent on AI-assisted contributions"},
    {"name": "first-response-known", "grade": "pass", "evidence": "Sampled 5 recently-updated issues (#67, #57, #62, #69, #68) for maintainer response latency"},
    {"name": "maintainer-responsive", "grade": "fail", "evidence": "0 of 5 sampled issues have a maintainer/collaborator comment yet, only student claim comments"},
    {"name": "release-recency", "grade": "fail", "evidence": "Repo has 0 published GitHub releases"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "Labels: good first issue, tier-1, bug, rag"}
  ],
  "verdict": "accept"
}
```
```

---

## Eval iterations

**Run history**

Two runs, in order:

1. Partial run, `--only issue-01,issue-04,issue-09,issue-12,issue-20` - **5/5 scored items**.
   No bar verdict is printed on a partial run. These five were chosen deliberately as the
   cases most likely to break the rubric before paying for a full run: the two long-body
   accepts (`issue-01`, `issue-09`), the one-line-body accept (`issue-04`), the sole
   `policy` item (`issue-12`), and the unendorsed feature request (`issue-20`).
2. Full run, all 20 scored bundles - **20/20 scored items (bar: 18/20: PASS)**, with
   `categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 4/4`.
   This is the run saved by `--save-run` and committed as `eval-run.txt`.

The final score, 20/20, is the agreement line in the committed `eval-run.txt`.

**Issue analysis**

`issue-12` (`bookwyrm-social/bookwyrm#1133`, category `policy`).

- My rubric's decision: **reject**.
- Gold label: **reject**.

My rubric rejected it on exactly one check, `ai-policy-allows`, and on nothing else. Every
other required check passed, and that is the whole point of the issue: the repo is alive
(last push 2026-08-12, the capture date itself), the issue is unclaimed (`assignees: none`,
no linked PRs, and the one claim-shaped comment - "I've started to look at this" from
2024-09-19 - sits 23 months before the capture date, so my 90-day staleness window does not
treat it as blocking), the scope is a single bounded UI change to a progress bar, and it
carries `good first issue`. On the four lecture families it is a clean accept.

What sank it is the fifth surface. The repo-facts line quotes BookWyrm's contributing docs:
"Meaningful human interaction is the whole point of BookWyrm. We do not accept AI-generated
code or documentation." My `ai-policy-allows` check reads that as a refusal with no
compliant path - there is no disclosure or human-review term that would make an AI-assisted
pull request acceptable there - so it grades `fail`, and my verdict rule turns a single
required failure into `reject` with no compensation from the three preferred passes.

This is also the check that carried the category floor. `policy` has exactly one member in
the whole eval set, so `ai-policy-allows` is the only reason my run scored `policy 1/1`
instead of `policy 0/1`. Without it the run would have been 19/20 and would still have
failed the bar, because the floor requires at least one match in every category.

**Check rationale**

Quoted as currently written in the `rubric.md` uploaded to `tools/issue-select/`:

> | `ai-policy-allows` | Repo facts: the `contribution policy` line (CONTRIBUTING.md, any
> doc it links to, and any `AI_POLICY.md` / `AGENTS.md` it mentions). | The policy does not
> **ban** AI-assisted contributions. A ban is a refusal with no compliant path - "we do not
> accept AI-generated code or documentation". **Conditions are not bans**: requirements to
> disclose, to personally understand, to test, to human-review, or a rule against *fully*
> AI-generated work all pass, because this course's workflow can meet them. **Silence
> passes**: most repos state nothing, and that is not a restriction. | required |

The reasoning behind its current form is that the raw signal is nearly useless without the
two exclusions. Counting any mention of AI as a restriction would have been a disaster on
this set: `issue-01`, `issue-09` and `issue-16` all sit on conda, whose policy has a whole
"Generative AI" section, and `issue-08` and `issue-15` sit on zulip, whose policy closes
AI-generated PRs that look untested. All five of those policies are conditions I can
actually satisfy - disclose, understand, test, review - and three of those issues are gold
accepts. So the check had to be written to separate a refusal from a term.

I drew the line at whether a compliant path exists. "You must understand and test your
change" and "we do not accept fully AI-generated contributions" both leave a way to
contribute honestly; "we do not accept AI-generated code or documentation" does not. The
silence clause is the third piece: 13 of the 20 bundles say nothing about AI at all, and
`unclear` counts as `fail` everywhere else in my rubric, so without an explicit carve-out
stating that silence passes, this check would have rejected 13 of the 20 bundles -
including five of the eight gold accepts.

**Trade-offs**

What this check gives up is the middle of the range: a policy that is hostile without being
a ban passes it. `issue-10` (`tldr-pages/tldr`) is the case I accept that it will miss. Its
policy "strongly discourages generative AI for new pages" and closes "pull requests
suspected of being made wholly or partly with generative AI or machine translation without
human review". By my wording that is a condition, not a ban, so `ai-policy-allows` grades it
`pass` - and in the committed run `issue-10` was rejected on `bounded-scope` instead, for
being a megaissue. Had that issue been a bounded one, my rubric would have accepted a repo
where an AI-assisted PR is likely to be closed on suspicion alone. I am taking that
deliberately: the alternative wording rejects conda and zulip too, which costs five issues
to save a hypothetical one.

Nothing else in the run changed because of this check, and here is how I know: I kept the
per-check results of that same full run with `--out`, and in them `ai-policy-allows` appears
in the failed-check list of exactly one issue, `issue-12`. It is absent from all 19 other rows, including all
eight gold accepts. It is a single-purpose check that fires once on this set, which is the
behaviour I wanted - the other four families do the volume of the work, and this one exists
to catch the one thing they structurally cannot see.

---

## Selection rationale

**Selection rationale**

*1. The issue's fit to my interests and to the time available.*

I can read and debug Python without fighting the syntax, and issue #60 is Python end to end:
one function, `FaithfulnessChecker.check()`, in one file,
`rag/evaluator/faithfulness_checker.py`. The bug is that `chunk.get("text", "")` returns
`None` when the key exists with a `None` value, because a `.get()` default only applies to
missing keys, and the following `" ".join(...)` then raises `TypeError`. The issue ships
the reproduction as four lines of Python and names the failing test,
`test_none_context_chunk_text`. That matters more to me than the bug being interesting,
because I have a few hours for Unit 2, not a few days. There is no Docker, no database and
no multi-service stack between me and the first failing test - the repo runs on plain
pytest - and no CSS or visual judgement, which I wanted to avoid. I get a clean
before/after: the test fails, I fix the default handling, the test passes.

*2. What the verdict identified correctly, and what I weighed that the rubric could not.*

The verdict got the mechanical facts right, and got them right for stated reasons rather
than by vibe: the repo is not archived and was pushed to on 2026-09-16, five days before the
run; the issue has no assignee, no comments and no linked PRs; it is a bug rather than a
feature, so `maintainer-endorsed` correctly did not apply; and the repo's
`docs/CONTRIBUTING.md` is silent on AI, so the policy surface is clear. It also flagged two
preferred failures honestly instead of hiding them - `maintainer-responsive` failed because
none of the five sampled recently-updated issues has a maintainer reply yet, and
`release-recency` failed because the repo publishes no GitHub releases at all.

What I weighed that the rubric could not is that both of those failures are artefacts of
this being a classroom repo, not evidence of a dying project. A course repo a few weeks into
a term has no releases because there is nothing to release, and slow first responses because
the maintainers are instructors reading dozens of threads. In a real repo I would treat that
pair as a warning; here I discounted both. The rubric also cannot rank on what the fix
teaches me, and of the three issues it accepted I chose the one whose failure mode -
`.get()` with a default that does not apply to an explicit `None` - is a Python bug I expect
to meet again, rather than the regex-widening in #53 or the anchoring fix in #54.

*3. The anticipated difficulty in claiming it.*

Low, and the house rule is most of the reason. Path Review's `scope.md` says classmates'
claim comments do not block an issue and that credit attaches to the pull request I open
rather than to whether it merges, so even if someone claims #60 before I do, claiming it too
costs nobody anything. As of my live run the issue had zero comments and no assignee, so
there is nothing to share yet. The real risk is not the claim, it is the race: #60 is
labelled `good first issue` and `tier-1`, it is one of the smallest fixes in the tracker,
and that combination is exactly what everyone else's rubric will also rank first. I also do
not yet know the maintainers' response latency, because my own sample found no maintainer
replies at all, so I should not count on an assignment being confirmed before I start. I
plan to write the Unit 2 claim comment and open the PR on the assumption that nobody will
answer it, and treat any reply as a bonus.

---

Related paths: `eval-run.txt` in this directory; the skill's files in
`tools/issue-select/`.
