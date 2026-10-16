# A way back for responders who've gone quiet

One-pager · Product, Dispatch · 16 October 2026 · Draft for Helen Achebe

## Problem
A responder who misses a few pings is ranked lower, so gets fewer pings, so has fewer chances to be ranked back up. Nothing tells the responder, their handler or us. After 4.2 (12 Aug) this went from rare to common: four responders fell from 28% of all pings to 9%, and 59% of their pings were missed (about 14% for everyone else, up from 2%). Only about 14% of missed pings became a ticket, so tickets understate it.

**Vesper is one example, not the whole brief.** Vesper (handler: Aunt Dot) got 13-15 pings a week and took about 82%. After 4.2 that fell to 5, 2 and 1 a week, with one taken. Farlight, Meteor Mite and The Undertow went the same way, and Corporal Ashgrove and Halfmoon are sliding. Aunt Dot only noticed "quiet weeks". Kip had Meteor Mite (quiet) and The Gale (busy, same area) on one screen, "two different products," and could only say "hang in there."

**Why:** the 4.2 cut from a 90s to a 60s ping wait caused many more misses. In `history.py` a missed ping lowers the recent-acceptance score by 0.12, the same as a turn-down, and nothing restores it (a 2019 note asked whether it should). Wen Li has not yet confirmed this.

## Proposal
The system fixes this itself. Neither the responder nor the handler has to do anything.
1. **Switch the ping wait back to 90 seconds.** A config value. It should also ease the "gone before I could answer" tickets.
2. **Missed pings stop counting as turn-downs.** The Glossary treats them as different; the scoring code doesn't.
3. **Scores ease back toward neutral on their own** (the 2019 question, answered yes). I'd start at about a week; Wen Li sets it.
4. **One-time reset to neutral when the fix ships**, so the four already pushed down start level.
5. **Automatic alert to the PM and engineering** when a responder's pings fall by more than half against their recent average.

Information only: a "Gone quiet" flag on the handler's card ("Vesper: 1 ping this week, usually 13-15. 5 of the last 8 were missed") and a message on the responder's phone that their place is recovering. "Mark ready" is an optional handler shortcut. Clickable: `prototype.html`.

## Success measure
The four back to 10+ pings a week; missed pings back toward 2%; fewer "phone never goes off" and "gone before I could answer" tickets; the next drop flagged to us within days. Ravi Menon owns the weekly numbers; these are my own queries and he hasn't checked them.

## Scope
Not in this: reverting the proximity change (it stays weighted up); guaranteeing anyone a callout or sending test callouts; showing routing scores or letting handlers reorder the list; any action required of a responder; the Responder Availability Record; anything about who a responder is; mutual aid and shared cover (Q4).
**Risks:** a longer wait holds a callout 30 seconds more per unanswered ping, so watch time-to-accept. A responder who is genuinely away is pinged again once their score recovers. 4.2 shipped the wait and proximity changes together, so restoring the wait first, then measuring, is how we learn which mattered.

## Open questions
- **Helen:** comfortable reversing the ping wait? I found no written reason for 60s.
- **Wen Li:** confirm the mechanism, the recovery period, whether a restart can do the reset, and that the code snapshot matches production. Her routing scores for the four on 11-12 Aug would show how much is the score and how much is proximity.
- **Marcus Oyelaran:** effort, and whether it fits 4.3. **Sofia Marino:** flag and phone screen.
- **Availability Confidence** (committed for 4.2, no brief, not in release notes): same thing? And why these four and not The Gale?
