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

## ★ She can ask for this at any time — and a mid-day run is a lighter thing

The scheduled run is the guarantee. **It is not the only way this happens.** "Can you catch things up?" at eleven in the morning is a perfectly ordinary request, and it usually means something changed since the morning run — she has decided to bake a cake, something came up, a plan moved.

**Do not repeat the whole morning.** A second full run in one day spends another five of the ten reads for almost no benefit, and on a free plan that is the difference between the evening run working and failing. **A mid-day run does the part that has actually gone stale:**

- **Re-pick what the front page shows** and rewrite its lines. This is the thing that goes out of date within hours and the reason she asked.
- **File anything sitting in the Inbox** since the morning.
- **Note anything she has ticked off** since the morning.

**Skip:** the structure sweep and the weekly pass over the quiet lists (they ran this morning; nothing has changed), the recurrence pass (its work is done for the day and re-running it risks a second occurrence), and the dated-view stamping (the dates are still today's).

**And when the reason she asked is a single new urgent thing, you may not need a run at all.** Filing an action for today already puts it on the front page — capture does that as it writes. If that is all that has happened, say so rather than spending the budget: *"that's already on your page for today — nothing else needs catching up."*

## Before anything else — read the configuration

Read the client's `reflow-config` skill: their database bindings, contexts, areas, lists, timezone, and confidentiality settings. Without the bindings you cannot file anything, so if they are missing, stop and say so plainly rather than writing into the wrong place. Everything else falls back to documented defaults.

**The `gtd-method` skill is the other thing worth reading** — the definitions behind the lists and, more usefully, the places this system deliberately differs from standard GTD. Reach for it when something you are filing doesn't fit the capture skill's tree.

**Treat this file as behind, not as authoritative, on the option sets.** It records what her contexts, areas and lists *were* the last time anyone looked. She can change any of them in Notion herself, at any time, and Step 1 is where that gets noticed and the file caught up. The bindings are the exception — those are addresses, and they are authoritative.

**Timezone matters more here than anywhere else in the system.** "Today," "already past," and "when this is next due" all depend on it. Use the client's configured timezone.

**If it is not set, you are running in UTC — say so in the receipt, in those words.** Do not go hunting for a substitute — not in Notion, not anywhere. Nothing in the connection is known to expose a timezone of its own, and a run that quietly assumes one is exactly how every repeating thing in someone's life shifts by a day without anyone ever noticing. Write it plainly where they will see it — that this run used UTC because no timezone is recorded, and that telling Claude their timezone once fixes it for good. That sentence is the whole remedy; it is the only thing that turns this off.

This is not a rounding error for anyone in the Americas. From late afternoon on the west coast and early evening in the east, UTC has already rolled over into tomorrow — so a run in that window stamps the dated views with tomorrow's date and can bring a repeating thing back a day early. That is precisely the silent drift the rest of this skill exists to prevent, arriving through the one setting nobody was ever asked for.

## Then — check what you can reach, before you act

Two things vary from run to run and change what this run can honestly do. Check both once, at the start, and never carry an answer over from a previous run — a tool that answered yesterday proves nothing about today.

**First, the companion delete tool.** A local companion (an extra connection named `notion-extender-local`) may offer `trash_page` and `restore_page` — the one way a row can be moved to Notion's own trash rather than merely hidden. (Trash, honestly stated: recoverable there for thirty days, then gone. Never say "deleted for good" — the tool's own sibling is `restore_page`.) It runs on the client's own computer, so it is reachable only while their desktop app is open — which is why a scheduled run normally finds it absent. Look for it once. **Its absence is the normal state — never an error, never a reason to skip anything, and never worth an apology.** Everything below works fully without it; exactly one step (clearing noise, step 2) gains an extra move when it happens to be there.

**Second, the read meter.** On a free Notion plan the two list-reading tools (`query_data_sources`, the direct-query tool, and `query_database_view`, the view reader) are each budgeted, and the budget is checkable before you spend any of it: `fetch("self")` returns a per-tool status, and that fetch is itself unmetered — checking costs nothing. `limited_free_trial` means headroom; `upgrade_required` means that tool's budget is spent for now (it refills within about an hour). Three branches, decided here:

