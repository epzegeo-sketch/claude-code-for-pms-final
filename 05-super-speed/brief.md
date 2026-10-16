# A way back for responders who've gone quiet

One-pager · Product, Dispatch · 16 October 2026 · Draft for Helen Achebe

## Problem
A responder who misses a few pings is ranked lower, so gets fewer pings, so has fewer chances to be ranked back up. Nothing tells the responder, their handler or us. After 4.2 (12 Aug) this went from rare to common: four responders fell from 28% of all pings to 9%, and 59% of their pings were missed (about 14% for everyone else, up from 2%). Only about 14% of missed pings became a ticket, so tickets understate it.

**Vesper is one example, not the whole brief.** Vesper (handler: Aunt Dot) got 13-15 pings a week and took about 82%. After 4.2 that fell to 5, 2 and 1 a week, with one taken. Farlight, Meteor Mite and The Undertow went the same way, and Corporal Ashgrove and Halfmoon are sliding. Aunt Dot only noticed "quiet weeks". Kip had Meteor Mite (quiet) and The Gale (busy, same area) on one screen, "two different products," and could only say "hang in there."

**Why:** a missed ping lowers the recent-acceptance score by 0.12, the same as a turn-down, and nothing restores it (a 2019 note in `history.py` asked whether it should). The 4.2 cut from a 90s to a 60s ping wait caused many more misses. Wen Li has not yet confirmed this.

## Proposal
1. **Missed pings stop counting as turn-downs.** The small change engineering could ship this afternoon. Alone it fixes the cause going forward, but nobody would notice, and it doesn't lift anyone already pushed down.
2. **Handlers see it.** A "Gone quiet" flag on the responder's card: "Vesper: 1 ping this week, usually 13-15. 5 of the last 8 were missed." Aunt Dot: "I don't need to do anything about it. I'd just like to know."
3. **A way back that isn't a job.** The handler sends a ready check, a message and not a callout. One tap from the responder ("I'm here, phone works") puts them back to a neutral place in the order, not the top.
4. **The responder is told** on their phone why pings have been rare, and what the tap does.

Clickable version: `prototype.html` (made-up screens, real numbers, not connected to Dispatch).

## Success measure
The four back to 10+ pings a week; missed pings back toward 2%; ready checks used and fewer "my phone never goes off" tickets. Ravi Menon owns the weekly numbers; these are my own queries and he hasn't checked them.

## Scope
Not in this: reverting 4.2 (proximity stays weighted up); the 60s ping wait ("gone before I could answer" is a separate decision); guaranteeing anyone a callout, or sending a test callout; showing routing scores or letting handlers reorder the list; the Responder Availability Record Supply reads; anything about who a responder is; mutual aid and shared cover (Q4).
**Risk:** a responder who is genuinely away keeps their rank, and each ping to them burns 60 seconds. That's why the ready check is part of this.

## Open questions
- **Wen Li:** confirm the mechanism, that a ready check can safely reset a score, and that the code snapshot matches production.
- **Marcus Oyelaran:** effort for 1 versus 2-4, and whether it fits 4.3. **Sofia Marino:** design of the flag and phone screen.
- **Availability Confidence** (committed for 4.2, no brief, not in the release notes): same thing? And why these four and not The Gale?
