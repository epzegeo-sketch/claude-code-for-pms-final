# Dispatch 4.2: why some responders stopped getting pinged

For: Helen Achebe | From: Dispatch PM | Mid-October 2026

## In one sentence
4.2 appears to have started a feedback loop that has pushed a few responders to the bottom of the ping list, and the way the code scores them means they can't climb back up.

## What we're seeing
- Weekly acceptance held at 75-78% for six weeks, then fell to 54% in the week of 12 Aug (release day). It was back to 73% by the week of 31 Aug, still below normal. This is a step on release day, not a seasonal dip.
- Four responders (Farlight, Meteor Mite, The Undertow, Vesper) were getting 11-15 pings a week. After release they got 1-5, nearly all missed. Their share of all pings fell from about 28% to about 9%.
- Callout tickets ran 3-5x normal. Only about 14% of missed pings turned into tickets, so the tickets understate the problem.

## What 4.2 changed
Three settings, no new logic:
1. The time to answer a ping went from 90 to 60 seconds. This is the likely cause of the extra misses.
2. Distance now counts for more when deciding who is asked first (0.45 to 0.60).
3. A responder's recent track record counts for less (0.40 to 0.25).

## Why it gets stuck
The ranking code treats a missed ping exactly like a refusal, and it takes points off (0.12) with no way of earning them back unless the responder is pinged again. Responders who missed several pings in the first week fell down the list and were asked less, which gave them fewer chances to recover. Nothing in the code treats responders differently, so this wasn't a decision. It is how the settings combine.

This answers Marcus's 14 Aug question about whether the change was meant to apply to responders who turn pings down. The settings are the same for every responder, new or long-standing, and nothing in the code separates those who turn pings down from anyone else. The four affected responders weren't habitual turn-downs either: before 12 Aug they turned down 22% of pings, the same as everyone else (21%).

## What I'm not sure about
- This comes from my own database queries and the code snapshot. Ravi hasn't checked the numbers, and Wen Li hasn't confirmed the mechanism or that the snapshot matches production.
- Two changes shipped together, so I can't yet say which one did more.
- I can't explain why these four and not others, such as a responder in the same area who was fine.
- I have no data after 7 Sep, so I don't know if anything has changed since.

## The decision I need from you
Which fix should lead:
- **A. Stop counting missed pings against a responder's ranking.** Targets the loop. This is my lean.
- **B. Restore the 90-second wait.** Quick, but it brings back the problem the shorter wait was meant to solve, and it doesn't free responders already stuck at the bottom.

## Next steps
- Wen Li and Marcus: confirm the mechanism, and pull routing scores for the four on 11-12 Aug.
- Ravi: check my numbers against the weekly report.
- Call the four affected handlers once we have a fix.

I'd like 15 minutes this week to agree on A or B.
