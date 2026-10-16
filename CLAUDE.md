# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

I am the new PM for **Rook Dispatch** (started Mon 24 Aug 2026; today is mid-Oct 2026). My director is Helen Achebe. Sources: rook-wiki (About Rook, Glossary, Team directory, Releases, Q3 roadmap, Product briefs) and Priya's handoff doc (`00-rook/company/notes/handoff-from-priya.docx`). The `rook-database` connector (read-only SQL; tables callouts, pings, responders, handlers, support_tickets; data 29 Jun to 6/7 Sep 2026) was queried in session 1.

### Company and products
- Rook Industries: coordination and provisioning software for masked responders and their handlers. Subscription, priced per active responder. Founded 2014, HQ Site Aleph; offices in Berlin, Singapore, Cornwall.
- **Rook Dispatch** (mine): availability, proximity, who gets pinged for a callout, whether they take it. Users: handlers (console, desktop) and responders (phone).
- **Rook Supply**: requisitions, maintenance, failure reports. Users: handlers and quartermasters.
- Ships monthly on a release train; point releases are 4.x.
- **Confidentiality:** responder cover identities are never stored and Rook holds no mapping to legal identities (Security Policy 4.1). Never design for, or try to work out, who anyone is.

### People
| Person | Role | Notes |
|---|---|---|
| Helen Achebe | Director of Product (my boss) | Owns roadmap and commitments |
| Marcus Oyelaran | Engineering Manager, Dispatch | Site Aleph; runs the eng team |
| Wen Li | Staff Engineer, Dispatch | Berlin; built the ping-ranking logic; no written doc, talk to her |
| Sofia Marino | Product Designer | Console and phone app; ran the September interviews |
| Ravi Menon | Data Analyst | Singapore; owns the weekly acceptance numbers |
| Nadia Hoffmann | Support Lead | Berlin; owns tickets; offers a standing 15 minutes |
| Priya Raghunathan | Previous Dispatch PM | Left 21 Aug; only PM for 14 months |

Wiki comments use roles, not names: "Engineering manager" = Marcus, "Staff engineer" = Wen Li, "Support lead" = Nadia, "Product designer" = Sofia, "Priya" = Priya. Handlers appear in the Customer interviews database (Aunt Dot, Mr. Ambrose, Halloran, Kip); I haven't read those yet.

### Vocabulary
- **Callout** (unit of work) → **ping** (one callout offered to one responder) → **taken**, **turned down**, or **missed** (no answer within the **ping wait**). Turned down and missed both pass the ping on, but are recorded separately.
- **Acceptance rate** = pings taken / pings offered. Dispatch's headline metric. **Time-to-accept** = median seconds from ping to taken.
- **Coverage gap** = no available responder had the required **capability tags**. Different from low acceptance.
- **Routing priority** = score that ranks responders: proximity (travel-time estimate), availability, capability match, recent acceptance history. Turning down or missing pings lowers the recent-acceptance part, which lowers later ranking.
- **Responder Availability Record**: written by Dispatch, read by Supply. **Mutual aid**: not supported; on the Q4 exploration list.
- Supply: **requisition**, **field failure report**, **service interval**. **Quartermaster** owns stock and approvals.

### Where things stand
**Releases:** 4.0 (7 Apr): console navigation, profile redesign, routing override audit log. 4.1 (16 Jun): travel-time proximity, bulk callout, push reliability. 4.2 (12 Aug): proximity weighted up vs. acceptance history, ping wait 90s → 60s, persistent console filters, three defect fixes.

