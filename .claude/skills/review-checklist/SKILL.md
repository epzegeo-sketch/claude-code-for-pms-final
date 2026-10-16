---
name: review-checklist
description: Runs the same four-point review on a product brief before it goes any further. Use when the user asks to review, check or sanity-check a brief (or says "run the review checklist"), and points at a brief file or pastes one.
---

# Review checklist for briefs

Apply these four checks, in this order, to the brief the user points at. Read the whole brief first. Judge only what is written on the page; do not fill gaps from memory or other sources. If the brief is missing, ask which one to review.

## The four checks

1. **Owner.** The brief names who owns it, by name or role, in one clear place.
   - Fail if there is no owner, more than one owner with no lead, or an owner that conflicts with another line in the brief.
2. **Success measure.** The brief says how we will know it worked: a metric or observable outcome, a baseline (where we are now), and a target or threshold.
   - Fail if success is only "ship it", or if there is a metric with no baseline.
3. **Scope consistency.** The scope at the end matches the scope at the start.
   - Compare the opening statement of scope (summary, goal, problem) with the closing scope (requirements, deliverables, plan, out-of-scope list). List anything that appears only at the end (creep) and anything promised at the start that disappears (dropped).
4. **Problem before solution.** The brief explains the problem (who has it, what happens, evidence) before it proposes a fix.
   - Fail if a solution appears before the problem is described, or the problem is never described apart from the solution.

## Output

Use this format every time:

**Brief:** <title or file name>

| Check | Result | Evidence |
|---|---|---|
| Owner | Pass / Fail / Unclear | quote or section |
| Success measure | Pass / Fail / Unclear | quote or section |
| Scope consistency | Pass / Fail / Unclear | quote or section |
| Problem before solution | Pass / Fail / Unclear | quote or section |

**Verdict:** Ready to move on / Fix before it goes further.

**Fixes needed:** one line per Fail or Unclear, saying exactly what to add or change. If everything passes, write "None."

## Rules

- Quote the brief for each result; no result without evidence.
- Use "Unclear" when the brief is ambiguous rather than guessing.
- Stay on these four checks. If you spot something else (typos, tone, feasibility), add at most one line under "Also noticed", and only if it matters.
- Do not edit the brief unless the user asks.