- **Both healthy** — proceed normally.
- **The direct-query tool spent, the view reader healthy** — take the three snapshots through the saved views instead: each list has one that covers this run's need (Actions' plain default table view, the Inbox's To process, Projects' Active projects), and the view budget is much deeper — fifty-plus reads per window against ten. The run proceeds nearly in full; say in the summary that it read through views this time.
- **Both spent** — this run degrades to what single-page reads and writes can do, and says so plainly. **Never present a budget you couldn't spend as an Inbox with nothing in it.** An Inbox you could not read is unknown, not empty — reporting it empty is exactly the silent failure this whole skill exists to prevent.

And if exhaustion slips through mid-run anyway, know its face: the failure is HTTP 400 `validation_error` carrying `entitlement_required` (and `retryable: false`) in the error body — **not** a 429, and not shaped like a rate limit at all. Match the error code, not the shape. Misread as a permanent validation bug it looks like something is broken; it is only the meter, and the next run will find the budget refilled.

## Read each list once, then work from memory

The steps below need to look through the Inbox, the Actions, and the Projects — several of them look through Actions more than once, for different reasons. **Do not go back to Notion each time.** On a free Notion plan, the tool that reads a whole list has a hard, low limit — about ten reads in a window, then it simply stops — and re-reading the same list for every step would blow past it and leave the run half-finished with no way to tell.

So: at the start, read each of the three lists **once** — the Inbox, all of Actions, all of active Projects — and hold them. Then every step below works against what you already have in hand: the orphan check, the completion stamping, the occurrence backfill, the recurrence pass, the "does this chain already have an open occurrence" check, the front-page tier pass — all of it reads from memory, not from Notion. Reading a single page's *content* — checking one project's status, reading a note — is fine and unmetered. **But verifying your own writes is different, and it is not free:** the cheap unmetered page read is the render that has echoed writes that never landed, so write-verification must go through the budgeted query tools — which means it is done in **batches, never per row**. One extra Inbox read at the close confirms every `Cleared` tick at once; if rows were trashed, one more confirms them all gone at once. The whole run's budget arithmetic, spelled out: three snapshots + at most two batched verification reads = **five of the ten**. Per-row verification would blow the budget by the fourth noise row — that is why it is banned, not just discouraged.

**Two things Step 1 does are deliberately outside that arithmetic, and both are free by design.** Reading each database's *shape* — its properties, its option sets, its views — is plain `fetch` and spends nothing from either budget, which is why the structure sweep can run every single time without a thought. And the weekly pass over the quiet lists reads them **through their saved views**, which come from a second, much deeper budget than the direct-query tool — so it costs nothing from the ten either. **Neither of them may be moved onto the direct-query tool to save effort.** Doing that turns a free check into a third of the run's entire budget, on the one run a week that can least afford it.

## Are you alone?

Three things — and only these three — depend on whether the client is present. Decide once, at the start, and be consistent for the whole run.

| | **Nobody there** (the floor — assume this) | **Client is present** |
|---|---|---|
| A capture too unclear to file | Leave it in the Inbox. Ask nothing. | You may ask the one clarifying question the capture skill describes. |
| Something left out for confidentiality | Write it to the notice store, unacknowledged. | You may say it directly, and mark the notice delivered. |
| The summary of what you did | Rewrite the home page blocks. | You may also say it in conversation. |

Everything else in this skill is the same either way. When in doubt, behave as though nobody is there — that is always safe.

## Step 1 — Take stock of what is actually there, then repair what is half-done

**Nothing tells you when her Notion changes.** There is no notification, no webhook, no signal of any kind — she edits something and the system finds out only because a run looked. **This run is the only thing that looks every day**, so this step is where the system stays in touch with reality rather than with its own memory of it. Do not skip it on the grounds that she mostly works through Claude. She has a Notion app on her phone and she is allowed to use it.

### The structure sweep — every run, and it costs nothing

**Walk the whole tree under her system page, not just the databases.** Reading a page's contents and a database's shape are both plain fetches — **unmetered**, spending nothing from either read budget — so scope this to *everything that is there*, not to the parts the system happens to have built. Her system is a place in her Notion, and things appear in places.

