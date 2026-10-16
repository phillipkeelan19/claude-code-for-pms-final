# Product brief: Quiet responder recovery (Rook Dispatch)

Author: PM, Rook Dispatch. For: Helen Achebe, Director of Product. Status: draft for review, nothing built.

## The problem in one paragraph

Since 4.2 (12 Aug), four responders (Vesper, Meteor Mite, The Undertow, Farlight) have gone from regular callouts to 0 to 3 pings in two weeks, with 0 taken. Their handlers report "phone never goes off". 22 such tickets are open. The code explains how it can happen: a missed ping or a turn-down costs 0.12, a taken ping earns 0.08, scores never decay, and offers stop at the first yes. A responder ranked low is only asked if everyone above says no, so they get no chance to earn points back. 4.2 raised the proximity weight and cut the ping wait to 60s, which pushed some responders below that line. Nobody is told this is happening, and no metric tracks pings per responder.

**Caveats:** this is my reading of the code and data, not confirmed by Wen Li. Open items: whether scores persist across deploys, whether the four's availability was truly set, and how much of the drop is the 60s wait versus the weights. Data stops at 6-7 Sep, so current numbers need Ravi Menon.

## 1. Who this is for

- **Primary: responders who have gone quiet** (today: the four above, and mildly Halfmoon and Corporal Ashgrove). They are available, but stop being offered work, and nothing tells them why. After this ships they get a fair chance to be asked again.
- **Primary: handlers of those responders** (for example Kip, Aunt Dot, Linda Pruitt, Desmond Okafor, Simone Fischer, Yusuf Demir). They find out their responder is quiet because phones stay silent and tickets get filed. After this ships they see it in the console first, with a reason.
- **Secondary: Nadia Hoffmann (support lead).** She stops absorbing "phone never goes off" tickets as a mystery.
- **Secondary: Helen and the team.** There is a metric for the problem we could not see.
- **Not for:** responders who are healthy in the ranking. Their experience should not change visibly.

## 2. What changes once it ships

For a **responder who has gone quiet**:
- They are offered a share of callouts again, even when ranked low, so a taken ping can lift them back up. Recovery no longer depends on everyone above them declining.
- In the phone app they can see their own status ("you've had few callouts lately") rather than silence.

For a **handler**:
- The console flags a responder who is available but has had far fewer pings than their usual level. It shows when the drop began and the likely reason.
- The flag appears before a support ticket is needed.

For **Product and Support**:
- A weekly "pings per responder" view sits next to acceptance rate, so aggregate acceptance cannot hide a collapse again.
- Success measures, to be baselined with Ravi:
  - The four recover to a normal pings-per-week range (normal volume was about 10 to 15 a week; the "49 a week" figure from session 1 is not reproducible).
  - The 22 open quiet-phone tickets close and new ones fall to the pre-4.2 level (5 to 8 tickets a week in total).
  - Acceptance rate and the share of callouts with no taker (11.1% after 4.2, versus 5.5% before) do not get worse.

Open design questions for Sofia Marino and Wen Li: how often a low-ranked responder is offered a ping, and whether the offer is flagged as lower priority. These are my guesses and need Wen's input before any build.

## 3. What it does not do

- **It does not fix the 60s ping wait.** That drives the "gone before I could answer" theme (about one third of tickets) and is a separate decision. Missed pings rose in every area, so it likely sits under this problem too.
- **It does not revert 4.2 or undo the proximity weighting.** Proximity was a long-requested change.
- **It is not a handler-controlled setting, and handlers cannot override or pin rankings.** Routing config ships in the release, not at runtime.
- **It does not treat missed and turned-down pings as the same thing yet.** Whether they should cost the same (both 0.12 today) is a separate question for Wen.
- **It does not guarantee a quiet responder gets work.** If there is a genuine coverage gap or the responder is unavailable, nothing changes.
- **It does not store or infer identities.** Only capability tags, availability and callout history are used (Security Policy 4.1).
- **It does not cover mutual aid, Availability Confidence, the handler phone app or the filter-persistence bug.**
- **It does not change Supply directly.** I still need to check whether any change to availability or scoring flows into the Responder Availability Record and maintenance scheduling (tickets 3054 and 3109 are unverified).
- **It is not the "small fix this afternoon".** Changing a number would restore pings but not the visibility or the metric. Helen asked for the full picture first.

## Before anyone builds

1. Wen Li confirms the mechanism, score persistence across deploys, and whether miss versus turn-down was ever discussed.
2. Ravi Menon supplies current pings-per-responder data.
3. Sofia Marino sketches the handler flag and the responder's status view (clickable prototype is the next step).
4. Marcus Oyelaran is told, per the note in config.py.
