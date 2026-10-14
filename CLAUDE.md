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

I am the new PM for **Rook Dispatch** (started 24 Aug 2026), replacing Priya Raghunathan, who left 21 Aug with no overlap. Sources: rook-wiki (About Rook, Glossary, Team directory, Releases, Q3 roadmap, Product briefs, 4.2 page comments) and Priya's handoff doc (`00-rook/company/notes/handoff-from-priya.docx`). Wiki comments use roles, not names; the map is below.

### Company and products
- Rook Industries sells coordination software to independent masked responders and their handlers. HQ is Site Aleph; offices are in Berlin and Singapore. Subscription pricing is per active responder.
- **Rook Dispatch** (mine): availability, proximity, who gets pinged for a callout, and whether they take it. Handlers use the web console. Responders use the native phone app. Monthly release train, 4.x numbering. Routing config ships in the release and is not a runtime setting.
- **Rook Supply**: requisitions, quartermaster approvals, maintenance, field failure reports. It reads the Responder Availability Record, which Dispatch writes. Any change to how Dispatch calculates availability lands in Supply's maintenance scheduling automatically.
- **Hard rule:** responder cover identities are never stored. We hold capability tags, availability and callout history only. Never design anything that assumes a cover-to-legal-identity mapping, and never try to work out who anyone is. Read Security Policy 4.1 before touching responder records.

### People (role in wiki comments -> person)
| Role | Person | Notes |
| --- | --- | --- |
| Engineering manager | Marcus Oyelaran, Site Aleph | Runs Dispatch engineering. Priya's first stop for anything uncertain. |
| Staff engineer | Wen Li, Berlin | Built routing (who gets pinged). Only real source on how ranking works. Prefers direct messages. |
| Support lead | Nadia Hoffmann, Berlin | Owns tickets and hears handler complaints first. Priya recommended a standing 15 minutes. |
| Product designer | Sofia Marino, Site Aleph | Owns console and phone app. Ran the September interviews. |
| Data analyst | Ravi Menon, Singapore | Owns the numbers and the weekly acceptance report. |
| Director of Product | Helen Achebe, Site Aleph | My director. Owns roadmap and commitments. |
Correction to the handoff: Priya says the engineering manager can pull numbers. The wiki says Ravi owns them, so go to Ravi for real data. Marcus can only give rough figures.

### Vocabulary
- **Callout**: request for a responder to attend an incident. **Ping**: one callout offered to one responder's phone.
- Ping outcomes: **taken**, **turned down**, **missed** (the ping wait ran out). Missed and turned down both pass the ping on, but they are recorded separately.
- **Ping wait**: how long a ping stays before it counts as missed. It is the same for everyone.
- **Acceptance rate**: share of pings taken. This is the headline metric. **Time-to-accept**: median seconds from ping to taken.
- **Coverage gap**: no available responder had the required capability tags. This is not the same as low acceptance.
- **Routing priority**: the ranking score. Inputs are proximity (travel-time estimate), availability, capability match and recent acceptance history. Turning down or missing pings lowers recent acceptance, which lowers a responder's place in later orders.
- **Capability tags**: flight, structural-entry, hazmat-tolerant, cold-weather, aquatic, crowd-management, de-escalation.
- **Mutual aid**: responders covering for each other across areas. Not supported; on the Q4 exploration list.
- Supply terms: requisition, field failure report, service interval.

### Where things stand
**Releases:** 4.0 (7 Apr: new nav, profile redesign, override audit log). 4.1 (16 Jun: travel-time proximity, bulk callout, push reliability). 4.2 (12 Aug): proximity weighted up vs recent acceptance, ping wait cut from 90s to 60s, console filters persist, three defect fixes. The 4.2 rollout was clean, with no rollback.