**4.2 is the open problem.** After release:
- Callout tickets ran about 3x normal from 12 Aug and were still elevated on 26 Aug. Split about two thirds "my phone never goes off" and one third "gone before I could answer".
- Nadia could explain the second (the 60s wait) but not the first. A handler emailed her directly, which is rare.
- Marcus asked on 14 Aug whether the proximity change was meant to apply to responders who turn pings down. The config doesn't distinguish, and he wasn't sure if that was a decision. Wen Li was away until 24 Aug and nobody has answered.
- Priya's view is that it's mostly seasonal ("August is always soft") and that reverting would just trade one angry group for another. The database contradicts it (see Data findings below). Ravi has the official weekly numbers (Priya's note that Marcus can pull numbers is wrong).
- Two changes shipped together (proximity weighting and a shorter ping wait), so effects are confounded.
- Likely mechanism (fits the data, not confirmed by Wen Li): missed pings lower recent acceptance, which lowers ranking, which means fewer pings, which compounds. Marcus asked for a regroup once I'd had a week; I don't know whether it happened.

**Roadmap (Q3, last reviewed 30 Jun, so stale):**
- 4.2 committed: change to who gets pinged (shipped), ping timeout tuning (shipped as 90 → 60s), **Availability Confidence** (not in the 4.2 release notes, so it appears to have slipped).
- 4.3 committed: requisition approval chains (Supply).
- Q4 exploring: handler phone app, shared cover between responders.
- All items list Priya as owner; they need reassigning. Priya said the Q3 commitments conversation with Helen never happened. Roadmap changes go through Product.

**Briefs:** Bulk Callout (Jan, shipped in 4.1 though the brief calls it unowned/next quarter; lacks a time-to-full-coverage baseline). Routing Override Audit Log (Mar, shipped in 4.0). Handler Phone App (8 Sep, Q4 exploration; the brief names Sofia as owner while the roadmap names Priya). Requisition Approval Chains (Jul; the core ask is a second approval over $2,000, but the brief has scope-crept into a dashboard, routing around approvers and replacing a spreadsheet; it needs trimming).

### Learned in session 1
- Wiki search matches titles only; comments (where the 4.2 story lives) show up only via read_page.
- Wiki comments name roles, never people; use the mapping above.
- Roadmap and briefs are partly stale or inconsistent with the release notes. Check Releases before trusting a status.
- Priya's handoff reflects her own read and contains at least one error (who owns the numbers). Verify claims in it before repeating them.
- Not yet read: Customer interviews (Sofia, Sept), Research page.

### Data findings (rook-database, my own queries; confirm against Ravi's weekly numbers before presenting)
- **Not seasonal.** Weekly acceptance was flat at 75–78% for six weeks, then fell to 54% in the week of 12 Aug (missed pings 2–6 a week before, 38 that week). It was 66% for two weeks and 73% by the week of 31 Aug, still below baseline. A step on release day is not a seasonal pattern.
- **Four responders were nearly cut out:** Farlight (handler Linda Pruitt), Meteor Mite (Kip), The Undertow (Desmond Okafor), Vesper (Aunt Dot). They got 11–15 pings a week and took about 75% before 12 Aug. Each had 4–5 misses in the first week after release, then fell to 1–5 pings a week, nearly all missed. Tickets from 17–20 Aug match ("phone has not gone off in 3 days"). Other responders' acceptance dropped about 10 points but their volume held.
- **Ping wait effect:** pings per callout went from about 1.24 to 1.61 in release week, then about 1.3.
- 49 callouts after 12 Aug had no taker; I have no pre-release baseline for that.
- **Code confirms the mechanism** (`00-rook/code/dispatch-routing/`, a snapshot; may not match production). `history.py` scores a missed ping the same as a turned-down one (-0.12; a taken ping is +0.08), with no decay (a 2019 TODO left it that way). `config.py` weights since 4.2: proximity 0.60 (was 0.45), recent acceptance 0.25 (was 0.40), capability 0.15. Weights are global, so nothing treats turn-down responders differently, which answers Marcus's question: it fell out that way. A responder who stops being pinged can't earn points back.
- Not explained: why these four. Kip's other responder, The Gale, is fine, and shares an area with Meteor Mite. The database has no location, capability or score data.
- Next step: confirm the mechanism with Wen Li, decide between fixes (stop counting missed pings against ranking, or restore the 90s wait), and call the four handlers.

### Contradictions and gaps in the sources
- Glossary says missed and turned down are recorded separately; the code records them separately but scores them the same.
- README says ranking only orders the list, but ordering decides who actually gets pinged, which is why starved responders exist.
- About Rook says monthly releases; actual releases were 7 Apr, 16 Jun, 12 Aug.
- Bulk Callout brief (Jan) says unowned, but it shipped in 4.1. Its baseline was never set.
- Halloran is a handler in the interviews database but acts as the quartermaster in the Supply briefs.
- Every roadmap item lists Priya, including a Supply item. Handler Phone App lists Priya on the roadmap but Sofia in its brief. Mutual aid (Glossary) and Shared cover between responders (roadmap) look like one Q4 item.
- Availability Confidence (committed 4.2) is missing from the release notes and changelog, and has no brief.
- Nothing after 28 Aug in the wiki or 7 Sep in the database: no record of 4.3, the regroup, or any weight change.
- No Ravi weekly report, no August 2025 data, no Supply owner in the directory, empty `feedback/` folder, no written description of ranking.
- Priya waited on 19 Aug although the starved-responder tickets (17 and 20 Aug) were already filed.

### Open to-dos from the handoff
1. Check my database findings against Ravi's weekly numbers and last year's August.
2. Get the ranking logic explained by Wen Li, then write it down (nobody has).
3. Agree with Helen which Q3 items are still commitments, and reassign ownership.
4. Standing 15 minutes with Nadia. Don't let console filter-persistence tickets eat my time.

Session 3 (pings vs tickets, per-responder rows):
- Only Farlight (Linda Pruitt) and The Undertow (Desmond Okafor) filed tickets about being starved, about 10 each from 17 Aug. Aunt Dot (Vesper) and Kip (Meteor Mite) filed none; both described it only in their 3-4 Sep interviews. This corrects the "tickets match all four" line above. Only about 14% of missed pings (about 110 from 12 Aug) became "gone before I could answer" tickets, so ticket volume understates the problem.
- The four starved responders share one thing: 4-5 missed pings in 12-16 Aug (everyone else had 3 or fewer). Area, handler, prior volume, prior acceptance and time of day don't separate them. The `responders` table does have an `area` column (one area each except Eastgate, shared by Meteor Mite and The Gale). Meteor Mite fell to 14 pings while The Gale kept 69, same area and handler.
- Their share of all pings fell from about 28% to about 9%. Corporal Ashgrove and Halfmoon slid about 25% (10-11 to 7-9 a week) and are worth watching.
- Pings and tickets agree: every ticket claim I could check matched the ping counts. Tickets split two thirds "quiet" to one third "gone before I could answer"; the gone-before ones came first, the quiet ones a week later. Total tickets ran 3-5x the 6.5 a week before 12 Aug.
- I drafted a note to Helen asking which fix to lead with (stop counting missed pings against ranking, or restore the 90s wait; I lean to the first). Still open: Wen Li's confirmation and routing scores for the four on 11 and 12 Aug, Ravi's check of these numbers, and anything after 7 Sep.

Session 4 (reading the routing code, `00-rook/code/dispatch-routing/`):
- 4.2 changed only three values in `config.py` (wait 90 to 60s, proximity weight 0.45 to 0.60, recent-acceptance weight 0.40 to 0.25); no logic changed. The lower acceptance weight softens the penalty (a score of 0 costs at most 0.125 of rank, was 0.20), so it doesn't explain the compounding. The shorter wait is the main suspect for the misses; the proximity weight may have reshuffled who is asked first. I can't separate the two without routing scores.
- Only two things raise a score: a taken ping (+0.08) and the 0.5 starting score for someone never seen. A miss or a turn-down costs 0.12, with no decay or reset (2019 TODO never built), so a quiet responder stays where they were and can only climb by being pinged and saying yes. In this snapshot scores sit in memory (`_scores`); whether a restart resets them in production is unknown.
- The weights are global, so the 4.2 change applied to everyone; nothing treats responders who turn pings down differently (answers Marcus's 14 Aug question). The four starved responders weren't habitual turn-downs: 21.6% turned down before 12 Aug, the same as everyone else (20.9%).
- Pings table, rechecked: turn-downs stayed about 21% to 18% but misses went from about 2% to about 14% for everyone else, and 59% for the four since 12 Aug. Misses were still elevated in the week of 31 Aug (21, against 2-6 before), mostly from responders other than the four.
- Engineering comments worth following up with Wen Li and Marcus: the 2019 decay TODO; "same either way" for missed and turned down, written when the wait was 90s; README saying ranking only sets the order when the order decides who is pinged; `config.py` asking that the engineering manager be told of changes; the README owner fallback that didn't work while Wen Li was away; the Supply contract on the availability record.
- Saved a one-page plain English summary for Helen at `04-x-ray-vision/helen-summary-4-2-routing.md` and drafted a message to Wen Li and Marcus (in chat only). The code folder has no history of its own (one commit on 13 Oct) and no sign of any change after 4.2; still unconfirmed with Wen Li whether the snapshot matches production.

Session 5 (brief and prototype for Helen, `05-super-speed/brief.md` and `prototype.html`):
- Helen asked for a one-pager and something clickable on the fix, seen from the person it happens to, not "a setting". Vesper (handler Aunt Dot) is the worked example; Meteor Mite (Kip) is the second. The brief says Vesper is one example of a wider problem (four starved, Corporal Ashgrove and Halfmoon sliding).
- Direction I chose: the system fixes it, with nothing asked of the responder or handler. Restore the 90s ping wait (I said "90 minutes" but meant seconds), stop counting missed pings as turn-downs, let scores recover over time (the 2019 TODO answered yes), a one-time reset to neutral on release, and an automatic alert to PM and engineering when a responder's pings halve. The handler flag and "Mark ready" are information and a shortcut only.
- This reverses the earlier line that the 60s wait was a separate decision: I now treat it as the main cause of the misses. 4.2 also changed the proximity weights, so the two are still confounded; restore the wait first, then measure. The proximity change stays.
- Prototype has two tabs (Kip and Meteor Mite; Aunt Dot and Vesper), the responder's quiet-week message, and an incoming-ping screen with a 90s timer. Location and capability on that screen are invented; "about 6 days" recovery is a placeholder for Wen Li to set. Not browser-tested.
- Still open: Wen Li (mechanism, recovery period, whether a restart resets scores, snapshot vs production, routing scores for the four on 11-12 Aug); Ravi has not checked my numbers; Helen has not said yes to reversing the wait and I found no written reason for 60s; Marcus on effort and 4.3; Availability Confidence overlap. A handler phone app (Aunt Dot's mock-up) stays a Q4 exploration, not part of this brief.
