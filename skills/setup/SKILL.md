---
name: setup
description: >-
  Build the client's system in their own Notion — the five lists, the views, the weekly
  review page, and the plumbing that holds it together. Safe to run more than once: it
  adopts and repairs whatever it finds rather than making a second copy. Use when setting up
  a new client, when the structure needs bringing up to date after a change, or when
  something in the system looks broken and needs checking over.
---

# Setting up the system

This builds the thing every other skill writes into. It runs with the client there — it needs their permission before it starts, and it can't be done while nobody's watching.

**The exact structure to build is the Build specification, bundled alongside this skill as `build-specification.md` (in this skill's own folder inside the plugin).** Read it before touching anything. Names, property types, option sets, the two formulas written out literally, all ten views with their filters and sorts, and which fields to hide. Follow it exactly. This skill describes *how to build safely*; that describes *what to build*. Where they seem to disagree, the specification wins — and say so rather than quietly picking one. **If you cannot find or read that file, stop and say so — never build from memory of what the structure probably is.** A plausible-looking build from memory is the worst outcome available: it can't be deleted, and every difference from the real specification becomes permanent.

## The thing to understand before you start

**Check before you create, always.** Never assume you are starting from nothing. Re-running this is meant to be safe and boring — it should find its own previous work and leave it alone. If re-running would produce a second copy of anything, you have got it wrong.

That is good practice under any circumstances; nobody wants a workspace with two lists called "Next Actions" and no way to tell which is real. But right now it carries extra weight, because **cleaning up afterwards is not currently possible.** The connection to Notion has no way to delete a database, a field, or a row — so today, a mistake is permanent furniture in someone's workspace.

**That is a gap in the connection, not a limit of Notion**, and it is being closed: a companion tool is planned that will restore deleting. Where this skill tells you to stop rather than risk something, or to leave something in place and explain it, that is a *temporary* accommodation and is marked as such. The careful checking stays either way. The dead ends go away.

## Step 1 — Ask before you touch anything

Confirm you can reach Notion. Then find where you would build: the page named in the client's settings, or `My System`, or one you would create.

**Say the full name of that page and where it sits, and wait for a clear yes.**

This is the only moment in the whole build that can be taken back. If the connection granted access to the wrong place — an easy thing to get wrong while clicking through setup — everything after this permanently scatters five databases through something that matters. Thirty seconds of confirmation buys back the only irreversible decision here.

If they say no, stop. Don't hunt for a better page on your own.

## Step 2 — Find what's already there

Look for previous work, in this order:

1. **The recorded addresses in their settings.** If earlier work saved them, use them. This is durable — it survives someone renaming things.
2. **Failing that, look by name** under the target page. Exact match, and *only* under that page — never search the whole workspace, or an unrelated database called "Projects" somewhere else in their life gets adopted into this system.

**If you can't complete this search — you've run out of the plan's allowance for reading, or something errors — stop and say so.** Do not build on a partial look. This search is the only thing standing between a second run and a permanent duplicate, so when it can't be trusted, nothing after it can be either.

## Step 3 — The five lists

**Inbox**, **Next Actions**, **Projects**, **Someday / Maybe**, and **Reference**. (Note the spaces around the slash — that's part of the name, and names are matched exactly.)

For each, create it or adopt what's there, then bring its fields to match the specification. Don't work from memory of what the fields are — read them, every time. There are thirty-one across the five lists and several are easy to get subtly wrong.

- **Adding a missing field is safe.** Do it, and mention it.
- **A field of the wrong type is not.** Notion will often accept the change and lose data doing it, and field structure isn't covered by page history — so there's no getting it back. **Stop, and say plainly what's wrong.** Never convert it and hope.

  Then offer the way out. *Today:* you can open Notion directly in the browser and remove the field by hand, which you can do even though the connection can't. *Once the companion delete tool exists:* remove it directly and carry on with the build, no interruption. Either way this stops being a dead end — the client is never left holding a system that can't be finished.

The near-certain instance of this: Notion's own default for anything task-shaped is its special **Status** field type, while this system uses a plain **Select** called Status. A database the client made themselves, or a half-finished earlier attempt, will hit this immediately.

## Step 4 — The plumbing chain

Five things, in this order, each impossible before the one before it:

> the link between Next Actions and Projects → the `Next?` formula → the rollup that sums it → the `Stalled` formula that reads the rollup → the view that filters `Stalled`

Build them in that order. Out of order, the errors look like the connection is broken rather than like a sequencing mistake, and you will waste the client's time looking in the wrong place.

**Existing is not the same as correct, and this is where that bites.** Check how each one is actually configured, not just that something with the right name is present:

- **The link must have both sides** — `Project` on Next Actions *and* `Actions` on Projects. A half-made link looks fine from one side and the rollup can't be built at all. A previous partial run can leave exactly this.
- **The rollup must sum `Next?`** — not count everything. A rollup with the right name and the wrong sum makes the stalled view lie.
- **`Stalled` must return text.** If it returns a checkbox, everything still *looks* built — but the view filtering for the word "STALLED" will match nothing, ever. And a stalled-projects view with nothing in it is exactly what a perfectly healthy system looks like. This is the single easiest way to hand someone a broken system they'd never know was broken.

If a run stopped partway through this chain, pick up from the first link that's missing.

## Step 5 — The views and the review page

Build the ten views to specification — type, filter, grouping, sort — and hide the plumbing fields in every one of them. The client should never see a column called `Stalled`.

Notion creates a default view with every new database and it can't be removed. **Rename and reuse it as that database's first view** rather than building alongside it and leaving something unnamed behind forever.

Dates in filters are written in as real, exact dates, because there's no way to say "today" that keeps up on its own. That's expected — the daily run re-stamps them. Set them to today's actual date as you build.

**Never write the literal word "today" into a date filter.** It looks like it should work, and the connection *accepts* it without complaint — but it stores a dead value that matches nothing, so the view comes back permanently empty and nothing tells you it broke. This was confirmed the hard way. Always compute today's real date and write that exact date; a filter with "today" in it is a silently broken view, which is worse than an obvious error.

Then the review page: the eight linked views, in the order the weekly walk goes.

## Step 6 — The status block

Put a callout near the top of `My System` with placeholder text. The daily run rewrites it every time; it needs it to already exist.

It's a small thing that does something nothing else does: it says when the system last ran. If the daily run ever quietly stops, the client sees items sitting in her Inbox — which is exactly what she sees when everything is fine and she's just captured a few things. Nothing else would ever tell her, and nobody else can look at her system to notice for her.

## Step 7 — Prove it actually works

You can't read the rollup's value back — the connection doesn't expose it. So the only real proof is watching the stalled view change.

Make a test project and one test action linked to it. Then walk the action through three states, checking the stalled view each time:

| Action's status | Stalled view should show the project |
|---|---|
| `Next` | no — it has a live next step |
| `Waiting` | no — it *still* has a next step, just a blocked one |
| `Done` | **yes** — nothing live is left |

The middle one is the one people skip, and it's the one that catches a real fault: if `Next?` counted waiting items as live, a project that's completely blocked would never show as stalled, and the client would never be told about the thing most worth telling her.

Also check the main "what can I do now" view, since its filter is the fiddliest in the system: give a test action a deferred date in the future and confirm it stays out of sight.

**Leave both test rows with no completion date.** That keeps them out of "what got done," which is where the weekly review opens — nobody's first review should start with two rows called "test." Name them so their purpose is obvious, and mention them at handover so they're never a small mystery.

On a re-run, reuse the same two test rows rather than making more. *Once the companion delete tool exists, simply remove them when the check passes* — the whole business of retiring them gracefully is a workaround for not being able to tidy up.

## Step 8 — Write down where everything is

Record each list's address in the client's settings **as you create it**, not in one batch at the end. A build that gets interrupted near the end would otherwise leave a complete system with no record of itself, and the next run would have to fall back to guessing by name — at exactly the moment when getting it wrong is most expensive.

Record the page you built under, and stamp the structure's version so a later run can tell what predates a change.

**Their settings file is theirs. Read what's there and change only the addresses.** Their contexts, their timezone, how they answered about confidential records, how they like being spoken to — all of that lives in the same place, and replacing the file wholesale would wipe it. That would be this system doing exactly the thing it promises never to do.

## Step 9 — Tell them what you did

Plainly, and in their terms — five lists, a review page, and the wiring that keeps projects from going quiet. Not a schema.

Say three things that would otherwise become small mysteries:

- The two test rows, and that they can stay.
- Anything you repaired or couldn't, especially a field you had to stop on.
- That Notion's own starter pages are still sitting there. Every new Notion workspace comes with them and there's no way to start without them. Offer to clear them out — through the browser today, directly once the companion delete tool exists.

## What you never do

- Build before they've said yes to the page.
- Create anything without checking whether it already exists.
- Convert a field to a different type.
- Carry on after a search you couldn't finish.
- Replace their settings file rather than editing part of it.
- Report the system as built when a link in the chain is missing — a half-built system is worse than an unbuilt one, because it looks finished.