So: the system page itself and its blocks, any child pages and theirs, and the six databases. Four kinds of thing come back, and each has its own answer.

**1. The pages the system built, and the blocks it writes into.** The home page's greeting, date line, status callout, prose lines and toggles; the review page's headings and embeds; the someday page's two embeds. **These are load-bearing** — later steps of this run rewrite several of them, and a rewrite that cannot find its target is the failure that ends with a duplicate greeting or a lost note. Knowing now is better than discovering at write time. If something is gone, say so plainly and offer it back; **never quietly rebuild it, and never create a second one.**

**2. Blocks she added herself.** Notes on the home page, a paragraph under a heading, a whole section she made. **These are hers and they are not clutter.** Leave every one alone. The important part is what this implies for the rewriting later in this run: **you are editing specific blocks, never replacing a page's contents.** A rewrite that takes out something she wrote is the worst thing this run can do — it is her own words disappearing from her own system, with nothing to show her why.

**3. Things she made herself — pages, and databases too.** ★ **These do not get shrugged at.** She built something in her own system; the least useful possible response is to notice it and do nothing.

- **Learn what it is.** Open it. Reading is free and costs nothing from any budget. You are after the gist — *"a page of notes on books she's reading," "a table of the kids' school dates"* — not a summary of its contents.
- **Write down that it exists**, in her settings, alongside everything else the system knows about her setup: what it is called, where it lives, and one line on what it seems to be for. **Record the shape, never the contents** — if what she made holds anything private, a description of it does not belong in a settings file, and the one-line gist is the right level regardless.
- **Ask her once whether she wants it looked after.** *"I noticed you made a Book notes page — do you want me to keep an eye on it, or is that one yours?"* One question, the first time, phrased so that "mine, thanks" is an easy answer.
- **Then honour the answer, permanently.** Yes → it is part of what you tend: it gets read on the weekly sweep, it can be filed into, and it is fair game to mention when it is relevant. No → recorded as hers, never asked about again, never touched.
- **Until she answers, it is hers.** An unanswered question is not consent.

**Why the asking, rather than just adopting it.** Maintaining something is a commitment on her behalf, and she did not ask for it. But *knowing about it* costs nothing and refusing to know is just unhelpful — the point of this system is that nothing in her life is invisible to it, and a page she made is part of her life. **The old answer here was "it is hers, nothing will tend it" full stop, which read as a limitation of the platform when it is really only a question nobody had asked her.**

**4. The six databases** — their properties, their option sets, their views. That is the rest of this section.

Fetch each of the six databases and look at what came back.

**Option sets — contexts, areas, lists.** Compare them against her settings.

- **In Notion but not in her settings** — she added it. **Notion is right and her settings are behind.** Catch the file up so capture starts using it, and say so in the receipt: *"you added an `@Office` context — I've started using it."* Without this the option sits in the dropdown doing nothing, because Claude never files into an option it doesn't know about. That is worse than the option not existing, since it looks like it works.
- **In her settings but not in Notion** — usually a setting written that never reached the structure. Add it: read the current options, keep every one exactly as it is, append the missing one.
- **Never resolve a difference by deleting** — not from Notion, not from her settings. If they disagree in a way adding cannot fix, say what you found and change nothing.

⚠ **The one thing that must never happen: writing an option set from the specification alone.** That destroys every option she added, and every row holding one goes blank — silently, with the write reporting success (gap ledger **F-26**). Read first, keep what is there, only ever append.

**Properties and views.** Note anything missing that the system depends on — a property gone, a view deleted or renamed. **Do not rebuild it silently and do not panic.** Say what is missing and what it costs her (*"the `Waiting for` view isn't there any more, so there's no screen showing what you're waiting on"*), and offer to put it back. A view she deleted on purpose is her call; a view she deleted by accident is invisible to her precisely because it is gone.

**A database she built herself** gets exactly the same treatment as a page she built — learn it, record that it exists, ask once whether she wants it looked after, honour the answer. See point 3 above.

