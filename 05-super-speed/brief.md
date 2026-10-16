# A way back for responders who've gone quiet

One-pager · Product, Dispatch · 16 October 2026 · Draft for Helen Achebe
- **Owner:** PM, Rook Dispatch (me)
- **Helen Achebe:** Director of Product; the draft is for her, and she decides on reversing the ping wait
- **Sofia Marino:** designs the handler flag and phone screen
- **Marcus Oyelaran:** Engineering Manager; his team builds it
- **Ravi Menon:** owns the weekly numbers
- **Wen Li:** Staff Engineer; confirms the mechanism and sets the recovery period

## Problem
When a responder misses a few pings, the system ranks them lower, so they get fewer pings and have no chance to climb back. Nobody is told. Since 4.2 (12 Aug), four responders have gone from 28% of all pings to 9%, and most of their pings go unanswered. Tickets show only part of it.

**Vesper is one example, not the whole brief.** Vesper (handler: Aunt Dot) used to get 13-15 pings a week. Now she gets 1-5. Aunt Dot only noticed "quiet weeks". Farlight, Meteor Mite and The Undertow went the same way, and Corporal Ashgrove and Halfmoon are sliding.

**Why:** 4.2 cut the ping wait from 90s to 60s, so more pings were missed. The code counts a missed ping the same as a turn-down and never restores the score. Wen Li has not yet confirmed this.

## Proposal
The system fixes this itself. Neither the responder nor the handler has to do anything.
1. **Switch the ping wait back to 90 seconds.** A config value. It should also ease the "gone before I could answer" tickets.
2. **Missed pings stop counting as turn-downs.** The Glossary treats them as different; the scoring code doesn't.
3. **Scores ease back toward neutral on their own** (the 2019 question, answered yes). I'd start at about a week; Wen Li sets it.
4. **One-time reset to neutral when the fix ships**, so the four already pushed down start level.
5. **Automatic alert to the PM and engineering** when a responder's pings fall by more than half against their recent average.

Information only: a "Gone quiet" flag on the handler's card ("Vesper: 1 ping this week, usually 13-15. 5 of the last 8 were missed") and a message on the responder's phone that their place is recovering. "Mark ready" is an optional handler shortcut. Clickable: `prototype.html`.

## Success measure
Baselines are before 4.2 (12 Aug); targets are proposed, for Helen and Ravi to confirm. Measured weekly, starting the week after the fix ships.

| Measure | Now (since 12 Aug) | Target |
|---|---|---|
| Pings a week, the four (Vesper, Farlight, Meteor Mite, The Undertow) | 1-5 | 10+ each, within 4 weeks of shipping |
| Pings a week, Corporal Ashgrove and Halfmoon | 7-9 | Back to 10-11 each |
| Missed pings, everyone else | about 14% | About 2%, within 4 weeks |
| Callout tickets a week | 3-5x normal | Back to about 6.5 a week (the level before 12 Aug) |
| Next drop in a responder's pings | Not noticed until tickets or interviews | Alert reaches PM and engineering within 3 days |

Watch time-to-accept so the longer wait doesn't cost us. Ravi Menon owns the weekly numbers; the "now" figures are my own queries and he hasn't checked them.

## Scope
**In scope:**
- The five fixes above, for every responder
- The four starved responders are the worked example; Corporal Ashgrove and Halfmoon are tracked in the measures
- The "Gone quiet" flag and the phone message are information only
- "Mark ready" is an optional handler shortcut; nothing is required of a handler or responder

**Not in this:**
- Reverting the proximity change (it stays weighted up)
- Guaranteeing anyone a callout or sending test callouts
- Showing routing scores or letting handlers reorder the list
- Any action required of a responder or handler
- The Responder Availability Record
- Anything about who a responder is
- Mutual aid and shared cover (Q4)

**Risks:**
- A longer wait holds a callout 30 seconds more per unanswered ping, so watch time-to-accept
- A responder who is genuinely away is pinged again once their score recovers
- 4.2 shipped the wait and proximity changes together, so restoring the wait first, then measuring, is how we learn which mattered

## Open questions
- **Helen:** comfortable reversing the ping wait? I found no written reason for 60s.
- **Wen Li:** confirm the mechanism, the recovery period, whether a restart can do the reset, and that the code snapshot matches production. Her routing scores for the four on 11-12 Aug would show how much is the score and how much is proximity.
- **Marcus Oyelaran:** effort, and whether it fits 4.3. **Sofia Marino:** flag and phone screen.
- **Availability Confidence** (committed for 4.2, no brief, not in release notes): same thing? And why these four and not The Gale?
