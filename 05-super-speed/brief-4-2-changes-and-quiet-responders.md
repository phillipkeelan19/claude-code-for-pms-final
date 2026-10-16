# Rook Dispatch: the 4.2 release and responders who stopped getting work

For: senior leadership. From: PM, Rook Dispatch. Status: draft, based on data to 7 Sep.

## Summary

Since the 4.2 release on 12 Aug, Dispatch has been offering far less work to a small group of responders. Four have gone from regular callouts to almost none and have taken nothing in the last two weeks of data. Their handlers are filing tickets, and overall support volume is about three times normal. The "seasonal dip" explanation does not fit the data: acceptance fell on release day itself. The likeliest cause is how 4.2 changed the ranking of who gets asked. That is my inference, not yet confirmed by engineering. **The ask: hold off on a revert-4.2 decision for now. Proximity was a long-requested change. Let us confirm the cause this week and bring back a fix proposal.**

## Why it matters

- **Customer impact:** responders pay per active responder, and handlers depend on their people being reachable. 45 related tickets are still open, 22 of them about the four.
- **Coverage:** callouts with nobody taking them doubled, from 5.5% to 11.1%. They recovered to 94.5% filled by the week of 31 Aug.
- **Hidden risk:** overall acceptance hides the problem, and nothing tracks work offered per responder. Quiet responders can go unnoticed until a handler complains.

## What 4.2 changed

1. The ranking now favours who is closest over who has said yes recently.
2. Responders now have 60 seconds to answer a ping, down from 90.
3. Console filters now persist between sessions. This is minor.

## What happened

- Acceptance fell from about 75% to about 40% in the first days, and missed pings rose from about 2% to 13-21%.
- The four responders missed roughly half their pings in week one. Each miss lowers their ranking, and the ranking never recovers on its own, so they stopped being asked and had no way to earn their place back.
- Support tickets fall into two groups. About two thirds say "my phone never goes off" and are tied to the four. About one third say "gone before I could answer", which fits the shorter 60-second wait.

## How sure we are

- **Confirmed by data:** not seasonal; the four stopped being offered work.
- **Likely, not proven:** the new ranking plus no way to recover caused it. We cannot yet separate it from the shorter wait.
- **Unknown:** whether rankings reset at each release, and whether the four's availability was set correctly.

## Next steps

1. Staff engineer Wen Li confirms how ranking and recovery work. This is the question the engineering manager asked on 14 Aug, and it has not been answered.
2. Data analyst Ravi Menon supplies data after 7 Sep so current numbers can be quoted.
3. Product designer Sofia Marino explains why the four most vocal handlers were not interviewed.
4. I return with a fix proposal for your decision.