**4.2 problem (my first priority):**
- Since 4.2, fewer pings are being taken and ticket volume is about 3x normal, still elevated on 26 Aug. About two thirds say "phone never goes off". About one third say "gone before I could answer". The second theme is explained by the 60s ping wait. Nobody has explained the first.
- Priya and Marcus attribute it to a seasonal August dip that will recover in September. This is a hypothesis, not a finding. There is no data yet, and two changes shipped together. One handler emailed Nadia directly, which is rare.
- Marcus asked on 14 Aug whether the new ranking was meant to apply to responders who have been turning jobs down. The config does not distinguish them. Wen was away until 24 Aug, and no answer is recorded. This is a possible cause of the "phone never goes off" theme, and I should confirm it before concluding anything.
- Priya's advice: do not make this a revert-4.2 conversation, because proximity was a long-requested change. Marcus planned to regroup with me after my first week. The Sept ticket breakdown (Nadia) and weekly acceptance data (Ravi) are the inputs I need.

**Q3 roadmap** (last reviewed 30 Jun, so stale; all items owned by Priya and need a new owner):
- Committed for 4.2: change to who gets pinged (shipped), ping timeout tuning (shipped as 90s to 60s, presumably), **Availability Confidence** (confidence score next to stated availability; **not in the 4.2 release notes**).
- Committed for 4.3: requisition approval chains (Supply).
- Exploring for Q4: handler phone app, shared cover between responders.
- Priya says "a couple of items got squeezed out of 4.2". Availability Confidence is the likely one. I still need a conversation with Helen about which items are still real Q3 commitments. Items on a numbered release count as locked, and changes go through Product.

**Briefs** (all one-pagers):
- Bulk Callout (Jan): shipped in 4.1 although the brief says nobody has picked it up. The brief has no baseline for time-to-full-coverage.
- Routing Override Audit Log (Mar): the 4.0 notes list an override audit log, so it probably shipped. Confirm.
- Requisition Approval Chains (Jul, Supply): the ask is a second approval step above $2,000, but the brief has accreted at least four other features. Scope needs cutting before 4.3.
- Handler Phone App (8 Sep): exploration only, unstaffed, no baseline. The Aunt Dot interview is the source.

**Other open items:**
- Write the missing description of how routing decides who gets pinged. Priya asked for this, and Wen is the source.
- Console filter-persistence tickets are noise, so don't let them take my first month.
- Priya admits she made calls faster than she checked them. Look for unexamined decisions in areas nobody has reviewed.

### How I want you to work
- Check claims against the wiki or data before treating them as fact. Flag where sources disagree, as in the examples above.
- Use names with roles on first mention. Wiki comments use roles only.
- Do not assume a hypothesis (such as seasonality) is established because several people repeat it.

### Findings from session 1 (rook-database, 29 Jun to 6 Sep 2026, and the routing code)
- The seasonal explanation does not hold. Acceptance was 75-78% every week until 4.2, then stepped down on 12 Aug itself (68% to 44% to 40% over the first days). It was 73% in the last week of data. Missed pings went from about 2% to 13-21%. Tickets went from 5-8 a week to 20-32. Callout volume dipped about 10-20% and was recovering, which is the only seasonal-looking signal.
- Four responders (Vesper, Meteor Mite, The Undertow, Farlight) fell from about 49 pings a week to 3 and were at 0% taken in the last two weeks. The other twelve now get more pings. Aggregate acceptance hides this, and no metric tracks pings per responder.
- Code reading (`00-rook/code/dispatch-routing`): a missed ping and a turn-down both cost 0.12, an acceptance earns 0.08, and scores never decay (2019 TODO). 4.2 moved the weights from 0.45/0.40/0.15 to 0.60/0.25/0.15 for proximity, acceptance and capability. My working theory is that low-ranked responders stop being asked and cannot recover. Unconfirmed, and the data cannot separate the weights from the 60s ping wait.
- Still open: Wen Li's answer to Marcus's 14 Aug question; whether scores persist across deploys; which Q3 items are still commitments (Availability Confidence missing from 4.2); the requisition brief wants a second approval step while Halloran's complaint is that approvals are too slow; no 4.3 in the Releases table.
- Drafts to Helen Achebe, Marcus Oyelaran and Wen Li were written but not sent. Next: draft notes to Nadia Hoffmann (September ticket breakdown) and Ravi Menon (confirm these numbers against the weekly report).