**And the general rule, for anything this sweep finds that is not in the specification:** *it is hers, it is not a fault, and it is not yours to remove.* The specification says what must be **present**. It has never said what must be **absent**, and a run that treats "unexpected" as "wrong" will eventually delete something she cared about. When you genuinely cannot tell what something is, that is fine — say you saw it, say you left it alone, and move on.

### The quiet lists — once a week

The three lists this run reads every time are the Inbox, Actions and the active Projects. **Reference, the lists, and the parked projects are never read**, which means anything wrong in them is invisible for as long as nobody looks. A task misfiled into Reference is the worst version of this: it is in none of the review's steps either, so it is simply gone.

So **once a week — on the first run of the day if it has been seven days or more since the last sweep — read them too.** Do it **through their saved views**, not through the direct-query tool: view reads come from a separate and much deeper budget, so this costs effectively nothing from the precious one.

What you are looking for, and it is a short list:

- **Something that is obviously a task** sitting in Reference or on a list — *"renew the passport"* is not a fact to look up and not a thing to pick up while shopping. Move it and say you did.
- **Rows she added by hand** with fields left blank — complete them, per the rule below.
- **A list filling up that has no home** — several captures of the same shape landing in one place is D17's pattern, and the answer is to offer her a list for it.

Say what the sweep found in the receipt. If it found nothing, say that too — *"had a look through your reference and your lists, all in order"* — because a silent check is indistinguishable from one that never ran.

### Then: repair anything left half-done

**Do this before touching new captures.** Filing is several steps, and only the first one is atomic, so a run that died partway through can leave something stranded where nobody will ever see it.

Look for the signature of an interrupted filing: an action carrying what looks like raw captured wording with no Status set, or a project with no outcome and no action linked to it. These are invisible in every view the client looks at, and they are no longer in the Inbox, so no ordinary pass would ever find them again.

Finish each one properly — set the fields it never got — before moving on. If you cannot tell what it was meant to be, move it back to the Inbox and let it be processed normally. This same pass is what catches the rare case where two runs overlapped and both touched the same thing.

### ★ Also here: rows she wrote herself

**She can add a row straight into Actions, and she may.** It is her Notion; the fields are right there and she can fill in as many or as few as she likes. A row that arrives this way is not an error and never gets treated as one — **it is a capture that took a shortcut.**

Give it whatever it is missing, silently and without comment: a `Status` of `Active` if it has none, an `Area`, a `Context` if you can tell what one fits. **Never overwrite anything she filled in herself** — if she chose `@Errands`, that is the answer, and your job is only the blanks. If a field is genuinely unguessable, leave it blank rather than inventing one; a missing context costs her a little, a wrong one costs her trust.

The same goes for a row she adds to Projects, to Reference, or to any of her lists. Complete the blanks, change nothing she wrote.

*(The structure sweep and the weekly pass over the quiet lists are above, at the top of this step — they run before any of this, because knowing what is actually there comes before repairing it.)*

## Step 2 — Empty the Inbox

For each row, oldest first. **Do not restate the filing decision here** — the capture skill owns what a captured thought is and where it belongs; read it and follow it. This skill owns only *when* that happens and *how the row physically moves*.

**Skip what has already been judged.** A row whose hidden `Cleared` box is ticked is settled — pass over it in silence. So is a row whose `Note` carries a written verdict from a run that predates the checkbox (`noise — judged …`): honour it, and if the `Cleared` box exists, tick it now so the row finally leaves the client's view too. What a verdict is and when you record one is at the end of this step.

The order is exact, and it matters:

1. **Move the row** into the database it belongs in. Do not create a new row and try to remove the old one — moving carries the original capture date with it, and the copy-then-trash alternative is worse even now that a trash tool sometimes exists: it would park the client's original words in Notion's visible trash for thirty days, trading a clean move for a lingering copy.
2. **Write the client's own words into the page body**, if what you are about to call it differs meaningfully from what they wrote. Not into a notes field — those are named differently in every list, and half of them don't have one. This has to happen after the move (the Inbox has nowhere to put it) and before the rename (which is what replaces their wording).
3. **Rename it** to the action or outcome.
4. **Set the fields** the capture skill specifies.

