# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

Are there any engineering comments in the codebase worth evaluating further

### 2.

Marcus Oyelaran asked on 14 Aug whether the new ranking was meant to apply to responders who’d been turning jobs down. No answer is recorded, so it’s unclear whether he was told about the 4.2 changes or reviewed them. How is the code programmed?

### 3.

so a no reposnse gets the same penaltiy as a decline

### 4.

Find me the part of this code that takes points off somebody when they miss a ping or turn one down. Show it to me and explain it in plain English. Then find me every single thing in this code that puts points back on.

### 5.

A responder who has 0 would have to do what to get back to 0.5, walk me through it step by step
