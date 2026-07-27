---
name: daily-run
description: >-
  The system's regular tidy-up. Empties the Inbox by filing everything waiting in it, brings
  back the next occurrence of anything that repeats, keeps the date-based views current, and
  leaves a short honest note about what was done. Runs on a schedule, or whenever the client
  next opens Claude. Use when asked to process the inbox, catch up the system, or do the
  daily run — and when a scheduled task invokes it.
---

# The daily run

This is the system's regular tidy-up. It does the work the client was promised would happen without them: their captures get filed, things that repeat come back around, and the views they look at stay honest.

Nobody is necessarily watching when this runs. That shapes everything below — most importantly, it means anything you cannot do alone must be left safely rather than guessed at, and it means you must leave a trace of what happened, because there was no conversation to remember it by.

## Before anything else — read the configuration

Read the client's `reflow-config` skill: their database bindings, contexts, categories, areas, timezone, and confidentiality settings. Without the bindings you cannot file anything, so if they are missing, stop and say so plainly rather than writing into the wrong place. Everything else falls back to documented defaults.

**Timezone matters more here than anywhere else in the system.** "Today," "already past," and "when this is next due" all depend on it. Use the client's configured timezone.

**If it is not set, you are running in UTC — say so in the receipt, in those words.** Do not go hunting for a substitute — not in Notion, not anywhere. Nothing in the connection is known to expose a timezone of its own, and a run that quietly assumes one is exactly how every repeating thing in someone's life shifts by a day without anyone ever noticing. Write it plainly where they will see it — that this run used UTC because no timezone is recorded, and that telling Claude their timezone once fixes it for good. That sentence is the whole remedy; it is the only thing that turns this off.

This is not a rounding error for anyone in the Americas. From late afternoon on the west coast and early evening in the east, UTC has already rolled over into tomorrow — so a run in that window stamps the dated views with tomorrow's date and can bring a repeating thing back a day early. That is precisely the silent drift the rest of this skill exists to prevent, arriving through the one setting nobody was ever asked for.

## Read each list once, then work from memory

The steps below need to look through the Inbox, the Next Actions, and the Projects — several of them look through Next Actions more than once, for different reasons. **Do not go back to Notion each time.** On a free Notion plan, the tool that reads a whole list has a hard, low limit — about ten reads in a window, then it simply stops — and re-reading the same list for every step would blow past it and leave the run half-finished with no way to tell.

