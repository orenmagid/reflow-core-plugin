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

**The exact structure to build is the Build specification, bundled alongside this skill as `build-specification.md` (in this skill's own folder inside the plugin).** Read it before touching anything. Names, property types, option sets, the two formulas written out literally, all fifteen views with their filters and sorts, and which fields to hide. Follow it exactly. This skill describes *how to build safely*; that describes *what to build*. Where they seem to disagree, the specification wins — and say so rather than quietly picking one. **If you cannot find or read that file, stop and say so — never build from memory of what the structure probably is.** A plausible-looking build from memory is the worst outcome available: it can't be deleted, and every difference from the real specification becomes permanent.

## The thing to understand before you start

**Check before you create, always.** Never assume you are starting from nothing. Re-running this is meant to be safe and boring — it should find its own previous work and leave it alone. If re-running would produce a second copy of anything, you have got it wrong.

That is good practice under any circumstances; nobody wants a workspace with two lists called "Actions" and no way to tell which is real. And check-before-create still carries real weight, because cleanup is uneven — corrected 2026-07-27, since an earlier version of this paragraph said nothing could ever be deleted and that is wrong in two of three cases:

- **A field CAN be removed** (drop the column — executed and verified, including on a column holding data). **But dropping a column destroys whatever data is in it**, so removal is never free — and removing a column that a formula or view filter depends on is untested territory. Treat field removal as a repair tool, not an undo button.
- **A whole database CAN be archived** (executed and verified) — a duplicate from a failed build is recoverable, not permanent.
- **A single row still cannot be deleted or trashed through the connection you build with** — a gap in the connection, not a limit of Notion, and the reason stray rows are named honestly rather than hidden.

**The row gap now has a real answer for attended work: the companion delete tool exists.** It is a separate, local connection (named `notion-extender-local`) running on the client's own computer, so it answers only while their desktop app is open — and only where it has been installed for this client at all. Check for it once per sitting, never carrying the answer over from a previous one, and know its one deliberate boundary: it refuses to touch anything outside the system it was installed for. Where it is reachable, a stray row stops being permanent; where it is not, the honest accommodations below stand exactly as written, and its absence is a normal state, never an error. The careful checking stays either way.

## ★ What she did herself is not drift — adopt it, never prune it

**The specification says what must be *present*. It never says what must be *absent*.** She may open Notion and change things — add a context, add an area, start a list, rename something, add a column, make a whole new database. That is her workspace and she is allowed. **Nothing you find that you did not create is a fault, and none of it is yours to remove.**

Concretely, when the structure has more than the specification asks for:

- **Extra options on a select** — a seventh area, a sixth context, a fifth list. **Keep every one of them.** When you re-assert an option set (which is how a new option gets added), you must include the ones already there or they are destroyed and every row holding them goes blank. Read the current options first, keep them all, append what is missing. Never write an option set from the specification alone.
- **Extra views, extra list values, extra rows** — leave them. A client with more lists than shipped is a client using the product properly.
- **Extra properties** — leave them. A column you did not create may be holding something she cares about, and dropping it destroys the data.
- **A renamed database** — the address recorded in her settings is what you match on, so a rename does not lose it. Update the recorded name and move on; do not rename it back.
- **A property whose *type* is wrong for the specification** — this is the one case that genuinely blocks the build, and it has its own handling further down. Stop and offer the two doors; never silently recreate it.

**Say what you found, out loud, in the summary.** "You've added a `@Office` context and a `Records` list since I was last here — I've left both alone and the system knows about them now." Silence here reads as either not noticing or not caring, and both cost trust.

⚠ **One honest limit to state plainly rather than paper over: a database she builds outside the five is not adopted, maintained, or watched.** The system finds its own work by recorded address, and hers has no address in it. Nothing is damaged and nothing is lost — Claude will help with it whenever she asks — but no run will tend it on its own, and she should be told that rather than left to discover it. _(Tracked as an open design question: act:f499cfa9.)_

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

**While you are in their settings, look at the timezone — and ask for it only if nobody has.** If it still holds the shipped placeholder or is blank, ask one short question now and write the answer in as Step 9 describes. **If it already holds a real value, do not ask and do not touch it.**

It has to happen here, and it has to happen with them. A few steps from now this build stamps real calendar dates into view filters, so getting the day wrong seeds the drift on the very first day. And this is the only moment in the system's whole life when a person is reliably present to answer — every run after this one happens with nobody there. A system whose timezone was never collected runs in UTC forever: from late afternoon on the west coast and early evening in the east, it already thinks it is tomorrow, so dated views get stamped a day ahead and repeating things come back early. Nobody would ever trace that back to a setting nobody asked about.

## Step 3 — The five lists

**Inbox**, **Actions**, **Projects**, **Lists**, and **Reference**. (Note the spaces around the slash — that's part of the name, and names are matched exactly.)

For each, create it or adopt what's there, then bring its fields to match the specification. Don't work from memory of what the fields are — read them, every time. There are thirty-eight across the five lists and several are easy to get subtly wrong.

- **Adding a missing field is safe.** Do it, and mention it.
- **A field of the wrong type is not.** Notion will often accept the change and lose data doing it, and field structure isn't covered by page history — so there's no getting it back. **Stop, and say plainly what's wrong.** Never convert it and hope.

  Then offer the way out: the wrong-typed column has to go, and there are two doors. The connection itself can now drop a column — but dropping a column destroys whatever data it holds, so that is the client's call after hearing exactly that; and on a build whose plumbing already exists, be doubly careful, because dropping a column a formula or view depends on is untested territory. Or they can open Notion in the browser and remove it by hand. (This is not the companion delete tool's job — that tool removes rows, never fields.) Either way this stops being a dead end — the client is never left holding a system that can't be finished.

The near-certain instance of this: Notion's own default for anything task-shaped is its special **Status** field type, while this system uses a plain **Select** called Status. A database the client made themselves, or a half-finished earlier attempt, will hit this immediately.

## Step 4 — The plumbing chain

Five things, in this order, each impossible before the one before it:

> the link between Actions and Projects → the `Next?` formula → the rollup that sums it → the `Stalled` formula that reads the rollup → the view that filters `Stalled`

Build them in that order. Out of order, the errors look like the connection is broken rather than like a sequencing mistake, and you will waste the client's time looking in the wrong place.

**Existing is not the same as correct, and this is where that bites.** Check how each one is actually configured, not just that something with the right name is present:

- **The link must have both sides** — `Project` on Actions *and* `Steps` on Projects. A half-made link looks fine from one side and the rollup can't be built at all. A previous partial run can leave exactly this.
- **The rollup must sum `Next?`** — not count everything. A rollup with the right name and the wrong sum makes the stalled view lie.
- **`Stalled` must return text.** If it returns a checkbox, everything still *looks* built — but the view filtering for the word "STALLED" will match nothing, ever. And a stalled-projects view with nothing in it is exactly what a perfectly healthy system looks like. This is the single easiest way to hand someone a broken system they'd never know was broken.

If a run stopped partway through this chain, pick up from the first link that's missing.

## Step 5 — The views and the review page

Build the fifteen views to specification — type, filter, grouping, sort, and **exactly the visible columns the specification's Presentation section names for each view, title first**. The client should never see a column called `Stalled`, nor the rollup's raw number, nor a table that leads with anything but the row's name.

Notion creates a default view with every new database and it can't be removed. **Rename and reuse it as that database's first view** rather than building alongside it and leaving something unnamed behind forever.

Dates in filters are written in as real, exact dates, because **the connection you are building through** has no way to say "today" that keeps up on its own. That's expected — the daily run re-stamps them. Set them to today's actual date as you build.

_(Notion itself can do relative dates; the tools you have here cannot. Don't record this as something Notion can't do — it is a limit of this connection only. After the build, a **one-time conversion** — a small script the consultant runs against Notion's own API — upgrades all four dated filters to genuinely self-maintaining relative values (`today`, `one_month_from_now`, `one_week_ago`), and from then on the daily run detects them and leaves them alone. The exact dates you write here are scaffolding for the gap between build and conversion, not the permanent state. And if a build you are ADOPTING already shows a relative word in a date filter, it has been converted — leave that filter exactly as it is.)_

**Never write the literal word "today" into a date filter.** It looks like it should work, and the connection *accepts* it without complaint — but it stores a dead value that matches nothing, so the view comes back permanently empty and nothing tells you it broke. This was confirmed the hard way. Always compute today's real date and write that exact date; a filter with "today" in it is a silently broken view, which is worse than an obvious error.

Then the two pages: the Someday page, then the review page with its nine linked views, in the order the weekly walk goes.

## Step 6 — The status block

Put a callout near the top of `My System` with placeholder text. The daily run rewrites it every time; it needs it to already exist.

It's a small thing that does something nothing else does: it says when the system last ran. If the daily run ever quietly stops, the client sees items sitting in her Inbox — which is exactly what she sees when everything is fine and she's just captured a few things. Nothing else would ever tell her, and nobody else can look at her system to notice for her.

## Step 7 — The system's pulse row

One small utility database, `System pulse`, holding exactly one row titled `heartbeat`. The rest of the product writes into it and reads from it: the daily run stamps its `Last checked` date every run, the weekly review stamps `Last reviewed` when a walk completes, and two formulas turn those dates into the only sentences the home page can show honestly with no run behind them — the "I haven't checked in since…" warning and the "ready when you are" review invitation. The specification has the exact schema and both formula strings; write the formulas character-for-character, never from memory.

Build it like everything else — **check before you create**:

- It may already exist in one of two places: directly under the target page, or inside a child page called `The filing room` (a build that already has the home surface keeps all its databases there). The recorded address in their settings wins; failing that, look by exact name in both places.
- **Create:** the database, the one `heartbeat` row, and seed *both* dates with today's date. That is honest, not decorative — this sitting reads every list and walks the whole structure with the client, and the review rhythm starts counting from it.
- **Adopt:** bring the properties up to the specification (adding a missing field is safe — the same rules as Step 3). Never overwrite a date that already holds a value; a newly added or empty date gets today's date, and you say so plainly ("the review rhythm starts counting from today"). Never make a second row — if extra rows exist somehow, use the one titled `heartbeat` and say what you found.
- **Verify what you can actually see.** Read the row back and confirm both dates landed. The formulas' computed sentences are invisible through this connection — that is a known limit, not a fault — so never claim to have checked what they say; a later step of the build (the home-surface script) proves them by drilling.

This row is the one place those stamps live. No run is ever allowed to invent its own place to write, so if this step is skipped the daily run and weekly review both end up with a duty and no home for it.

## Step 8 — Prove it actually works

You can't read the rollup's value back — the connection doesn't expose it. So the only real proof is watching the stalled view change.

Make a test project and one test action linked to it. Then walk the action through three states, checking the stalled view each time:

| Action's status | Stalled view should show the project |
|---|---|
| `Next` | no — it has a live next step |
| `Waiting` | no — it *still* has a next step, just a blocked one |
| `Done` | **yes** — nothing live is left |

The middle one is the one people skip, and it's the one that catches a real fault: if the live-step formula counted only `Next`, every project waiting on someone else's reply would light up the stalled view — the system nagging her about things she can't act on, until she learns to ignore the one view that must never be ignorable. Waiting has its own view, and the weekly review walks it; stalled means *needs a next action*, and a waiting project has one. So if the middle state shows the project as stalled, the build is carrying the old, pre-correction formula — rewrite it to the specification's exact string and run the probe again.

Also check the main "what can I do now" view, since its filter is the fiddliest in the system: give a test action a deferred date in the future and confirm it stays out of sight. **Then clear that date once the check passes.** (Found the hard way, 2026-07-24: a probe left holding a future date surfaces in the "scheduled to return" view and walks straight into the weekly review.)

**Leave both test rows at rest carrying no dates and no completion date** — Status `Active`, nothing else. No completion date keeps them out of "what got done," which is where the weekly review opens; no deferred or due date keeps them out of the "coming back" and "due soon" views, which the review also walks. Nobody's first review should start with rows called "test." Name them so their purpose is obvious, and mention them at handover so they're never a small mystery.

On a re-run, reuse the same two test rows rather than making more.

**One story about these rows, and every skill tells it the same way: they can stay, and deleting them costs nothing** — a later setup run simply makes them again. They are the build's own proof that the wiring works, not litter left behind. So never hand them to the client as something needing cleaning up, and never let the weekly review do it either; the review has its own instruction to leave them alone, and the two must not drift apart. *When the companion delete tool is reachable this sitting, the check can simply remove both rows once it passes* — confirm each is genuinely gone with an independent read, and then there is nothing to hand over at all. When it is not reachable, "they can stay" is the honest answer and the only one anybody should hear.

## Step 9 — Write down where everything is

Record each list's address in the client's settings **as you create it**, not in one batch at the end. A build that gets interrupted near the end would otherwise leave a complete system with no record of itself, and the next run would have to fall back to guessing by name — at exactly the moment when getting it wrong is most expensive.

Record the page you built under, and stamp the structure's version so a later run can tell what predates a change. **The current schema version is `0.2.0`** — the object-model change (2026-07-31, `docs/gtd-decisions.md` D23). Anything stamped `0.1.x` predates it and needs the migration under "Build order" in the specification, not a fresh build.

**Their settings file is theirs. Read what's there and change only the lines you have something new for** — the five list addresses plus the System pulse's, the page you built under, the schema version, and the timezone if you asked for it in Step 2 because it was blank. Splice each one into the file in place. **Never rewrite the file from the template and never re-emit it whole:** their contexts, their lists, how they answered about confidential records, how they like being spoken to, and any timezone they had already set all live in the same file, and a wholesale replacement wipes every one of them. That would be this system doing exactly the thing it promises never to do.

**A value they have already filled in is never yours to change.** If the timezone holds a real value and you have reason to think it's wrong, say so and let them decide — don't correct it on their behalf.

## Step 10 — Check your own work, then tell them what you did

**Before you report anything, read the build back — a handover records what exists, never what you intended.** The connection this build goes through has returned success for writes it did not perform, and its view tools have silently dropped filter clauses they didn't support (that is how the rollup gap was discovered) — so a clean build transcript proves nothing on its own. Step 8 already proved the plumbing chain behaves; this check covers everything Step 8 doesn't. Confirm each of these by reading it back fresh:

- **All fifteen views, by name — "the views" is not a list.** Each one's filter, sort, and visible columns match the specification. Sampling is how a real build once carried a filter ten days stale while every check reported fine.
- **No date filter anywhere stores the literal word "today."** The connection accepts it without complaint and stores a dead value matching nothing — a permanently, silently empty view. Every dated filter holds either today's real date (a fresh build, awaiting the one-time conversion) or a relative word (an adopted, already-converted build you left alone).
- **The fields, read back from the five lists' actual schemas** — all thirty-eight, against the specification, not against the creation calls having succeeded. Types especially: a field that landed with the wrong shape looks fine until the first write into it disappears.
- **The status block exists on the page.** The daily run can only rewrite what is already there; a build that skipped it leaves every future run with nowhere honest to speak.
- **The addresses you recorded in Step 9 read back from the settings file** — open it and look. A recorded address that didn't land sends the next run back to guessing by name, at exactly the moment guessing is most expensive.

If any of these fails, fix it and read it back again before saying a word about the build being done — a half-built system that reports itself finished is the one outcome this skill exists to prevent.

Then tell them what you did — plainly, and in their terms: five lists, a review page, and the wiring that keeps projects from going quiet. Not a schema.

Say three things that would otherwise become small mysteries:

- The two test rows, if they are still there — what they are, and that **they can stay, and deleting them costs nothing**, because a later setup run simply makes them again. (If the companion delete tool was reachable and the check already removed them, there is nothing to mention.)
- Anything you repaired or couldn't, especially a field you had to stop on.
- That Notion's own starter pages are still sitting there. Every new Notion workspace comes with them and there's no way to start without them. Offer to clear them out — in the browser, by hand. That stays a by-hand job even now that the companion delete tool exists: the tool deliberately refuses to touch anything outside the system it was installed for, and those pages sit outside it. A safety boundary, not a missing feature.

## What you never do

- Build before they've said yes to the page.
- Create anything without checking whether it already exists.
- Convert a field to a different type.
- Carry on after a search you couldn't finish.
- Replace their settings file rather than splicing into it, or overwrite a value they had already filled in.
- Report the system as built when a link in the chain is missing — a half-built system is worse than an unbuilt one, because it looks finished.
- **Ask the client to attach a folder wider than their Claude folder — ever, for any reason.** They hand you one folder and that is the whole of your reach on their machine. If something you are doing appears to need a file outside it, say plainly what you need and stop; moving that file in is their deliberate act, and it is the only way in. A widened folder is not a small convenience: inside an attached folder you can read, change and permanently delete every file the client's own account can reach, and nothing narrows that again afterwards. This holds even when the client offers — "just take my whole Documents folder" is a yes to something they have not been shown the size of, and the right answer is the narrower one.