**When a capture turns out to be a project:** move the row to Projects and rename it to the outcome — their words describe the thing they want, not the first step. Then create the first action fresh and link it. If a run dies between those two, the stalled-projects view will surface it, which is exactly what that view is for.

**When a capture is too unclear to file:** leave it exactly where it is. Do not guess, and do not fill the Inbox with half-decisions. It will be picked up in the weekly review.

**When a capture has nowhere to go at all** — pure noise, or something already done and needing no follow-up — **tick the row's hidden `Cleared` checkbox.** That is the whole verdict: the row leaves the client's To-process view the moment the box is ticked, and the judgement is durable, so no future run ever considers it again. Then name it in the summary — what was cleared, with a word of why — never a silent disposal. Do not invent a task to justify a capture.

**If the companion delete tool is reachable this run, finish the job — but in the right order, at the close.** After ticking `Cleared`, put the row on this run's trash list and move on; **the actual trashing happens in step 8, after the batched read has confirmed the ticks.** The order is load-bearing: a trashed row can no longer answer the tick check, so trash-then-verify makes a landed verdict indistinguishable from one that never landed. Verify the ticks first (one batched read), then trash the verified rows, then confirm them with one more batched read — all of them at once, in the trash — never the call's own success response, and never a page render, both of which have claimed effects that didn't happen. Name every row you sent to the trash in the summary, just as you name what you cleared. When the tool is absent — the normal state for a scheduled run — the tick alone is the whole move, and that is not a shortfall: the row is out of the client's sight and the verdict holds. Rows ticked by earlier runs stay where they are either way; sweeping the settled backlog for real is the weekly review's offer to make, never this run's surprise.

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
- Carry across everything that made it what it was: the name, the context, the project, the cadence, the area, the occurrence identifier. Status is `Active`.
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
- **carried** — `Planned` before today, and Status is none of `Done`, `Someday` or `On hold`. A plan that slipped stays in front of the client until it's done or re-decided; it is never allowed to quietly disappear. **The three excluded statuses are one rule, not three:** carried means *a plan of hers that slipped*, so something she has since parked must never come back to the front page wearing that word. Before the object model gave actions a parked status, `Done` was the whole of it because finishing was the only way out; now there are three ways out, and a someday action still holding last month's `Planned` date would otherwise read as "you meant to do this and didn't." **This is the same rule the home page's Carried view filters on — they must say the same thing, or the toggle's label counts one more item than the list behind it shows.**

These are the client's own commitments to today. The short list's cap yields to them, and they are never held behind the fold.

**The judgment tier — fill to a calm few.** After the guaranteed tier, fill the remaining slots to roughly seven in total: one action per active project first, then standalone captures. Tick those; leave everything else unticked — the overflow sits one tap away, never lost. On a week already carrying slipped plans, fill lighter: a carried group plus a crowded list reads as a pile, and a pile is what this system promises never to hand her.

Then clear the flag on everything you didn't choose this run. Yesterday's choices never linger.

**Two things you never do here.** Never change `Planned` itself — a slipped plan keeps its original date, because the date *is* the record the weekly review re-decides from; rolling it forward would quietly erase the truth. And never describe a carried item as overdue, late, or behind — it is *carried*: still here, nothing lost. Overdue is for deadlines, and a plan is not a deadline.

### Then say it in the page's own words

Ticking the flag decides *what* the home page shows. The page's short lines of prose are what make it read as calm rather than as a dashboard, and they go stale the moment the lists move underneath them. **A stale line is worse than no line**, because the client has no way to tell it is stale — it looks exactly like a fresh one.

**If the home page has none of these lines, it predates the surface — skip this and say so once in the summary.** Never invent a line the build didn't put there, and never add a second copy of one you cannot find. You are always rewriting a block that exists.

Find each by its role on the page, not by remembering an address — the build differs per client:

- **The greeting and the date line** at the very top. Time of day and the real date in the client's configured timezone. If the timezone is blank you are running in UTC, and you say the date plainly rather than guessing at their morning.
- **The lead action** — the single gray line under the "right now" heading, offering one thing worth doing: *"If you've got ten minutes: call the pharmacy about the refill."* Pick it from the guaranteed tier you just ticked, favouring something genuinely small. If nothing qualifies, a warm true sentence beats a manufactured suggestion.
- **The toggle labels** — the collapsed lines that say how much is held back and what is carried. Each carries a count when there is something inside and a **warm sentence when there is nothing**: "nothing carried right now" is the calm state and reads better than a zero. The same applies to the scent lines on the section headings ("8 projects · every one has a live next step") — and **only say that if you checked it**; a scent line asserting nothing is stalled, when you never looked, is the most quietly corrosive line on the page.
- **The empty-state sentences** — where a view has gone empty, its warm callout shows; where it has filled again, that callout goes away. Notion renders its own "no results" chrome and you cannot change it, so these swapped sentences are the only warmth available there.

Every one of these is prose about live numbers, so **write them from the rows you actually read this run**, never from what you expect them to be. If a budget ran out and you could not read a list, leave that list's line alone rather than writing a confident sentence about data you never saw.

## Step 7 — Keep the dated views honest

Some views filter on a date that was written in when they were built, not one that moves on its own. Left alone, they drift: an item that was deferred until a date that has since arrived falls out of the "what can I do now" view *and* out of the "coming back later" view, and becomes invisible in both. Nothing is more corrosive than a commitment the system quietly stops showing.

**First, look at what each filter actually says — because there are now two kinds of dated view, and they need opposite treatment.**

A view converted to Notion's own **relative** dates (its filter literally says `today`, `one_month_from_now`, `one_week_ago` — a word, not a calendar date) **maintains itself. Leave it completely alone.** Re-stamping it with a real date would be the worst edit available: it silently downgrades a self-maintaining view back into one that rots, and nothing would ever look wrong. These relative values are real and live — confirmed by execution over two days (2026-07-26/27): the stored `today` advances by itself.

A view still carrying an **absolute** date (a real calendar date like `2026-07-27`) is the old, interim kind — it was built through the first-party connection, which can only write literal dates — and it still needs the re-stamp, every run, until it gets converted.

**So the step is: read all four filters, skip the relative ones, re-stamp the absolute ones. Name them, and check them all — "the dated views" is not a list.** A run that handles some and not others leaves no trace, because a stale view looks exactly like a fresh one:

| View | Self-maintaining (relative) form — leave alone | Interim (absolute) form — re-stamp to |
|---|---|---|
| Actions — by context | `Defer` on or before `today` | `Defer` on or before today's real date |
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
- Every row you cleared this run actually reads back ticked — **one batched query covering all of them** (never per-row, never the page render that just accepted the write; a render can echo a write that never landed, and a verdict that didn't land means the same question tomorrow). **This check runs BEFORE any trashing** — the trash list waits until these ticks are confirmed.
- Every row you then trashed reads back in the trash — one batched independent read covering them all, never the call's own success response. A removal you didn't confirm is a removal you may not claim.
- If any work waited because a read budget was spent, the summary names that constraint in plain words. A run that was starved is never allowed to read as a run that found nothing to do.
- **Every line of prose you rewrote on the home page matches the numbers you actually read this run** — greeting and date, the lead action, both toggle labels, the scent lines, any empty-state sentence you swapped. A line you updated from memory of last run, or from an expectation rather than a read, is the failure this check exists for. Any line you deliberately left alone because you couldn't read its list is named in the summary, not silently skipped.
- **You wrote to blocks that already existed** — one greeting, one date line, one status callout, one heartbeat row. If you could not find one, you said so rather than creating a second. Two status callouts on a page is a system arguing with itself in front of the client, and the older one never goes away on its own.

Then rewrite the status block on the `My System` page — the callout the setup put there for exactly this. You are always rewriting it, never creating it; if it is genuinely missing, say so rather than improvising a second place to write, because a summary nobody can find is the same as no summary.

Keep it short, warm, and **honest above all**:

- What was filed, in plain numbers.
- What you left, and why — "I left one for you, I wasn't sure what you meant by it." A client who finds something you claimed to have handled is a client who stops trusting the whole thing.
- What you cleared as noise or already-done — named, with a word of why. A verdict the client never hears about is a thought that feels swallowed.
- What you sent to Notion's trash, if the companion tool was there — named, like the clearing verdicts, and stated as what it is: in the trash, recoverable for thirty days, then gone. Never "deleted forever." And when the tool wasn't there, cleared rows were hidden and left in place: one matter-of-fact sentence, not an apology.
- What waited for budget, if anything — named as the constraint it is ("the workspace's free query budget for this hour was spent; it catches up next run"), never dressed up as an empty list.
- What came back around, as a count rather than a list.
- Never claim an empty Inbox unless nothing unjudged is actually left waiting.

**Then record that you ran — on the heartbeat row, which is the specific durable place.** The system carries a one-row utility list (a "System pulse" table, kept out of the client's way in the filing room) whose single row holds a `Last checked` date. Stamp today's date there, and understand what you are stamping: **a formula on that row renders the staleness sentence on the home page, and a view filter shows the row only once the date is two days old.** That one date is the whole mechanism by which the page can admit the runs have stopped. Nothing else keeps the sentinel dormant, and no other write substitutes for it. If the row isn't there, the structure predates it — say so in the summary and carry on; never build a second one to write to.

**And the stamp is a claim, so a run that cannot honestly make it does not make it.** `Last checked` means *I looked at your lists today* — not *I executed*. If a read budget ran out and lists went unread, or you could not reach the workspace, **leave the date alone and say why in the summary.** The sentinel then fires on its own a day or two later and tells the client the truth: nothing has properly checked in. That is the system working. Stamping anyway would silence the one signal designed to survive your own failure — the single most damaging write available to you, because it makes a degraded system look serene.

Beyond the heartbeat, if the run was starved, the summary's own line says so, so a string of starved runs can never masquerade as a string of healthy ones. This matters more than it sounds: if this stops working — a connection expires, a task gets deleted, a plan stops supporting it — the client sees an Inbox with things in it, which is *exactly* what they see when everything is fine and they simply captured a few things. Silence looks identical to health. So if the last successful run is older than the configured threshold, say so plainly where they will see it. Nobody else can notice this for them; by design, nobody else can see their system at all.

**Anything that must survive being unread does not go in the status block**, because you rewrite that every run — a note left on Monday is gone by Tuesday. Above all this applies to something you left out for confidentiality, which is the highest-stakes thing you ever have to say.

Those go in the **page body of the action they concern**, where they stay as long as the action does and where the weekly review will find them. The status block carries only a count and a pointer: "there are two things I left out — the notes are on those tasks." No separate pile, and nothing important living somewhere that gets overwritten.

## What you never do

- Ask for a brain-dump, or suggest the client sit down and empty their head. Capture is something that happens whenever it happens; this run exists so it does not become homework.
- Fill an unclear capture with a plausible guess.
- Report an empty Inbox that isn't — including one you couldn't read because a budget was spent. Starved and empty are different truths.
- Treat the companion delete tool's absence as a failure, or report it as one — a scheduled run normally doesn't have it, and its absence changes nothing the client was promised.
- Claim a deletion you have not confirmed with an independent read.
- Describe a repeating item as though the client is behind on it.
- Change a `Planned` date, or describe a slipped plan as overdue, late, or behind — a plan that slipped is *carried*, and its original date is the record.
- Weaken the confidentiality strip because nobody was around to be told.
- **Stamp `Last checked` on a run that could not actually check** — a spent budget, an unreachable workspace, lists you never read. The stamp claims you looked; making it falsely silences the one signal built to survive your own failure, and leaves a degraded system looking serene.
- Create a second greeting, date line, status callout, or heartbeat row because you could not find the first. Say it is missing instead; a duplicate is permanent and the client sees both.
- **Replace a page's contents.** You edit the specific blocks you own — never rewrite a page wholesale, never "tidy" one, never remove a block you did not put there. She may have written something on any page in her system, and a page-level rewrite takes it out with no warning and nothing to restore it from. This is the single most destructive thing available to this run, and unlike a bad filing decision it leaves no trace of what was lost.
- **Delete or repair anything that is merely unexpected.** A page, a database, a property, a view, a block, an option you did not put there is *hers*, not drift. Say you saw it; leave it exactly as it is.
- Write a count, a scent line, or an empty-state sentence from what you expected the list to hold rather than from rows you read this run.