### Findings from session 2 (Customer interviews, support_tickets, pings re-check)
- Tickets since 12 Aug: 107, of which 83 are open. 30 are "phone never goes off" (all about The Undertow, Farlight, Halfmoon and Corporal Ashgrove) and 15 are "gone before I could answer" (11 responders), which matches Nadia's two-thirds to one-third split. All 45 are open. Vesper's and Meteor Mite's handlers filed no tickets.
- Pings re-check: Farlight, The Undertow, Vesper and Meteor Mite got 1-3 pings between 26 Aug and 6 Sep with 0 taken, confirmed. Halfmoon and Ashgrove are only mildly down. Normal volume was 10-15 pings a week, so the "49 a week" figure in session 1 cannot be reproduced and should not be quoted.
- Four interviews (2-5 Sep, run by Sofia Marino, product designer: Aunt Dot, Mr. Ambrose, Halloran, Kip) show the same two symptoms but no cause. Only Ambrose also filed a ticket (3043: his lost callout was on 12 Aug, 4.2 release day). The four handlers with the loudest quiet-phone tickets (Linda Pruitt, Desmond Okafor, Simone Fischer, Yusuf Demir) were not interviewed, and nothing says why. Ask Sofia.
- Filters: 14 tickets since 4.2, including 4 silent resets, the latest on 4 Sep, with no known cause (ask Marcus). Storage looks per-browser, not per sign-in. Worth a reset warning, but not a first-month priority.
- Halloran says maintenance scheduling has improved, but tickets 3054 and 3109 show it booking suits on marathon day. The wiki has no brief or roadmap item for a console redesign, only the interviews tagline "console redesign research".
- Session 3 (pings, tickets, callouts, routing code): The four who collapsed were pinged for every callout in their home area before 4.2, but by 24 Aug got 0 to 3 in two weeks while neighbours took 20 to 30. The neighbours (for example Falkirk, Cindermark and Bulwark for Uptown) were already the fallbacks before 4.2. That points at the acceptance score and not travel time, but travel times are not in the data (availability.py is a stub), so it is an inference.
- The four missed 4 or more pings in the first week after 4.2 (40-57% of their pings), and everyone else missed 3 or fewer. Their not-taken pings were mostly misses, other responders' were mostly turn-downs, though the code penalises both at 0.12. Break-even taken rate under my score replay is 60%; Halfmoon and Ashgrove sit at about 65%, which is why they only fell 21-24% in volume. The replay is my reconstruction and assumes scores persist across deploys.
- Pings per callout rose from 1.23 to 1.39, and callouts with no taker went from 5.5% to 11.1% (recovered to 94.5% filled in the week of 31 Aug). Missed pings rose in every area and at every time of day, so a broad cause (probably the 60s wait) sits under the four-responder collapse.
- Tickets match the pings exactly: 17 "N pings in seven days" claims and 4 "nothing since" dates are all right, and "N days" claims are the true gap rounded. All 22 quiet-phone tickets about the four are still open. The wiki Releases table has nothing after 4.2. Kip and Aunt Dot (silent handlers of Meteor Mite and Vesper) were interviewed, the four loud handlers were not.
- Still open: Wen Li's answer on whether scores persist across deploys; whether the four's availability was really set (handlers say yes, not in the data); data stops at 6-7 Sep, so I need newer data from Ravi Menon before quoting current numbers; not re-read this session: the 4.2 wiki page and comments, the "Change to who gets pinged" and "Ping timeout tuning" roadmap rows, CHANGELOG, handoff doc.
