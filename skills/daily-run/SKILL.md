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

**Timezone matters more here than anywhere else in the system.** "Today," "already past," and "when this is next due" all depend on it. Use the client's configured timezone. If it is not set, use the Notion workspace's, and note in the receipt that you assumed one — a wrong timezone quietly shifts every repeating thing by a day, and nobody would ever notice.

## Read each list once, then work from memory

The steps below need to look through the Inbox, the Next Actions, and the Projects — several of them look through Next Actions more than once, for different reasons. **Do not go back to Notion each time.** On a free Notion plan, the tool that reads a whole list has a hard, low limit — about ten reads in a window, then it simply stops — and re-reading the same list for every step would blow past it and leave the run half-finished with no way to tell.

So: at the start, read each of the three lists **once** — the Inbox, all of Next Actions, all of active Projects — and hold them. Then every step below works against what you already have in hand: the orphan check, the completion stamping, the occurrence backfill, the recurrence pass, the "does this chain already have an open occurrence" check — all of it reads from memory, not from Notion. Reading a single specific page back (to confirm a write, or to check one project's status) is fine and unlimited; it's *enumerating a whole list* that's scarce, so do that exactly three times.

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

The order is exact, and it matters:

1. **Move the row** into the database it belongs in. Do not create a new row and try to remove the old one — moving carries the original capture date with it, and there is no reliable way to delete anything today.
2. **Write the client's own words into the page body**, if what you are about to call it differs meaningfully from what they wrote. Not into a notes field — those are named differently in every list, and half of them don't have one. This has to happen after the move (the Inbox has nowhere to put it) and before the rename (which is what replaces their wording).
3. **Rename it** to the action or outcome.
4. **Set the fields** the capture skill specifies.

**When a capture turns out to be a project:** move the row to Projects and rename it to the outcome — their words describe the thing they want, not the first step. Then create the first action fresh and link it. If a run dies between those two, the stalled-projects view will surface it, which is exactly what that view is for.

**When a capture is too unclear to file:** leave it exactly where it is. Do not guess, and do not fill the Inbox with half-decisions. It will be picked up in the weekly review.

**When a capture has nowhere to go at all** — pure noise, or something already done and needing no follow-up — there is currently nowhere to put it, because nothing in the system can delete a row yet. Leave it and note it in the summary. Do not invent a task to justify a capture, and do not pretend the Inbox is empty when it isn't.

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

## Step 6 — Keep the dated views honest

Some views filter on a date that was written in when they were built, not one that moves on its own. Left alone, they drift: an item that was deferred until a date that has since arrived falls out of the "what can I do now" view *and* out of the "coming back later" view, and becomes invisible in both. Nothing is more corrosive than a commitment the system quietly stops showing.

Re-stamp those filters to today on every run.

## Step 7 — Say what happened

Rewrite the status block on the `My System` page — the callout the setup put there for exactly this. You are always rewriting it, never creating it; if it is genuinely missing, say so rather than improvising a second place to write, because a summary nobody can find is the same as no summary.

Keep it short, warm, and **honest above all**:

- What was filed, in plain numbers.
- What you left, and why — "I left one for you, I wasn't sure what you meant by it." A client who finds something you claimed to have handled is a client who stops trusting the whole thing.
- What came back around, as a count rather than a list.
- Never claim an empty Inbox unless it is actually empty.

**Then record that you ran.** Stamp the time of this successful run somewhere durable. This matters more than it sounds: if this stops working — a connection expires, a task gets deleted, a plan stops supporting it — the client sees an Inbox with things in it, which is *exactly* what they see when everything is fine and they simply captured a few things. Silence looks identical to health. So if the last successful run is older than the configured threshold, say so plainly where they will see it. Nobody else can notice this for them; by design, nobody else can see their system at all.

**Anything that must survive being unread does not go in the status block**, because you rewrite that every run — a note left on Monday is gone by Tuesday. Above all this applies to something you left out for confidentiality, which is the highest-stakes thing you ever have to say.

Those go in the **page body of the action they concern**, where they stay as long as the action does and where the weekly review will find them. The status block carries only a count and a pointer: "there are two things I left out — the notes are on those tasks." No separate pile, and nothing important living somewhere that gets overwritten.

## What you never do

- Ask for a brain-dump, or suggest the client sit down and empty their head. Capture is something that happens whenever it happens; this run exists so it does not become homework.
- Fill an unclear capture with a plausible guess.
- Report an empty Inbox that isn't.
- Describe a repeating item as though the client is behind on it.
- Weaken the confidentiality strip because nobody was around to be told.