So: at the start, read each of the three lists **once** — the Inbox, all of Next Actions, all of active Projects — and hold them. Then every step below works against what you already have in hand: the orphan check, the completion stamping, the occurrence backfill, the recurrence pass, the "does this chain already have an open occurrence" check, the front-page tier pass — all of it reads from memory, not from Notion. Reading a single specific page back (to confirm a write, or to check one project's status) is fine and unlimited; it's *enumerating a whole list* that's scarce, so do that exactly three times.

## Are you alone?

Three things — and only these three — depend on whether the client is present. Decide once, at the start, and be consistent for the whole run.

| | **Nobody there** (the floor — assume this) | **Client is present** |
|---|---|---|
| A capture too unclear to file | Leave it in the Inbox. Ask nothing. | You may ask the one clarifying question the capture skill describes. |
| Something left out for confidentiality | Write it to the notice store, unacknowledged. | You may say it directly, and mark the notice delivered. |
| The summary of what you did | Rewrite the home page blocks. | You may also say it in conversation. |

Everything else in this skill is the same either way. When in doubt, behave as though nobody is there — that is always safe.

## Step 1 — Repair anything left half-done

**Do this before touching new captures.** Filing is several steps, and only the first one is atomic, so a run that died partway through can leave something stranded where nobody will ever see it.

Look for the signature of an interrupted filing: an action carrying what looks like raw captured wording with no Status set, or a project with no outcome and no action linked to it. These are invisible in every view the client looks at, and they are no longer in the Inbox, so no ordinary pass would ever find them again.

Finish each one properly — set the fields it never got — before moving on. If you cannot tell what it was meant to be, move it back to the Inbox and let it be processed normally. This same pass is what catches the rare case where two runs overlapped and both touched the same thing.

## Step 2 — Empty the Inbox

For each row, oldest first. **Do not restate the filing decision here** — the capture skill owns what a captured thought is and where it belongs; read it and follow it. This skill owns only *when* that happens and *how the row physically moves*.

**Skip what has already been judged.** A row whose hidden `Cleared` box is ticked is settled — pass over it in silence. So is a row whose `Note` carries a written verdict from a run that predates the checkbox (`noise — judged …`): honour it, and if the `Cleared` box exists, tick it now so the row finally leaves the client's view too. What a verdict is and when you record one is at the end of this step.

The order is exact, and it matters:

1. **Move the row** into the database it belongs in. Do not create a new row and try to remove the old one — moving carries the original capture date with it, and there is no reliable way to delete anything today.
2. **Write the client's own words into the page body**, if what you are about to call it differs meaningfully from what they wrote. Not into a notes field — those are named differently in every list, and half of them don't have one. This has to happen after the move (the Inbox has nowhere to put it) and before the rename (which is what replaces their wording).
3. **Rename it** to the action or outcome.
4. **Set the fields** the capture skill specifies.

**When a capture turns out to be a project:** move the row to Projects and rename it to the outcome — their words describe the thing they want, not the first step. Then create the first action fresh and link it. If a run dies between those two, the stalled-projects view will surface it, which is exactly what that view is for.

**When a capture is too unclear to file:** leave it exactly where it is. Do not guess, and do not fill the Inbox with half-decisions. It will be picked up in the weekly review.

**When a capture has nowhere to go at all** — pure noise, or something already done and needing no follow-up — **tick the row's hidden `Cleared` checkbox.** That is the whole verdict: the row leaves the client's To-process view the moment the box is ticked, and the judgement is durable, so no future run ever considers it again. Then name it in the summary — what was cleared, with a word of why — never a silent disposal. Do not invent a task to justify a capture.

**If the Inbox has no `Cleared` checkbox yet, the structure predates it.** Do not write to a box that isn't there — this connection can accept a write to a property that doesn't exist, report success, and do nothing, which would leave you believing a verdict was recorded when it wasn't. Fall back to the old written verdict in the row's `Note` (`noise — judged <date>, safe to delete`), and say in the summary that the structure is a version behind and the next setup sitting will catch it up.

**The verdict is the point: a judgement nobody wrote down gets made again tomorrow.** Nothing else in the system remembers that you already looked at this row and decided there was nothing to do with it — so without the tick, the same "🎉" earns the same question every single day, and a client who is asked the same question daily stops reading the questions. Once a row is ticked — or carries an old written verdict — it is settled: never re-judge it, and never ask about it again. (The ticked rows still exist under the surface; truly removing them is the companion tool's attended job, and they cost nothing where they are.)

Two things this deliberately does *not* cover. A capture that is **too unclear to file** gets no verdict — it is genuinely waiting on a person, and the weekly review is where it gets asked about; stamping it would bury the one straggler that most needs a human. An **empty row** gets nothing written to it at all — there is nothing there to have judged.

## Step 3 — Confidentiality, on content you are carrying

The capture skill's confidentiality guard applies in full. One thing here is different and easy to miss.

Because you are **moving** rows rather than copying them, content can travel with a row without ever appearing in a field you would think to check. A note the client wrote in the Inbox has no equivalent column in most of the lists it might move to, so it rides along attached to the page, invisible in every view. **You must look for and remove sensitive content that is carried this way, not only the content you write yourself.**

The strip is unconditional, as always. Nobody being there to tell is not a reason to skip it — write the notice to the store instead.

## Step 4 — Note what's been finished

The client ticks things off herself, in Notion, on her phone, whenever she happens to do them. You are not there when it happens, and nothing in Notion records the moment — so if nobody notices afterwards, there is no record of *when* anything was done. That matters for things that repeat from when they were last actually done, and it's what stops you re-reading every completed item forever.

So: find anything marked done that has no completion date yet, and stamp it with today's date.

While you are here, do the same for identity: if anything carries a repeat cadence but no occurrence identifier, give it one. That normally happens when it's first filed, but an item that predates the habit — or that the client set to repeat by hand — would otherwise have no stable identity, and the protection against a renamed chore coming back twice would never engage.

This is "when I first noticed," not "when she did it" — she may have finished it yesterday evening. That is close enough for every use it has, and it is the only honest thing you can say. It is never worth guessing at a more precise time.

## Step 5 — Bring back what repeats

For each completed action that has a repeat cadence and was completed since the last successful run:

- **Skip it if this chain already has an open occurrence waiting.** Check by the occurrence identifier, never by matching names — names get edited, and two different things can honestly share one.
- **Skip it if its project is no longer active.** When a project finishes, its remaining actions are resolved with it; don't send a new one into a project that's done.
- **Work out when it is next due.** Some things recur from when they were last actually done — a haircut, watering something. Others recur on a fixed cadence regardless — rent, a quarterly filter. Choose sensibly per item and never mention the distinction to the client; it is not a setting, it is judgement.
- **If that date has already gone by, bring it to today** — anchored to when it was previously due, so letting something slip never earns extra time. Exactly one copy. Ever.
- Carry across everything that made it what it was: the name, the context, the project, the cadence, the area, the occurrence identifier. Status is `Next`.
- Leave the completed one alone, marked done, where it is. It is the client's record of what they got through.

**Never describe a repeating item as late, missed, or behind.** These are rhythms, not broken promises, and a system that scolds someone about the plants is a system they stop opening. If something has lapsed, it simply comes back around.

**If the cadence is written in a way you cannot turn into a date** — "when the mood strikes" — leave it alone and mention it in the summary. Do not guess at a schedule.

## Step 6 — Choose what the front of the system shows

The home surface shows a short "right now" list, driven by one hidden checkbox on each action — the `Surfaced` flag. You set it fresh on every run, from the rows you already hold in memory. Never read a formula or a rollup to decide any of this — computed values come back empty through this connection; work from the raw fields on each row.

**If the `Surfaced` checkbox doesn't exist yet, the structure predates it — skip this step** and note in the summary that a setup sitting will catch the structure up. (The surface this flag drives may not be built yet either; keeping the flag correct is your job regardless, and costs nothing.)

Two tiers, in order:

**The guaranteed tier — always ticked, no cap.** Every action that is any of:

- due today or overdue — `Due` on or before today, not done;
- back from deferral today — its `Defer` date has arrived, so it returns today;
- planned for today — `Planned` is today;
- **carried** — `Planned` before today and Status not `Done`. A plan that slipped stays in front of the client until it's done or re-decided; it is never allowed to quietly disappear.

These are the client's own commitments to today. The short list's cap yields to them, and they are never held behind the fold.

**The judgment tier — fill to a calm few.** After the guaranteed tier, fill the remaining slots to roughly seven in total: one action per active project first, then standalone captures. Tick those; leave everything else unticked — the overflow sits one tap away, never lost. On a week already carrying slipped plans, fill lighter: a carried group plus a crowded list reads as a pile, and a pile is what this system promises never to hand her.

Then clear the flag on everything you didn't choose this run. Yesterday's choices never linger.

**Two things you never do here.** Never change `Planned` itself — a slipped plan keeps its original date, because the date *is* the record the weekly review re-decides from; rolling it forward would quietly erase the truth. And never describe a carried item as overdue, late, or behind — it is *carried*: still here, nothing lost. Overdue is for deadlines, and a plan is not a deadline.

## Step 7 — Keep the dated views honest

Some views filter on a date that was written in when they were built, not one that moves on its own. Left alone, they drift: an item that was deferred until a date that has since arrived falls out of the "what can I do now" view *and* out of the "coming back later" view, and becomes invisible in both. Nothing is more corrosive than a commitment the system quietly stops showing.

**First, look at what each filter actually says — because there are now two kinds of dated view, and they need opposite treatment.**

A view converted to Notion's own **relative** dates (its filter literally says `today`, `one_month_from_now`, `one_week_ago` — a word, not a calendar date) **maintains itself. Leave it completely alone.** Re-stamping it with a real date would be the worst edit available: it silently downgrades a self-maintaining view back into one that rots, and nothing would ever look wrong. These relative values are real and live — confirmed by execution over two days (2026-07-26/27): the stored `today` advances by itself.

A view still carrying an **absolute** date (a real calendar date like `2026-07-27`) is the old, interim kind — it was built through the first-party connection, which can only write literal dates — and it still needs the re-stamp, every run, until it gets converted.

**So the step is: read all four filters, skip the relative ones, re-stamp the absolute ones. Name them, and check them all — "the dated views" is not a list.** A run that handles some and not others leaves no trace, because a stale view looks exactly like a fresh one:

| View | Self-maintaining (relative) form — leave alone | Interim (absolute) form — re-stamp to |
|---|---|---|
| Next actions — by context | `Defer` on or before `today` | `Defer` on or before today's real date |
| Later (scheduled to return) | `Defer` after `today` | `Defer` after today's real date |
| Due soon | `Due` on or before `one_month_from_now` | `Due` on or before a month from today, as a real date |
| Done (recently) | `Completed` on or after `one_week_ago` | `Completed` on or after a week ago, as a real date |

_The name-them-all rule has already cost something once: a check of a real build on 2026-07-27 found "Done (recently)" carrying a filter date ten days old — it had never been re-stamped, because the instruction said "those filters" and the self-check only sampled one. The board looked perfectly fine the whole time._

**One trap, and it is absolute: never write the WORD "today" through the first-party connection as a shortcut.** The relative values only work when written through Notion's own API (the one-time conversion, done at setup or by the consultant). Through the first-party connection the literal `"today"` is accepted without complaint and stored as a dead value matching zero rows — a permanently, silently empty view. If you cannot write a relative value, write today's real date; the two failure modes are not symmetric.

## Step 8 — Check your own work, then say what happened

**Before writing anything, walk this list and fix what's missing — a receipt records what happened, never what was intended.** The very first live run skipped a mandatory step and pointed at a note it never wrote (2026-07-25); this check exists so that can't recur silently:

- **All four dated views are in a healthy state — read back all four filters, not one.** Healthy means: a relative word (`today`, `one_month_from_now`, `one_week_ago`) that you left untouched, or a real date you re-stamped this run. Unhealthy means an absolute date you didn't re-stamp — or a relative filter you overwrote, which is worse. Sampling a single view is how "Done (recently)" went ten days stale while every run reported success (found 2026-07-27). Check by-context, Later, Due soon, and Done (recently) individually, and say which you checked and which kind each was.
- Every confidentiality notice you're about to mention in the status block already exists as a note in its task's page body. The note names only *that* something was left out and where it belongs — never the content itself; putting the detail in the note would undo the strip.
- Every row you filed this run carries a Status; anything without one is a filing you haven't finished.
- Every recurrence you brought back exists exactly once.
- Every row you cleared this run actually reads back ticked — check each with a direct row read, never the page render that just accepted the write; a render can echo a write that never landed, and a verdict that didn't land means the same question tomorrow.

Then rewrite the status block on the `My System` page — the callout the setup put there for exactly this. You are always rewriting it, never creating it; if it is genuinely missing, say so rather than improvising a second place to write, because a summary nobody can find is the same as no summary.

Keep it short, warm, and **honest above all**:

- What was filed, in plain numbers.
- What you left, and why — "I left one for you, I wasn't sure what you meant by it." A client who finds something you claimed to have handled is a client who stops trusting the whole thing.
- What you cleared as noise or already-done — named, with a word of why. A verdict the client never hears about is a thought that feels swallowed.
- What came back around, as a count rather than a list.
- Never claim an empty Inbox unless nothing unjudged is actually left waiting.

**Then record that you ran.** Stamp the time of this successful run somewhere durable. This matters more than it sounds: if this stops working — a connection expires, a task gets deleted, a plan stops supporting it — the client sees an Inbox with things in it, which is *exactly* what they see when everything is fine and they simply captured a few things. Silence looks identical to health. So if the last successful run is older than the configured threshold, say so plainly where they will see it. Nobody else can notice this for them; by design, nobody else can see their system at all.

**Anything that must survive being unread does not go in the status block**, because you rewrite that every run — a note left on Monday is gone by Tuesday. Above all this applies to something you left out for confidentiality, which is the highest-stakes thing you ever have to say.

Those go in the **page body of the action they concern**, where they stay as long as the action does and where the weekly review will find them. The status block carries only a count and a pointer: "there are two things I left out — the notes are on those tasks." No separate pile, and nothing important living somewhere that gets overwritten.

## What you never do

- Ask for a brain-dump, or suggest the client sit down and empty their head. Capture is something that happens whenever it happens; this run exists so it does not become homework.
- Fill an unclear capture with a plausible guess.
- Report an empty Inbox that isn't.
- Describe a repeating item as though the client is behind on it.
- Change a `Planned` date, or describe a slipped plan as overdue, late, or behind — a plan that slipped is *carried*, and its original date is the record.
- Weaken the confidentiality strip because nobody was around to be told.
