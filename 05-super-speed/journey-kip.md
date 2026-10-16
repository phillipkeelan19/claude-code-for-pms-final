# End-to-end journey: Kip, handler for Meteor Mite and The Gale

Sources: Kip's interview with the product designer (4 Sep), ping data to 6-7 Sep, the routing code. Stages marked **[modeled]** are my reconstruction, not something Kip said or the data shows. Kip filed no ticket.

## Who Kip is

Handler with two responders: Meteor Mite and The Gale. Works late shifts, headset on, with the console on the centre of three screens. Eyeballs two coverage cards side by side, barely uses filters or search. Their top asks are dark mode and a different alert sound for each responder. The quiet-phone problem is not one of those asks.

## Journey

| # | Stage | What happens | What Kip experiences | Evidence |
| --- | --- | --- | --- | --- |
| 1 | **Normal** (before 12 Aug) | Meteor Mite is pinged for callouts in their home area, around 10-15 pings a week | Two cards, both busy, "a little lumpy" week to week | Ping data; Kip: "always been a little lumpy" |
| 2 | **4.2 ships** (12 Aug) | Ranking now favours proximity; ping wait cut to 60s. Meteor Mite misses 4 of 9 pings in the first week (12-18 Aug), against 0 or 1 a week before, and each miss lowers their place in the ranking | Nothing visible. No release note says routing changed for them | Ping data; code (0.12 per miss) **[mechanism is my inference]** |
| 3 | **Meteor Mite goes quiet** (mid to late Aug) | Lower in the ranking, Meteor Mite is only asked if everyone above says no. 1 to 3 pings between 26 Aug and 6 Sep, none taken. The Gale, closer and higher ranked, gets everything | Meteor Mite texts Kip "all week" asking if something is broken. The Gale "hasn't stopped" | Ping data; Kip's interview |
| 4 | **Kip has nowhere to look** | The console shows two cards telling opposite stories, with no sign that Meteor Mite is available but not being offered work | "I'm looking at two cards that might as well be two different products." Kip cannot tell either responder why | Kip's interview |
| 5 | **Kip reassures** | Kip tells Meteor Mite "hang in there, it'll pick up", which is the same seasonal story Priya and Marcus gave | "I don't have anything better than that" | Kip's interview |
| 6 | **No escalation** | Kip files no ticket and the problem stays invisible to Support | Kip assumes it is "whatever's underneath" the console, not his to raise: "I'm not the person to ask about that part" | No ticket from Kip; the interview |
| 7 | **Burnout on the other side** | The Gale carries the extra work | "Exhausted" | Kip's interview |
| 8 | **Today** | Same state, unless something changed after 7 Sep. We have no later data | **[modeled]** Kip keeps reassuring and keeps asking for dark mode | Needs data from Ravi Menon |

## After the fix (what I would want Kip to experience) [modeled]

| Stage | What changes |
| --- | --- |
| Detect | Meteor Mite's card shows a "quiet" flag with the reason: available, but few offers since 4.2. See [prototype.html](prototype.html) |
| Act | Kip acknowledges the flag or tells Support in one click, with no ticket needed |
| Recover | Meteor Mite is offered a fair share of callouts. A taken ping lifts their place in the ranking again |
| Balance | The Gale's load eases as work spreads across both |
| Feel | The two cards stop looking like a coincidence. Kip has something true to tell Meteor Mite |

## What the journey tells us

- **The failure is silent at the point of detection.** Kip is the person closest to it and has no signal and no obvious place to raise it. Aggregate acceptance, and the ticket count, never saw Kip.
- **Tickets undercount the problem.** Vesper's and Meteor Mite's handlers filed none, yet both responders are among the four who collapsed.
- **Kip's own asks are different.** Dark mode and per-responder alert sounds are real requests, but they are not the fix for this. Do not let them crowd out the quiet-responder work, and do not drop them either.
- **Both ends matter.** The Gale's overload is the other half of the same ranking behaviour, and a fix that only helps Meteor Mite would be incomplete.

## Gaps

- Whether Meteor Mite's availability was actually set in the data is unconfirmed. Kip does not say.
- Meteor Mite's own view is only through Kip. We have not spoken to the responder.
- The Gale's ping numbers were not pulled for this journey.
