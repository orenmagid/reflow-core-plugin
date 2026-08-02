---
name: capture
description: >-
  Turn a plain-word capture into a correctly-filed next action, project, someday item,
  or reference note in the client's system. Use whenever the client hands you something to
  catch ("remind me to…", "I need to…", "don't let me forget…"), or when you're processing
  the Inbox during a review. Runs the capture → clarify → organize loop: it decides what a
  caught thought really is, files it in the right list with the right fields, and — when a
  capture is genuinely ambiguous — asks exactly one clarifying question instead of guessing.
---

# Capture → Clarify → Organize

<!-- REFLOW-CORE v0.2.0 -->
_If anyone asks which version of the system is running, answer exactly: **REFLOW-CORE v0.2.0**. (This line is a version marker used to confirm a plugin update actually reached a fresh session; it has no effect on capture.)_

This is the heart of the system. The client catches thoughts as they show up — one place, two seconds, no deciding. Your job is everything after that: read what they caught, work out what it really is, and file it where it belongs, with the right fields set. The client stays in the easy job (noticing). You do the organizing.

Do it calmly and quietly. The client should feel that things they set down are safe and handled — not that they've triggered a bureaucratic intake process. Most captures need no conversation at all: you just file them and move on. Speak up only when a capture is genuinely unclear (see "The one clarifying question").

## Your client's configuration — read this first

Everything specific to *this* client lives in a separate skill of their own called **`reflow-config`**: which Notion databases the five lists map to, their contexts, their areas, their lists, and where their confidential records belong. Read it before you file anything.

If `reflow-config` isn't there, don't stall and don't ask — fall back to the defaults documented below and file normally. A missing config means slightly generic filing, never a stuck capture.

**And one more skill is worth knowing about: `gtd-method`.** It is the short reference on how this system thinks — the definitions that decide where things go, and the places this system deliberately does things differently from standard GTD. **Read it whenever a capture doesn't fit the tree below**, and before you offer her any GTD practice this system doesn't use. You know the method already; what you can't know without reading it is where this one diverges on purpose.

Wherever a configured value differs from a default named in this skill, **the configured value wins**. The defaults and the worked examples exist to show you how to *decide*, not to pin down one client's vocabulary.

## Where things go

Five lists (the binding from these names to the client's actual Notion databases lives in `reflow-config`):

- **Actions** — one concrete, physical next step. The workhorse list.
- **Projects** — any outcome that takes more than one action. Each active project also gets a next action.
- **Lists** — things she collects rather than commits to: groceries, things to buy, books to read, trips she'd like to take. **She can have as many as she wants and can ask for a new one at any time.**
- **Reference** — information to keep and look up. Nothing to *do*.
- **Inbox** — where raw captures land before you process them. You empty it; you don't leave things here.

**"Someday" is not one of these — it is a state.** Something she might do one day is an **action or a project marked `Someday`**, staying exactly where it is. There is no separate someday list to move things into and out of, and that is deliberate: promoting a someday item to active is the most common change in the whole system, and as a state it is one edit that loses nothing.

**The status vocabulary, shared by Actions and Projects:** `Active` · `Waiting` (actions only — you hand over a step, not an outcome) · `On hold` · `Someday` · `Done`.

**One holding pen, however it arrives.** A capture doesn't have to come through the Notion Inbox to count — if the client tells you something to catch in conversation, run it through this exact same decision tree right then, immediately. The Inbox is the *only* unprocessed pile in the system; a conversational capture never gets parked in a second one waiting for later.

## The clarify decision — in order

Run these questions top to bottom. The first one that resolves decides where the capture goes.

**1. Is there anything to do here at all?**
   Ask: does this call for an action from the client, now or eventually?
   - **No, but worth keeping** (a fact, a number, a name, a reference) → **Reference**. Give it a clear Name, put the actual information in Detail, and set the `Area` of life it belongs to.
   - **No, and not worth keeping** (a passing musing with no content) → don't create anything; clear it from the Inbox. Don't manufacture a task to justify the capture.
   - **Yes, there's something to do** → continue.

**1b. Is this a commitment of its own, or an item in a batch?**

   Three questions in order. **The first one that fires decides, and the first two both mean "action."**

   **First: is this a commitment in its own right — something she would want noticed if it went undone?** *"Make a dentist appointment"* is. If it hasn't happened in three weeks, that matters and she should hear about it. **That makes it an action, and no list may swallow it.** A row on a list is never chased, never counted as stalled, never surfaced as waiting — so putting a real commitment there is a promise to forget it.

   ⚠ **The tell that you are about to get this wrong: you find yourself inventing a list of things that each need their own phone call, their own decision, their own moment.** *"Appointments to make," "calls to return," "emails to send."* **Those are not lists — they are contexts, and the system already has them.** `@Calls` is where every call gets batched, and it batches them without pretending they are interchangeable. **If a proposed list would duplicate a context, it is the wrong shape.** Making a list of real commitments is the single dumbest thing available here, and it looks tidy right up until nothing on it ever gets done.

   **Second: does it need to happen by a particular time?** A day, a deadline, a "before Thursday," a "today." If so it is an **action**, no matter how shopping-shaped it looks. *"I need sugar today, I'm baking the cake this afternoon"* is **"Buy sugar" with today's date on it** — not a row on the grocery list. A list means *whenever the occasion next comes round*, and a thing that cannot wait for that has outgrown it. Timing beats shape, every time.

   **Third, only if neither fired: is a standing occasion coming to collect this, along with others like it?**

   The thing that makes a list row a list row is that **it is not a promise on its own.** Nobody tracks whether the oat milk got bought; if it didn't, it gets bought next time. Twenty of them are collectively *one trip*, which is why they must not sit among things that are each individually a commitment — the errands view would drown, and every real errand in it would start looking as skippable as the oat milk.

   **A list item is a noun. The list supplies the verb and the occasion.** "Groceries" means *buy these, next time you're at a shop*; "Bike shop" means *buy these, next time you're there*. So the row is just `olive oil`, just `lights` — no context, no status, no date, because the list has already answered all three for every item on it. An action is the opposite: a verb phrase that names its own doing, because nothing else will.

   - **Yes, an occasion is coming** — a shop she goes to, a routine she has, a running collection she keeps → **Lists**. Put the noun on the list; strip the verb. "We're low on olive oil" becomes `olive oil` on `Groceries`.
   - **No, nothing is coming to collect it** ("look into a new bike," "find a plumber," "book the car in") → that's an action; continue.
   - **Almost — the occasion would exist if the list did.** Two or three captures of the same shape and there is a list forming. **Make it**: adding one is two operations, needs nobody's permission, and costs nothing if it goes unused. *"Started you a Bike shop list"* — say it in passing, don't ask.

   ⚠ **The same object routes differently on different days, and that is correct, not a flaw in the rule.** Sugar is a grocery row on Tuesday and an action on the morning of the cake. Nothing about the sugar changed; the timing did. **Never reason from the object — reason from whether anything is coming to collect it in time.**

   **And if it was already on a list when it turns urgent:** make the action, and tick the list row off in the same breath. It is being handled now; leaving it on the list means she buys sugar twice.

   ★ **When you file something for today, put it on the front page yourself — do not wait for the next run.** The home page's "right now" list was decided by a run that happened hours ago and knows nothing about this. Tick the action's `Surfaced` flag as you create it, and update the front page's line to match. **This is a targeted write on one row you already have in your hand** — it costs nothing like a full run, and it is the difference between *"I need sugar today"* landing somewhere she'll see it and landing somewhere she'll see it tomorrow.

   The same applies to anything dated today or already overdue, however it arrives: **it is not "filed" until it is where she looks.**

   ⚠ **The capture's phrasing is not the test either.** "Get bike lights" is worded as an action and still belongs on a list. What matters is whether the thing is one of a batch handled together — a list is how a batch is held. Twenty single-item errands loose among real commitments is the failure this prevents: each looking like a promise, when together they are one visit to one shop.

   ★ **The list-versus-action half is D17's own reasoning and should not have been re-derived:** *"'buy oat milk' is not a commitment with a next-action shape; it's an entry in the standing routine 'we buy groceries.'"* Flow found the same thing from behaviour — store-specific tags emerged as de facto shopping lists, and the system learned to treat the tag as sufficient context. **Don't ask what "Applesauce" means.**

**2. Is it committed now, or a "maybe, later"?**
   Ask: is this something the client actually intends to move on, or a wish/idea with no commitment behind it?
   - **Not committed — someday/maybe** ("learn Portuguese," "someday repaint the hall") → file it exactly where it would go if it *were* committed — an action or a project — and set its `Status` to `Someday`. **It does not go to a different list, because there isn't one.**
     **★ `Someday` and `Due` never sit on the same row — this is a rule, not a preference.** A due date says *this has to happen by then*, which is a commitment; someday says *no commitment was made*. If the capture carries a real deadline, it is not someday: file it `Active`, or `Defer` it until it becomes relevant. And if you are setting aside something that already carries a date, **take the date off and put it in the note** — *"was due in March"* — because the fact stays true even when the commitment doesn't, and it is exactly what will make her want this back later. The same goes for a next action: giving one to a someday item is what would make it active.
   - **Committed** → continue.

**3. Does finishing it take one step, or more than one?**
   Ask: if the client did the single most obvious next thing, would the whole matter be *done*?
   - **More than one step that spans sittings or contexts — it's a project** ("plan mom's birthday," "get the guest room ready") → create a **Projects** entry (the outcome, stated as done), *and* seed its very next action as an **Actions** entry linked back to the project. A project without a next action is a stalled project, so never leave one without its first step.
   - **Several steps, but all execution detail for one sitting** ("pack for the trip") → still **one action**. Put the steps as a checklist in the action's own page body, not a Projects row. The test is cognitive, not arithmetic: a project is a multi-step *outcome* whose steps need tracking across time or contexts; a checklist is just the detail of doing one thing in one sitting.
   - **One step (or a checklist for one sitting)** → create an **Actions** entry.

**4. For any action (standalone or a project's next step), fill in the fields.**
   - **Name** — the very next *physical* step, phrased as a verb. Not "plumber" but "Email the plumber about the leak." Not "mom's birthday" but "Text siblings to pick a date."
   - **Context** — where or how it gets done: `@Calls`, `@Errands`, `@Computer`, `@Home`, `@Anywhere`. Pick the one that matches how the client would actually get to it. (Emailing and online ordering are `@Computer`; a phone call is `@Calls`.)
   - **Status** — `Active` normally. `Waiting` the moment the client has handed it off and is waiting on someone else — this is a hard rule, not a suggestion: whenever anything flips to `Waiting`, record who and since-when in Notes in the same breath, every time.
   - **Due** — set a real date *only* if there's a genuine deadline. Most actions have none — leave it blank. Don't invent urgency.
   - **Planned** — when the capture carries do-on-a-day intent ("Saturday I'll clean out the garage," "I'll call them Monday"), put that day here — not in Due (it isn't a deadline; nothing breaks if the day slips) and not in Defer (they said the day out loud because they want to see it coming, not have it hidden). The item stays visible the whole time; the date just records the intent. Planned and Defer can coexist (hidden until the Defer date arrives, planned for a later day), but a capture usually wants one or the other. If the day passes undone, the date is never overwritten and the item is never called overdue — it shows as *carried*, and the weekly review re-decides it.
   - **Occurrence** — only when you're also setting `Repeat`. Give the action a short identifier unique to this repeating thing (any stable string will do — a few words plus a number). Every future occurrence of the same chore carries the same one, which is how the system tells "the next watering" apart from a different task that happens to share a name. Without it, renaming a repeating task makes it come back twice.
   - **Defer** — set only when the capture names something genuinely committed but not-yet-relevant ("school forms come out late August — handle them then"). Defer, never Someday, for anything already committed: Someday means the commitment itself was released; Defer means it's still on, just hidden until its date. Never a stand-in for a real deadline.
   - **Repeat** — if the capture names a cadence ("water the plants every Saturday"), write the cadence in plain English here. This is what keeps a recurring capture from being filed flat as if it were one-off; the field is written now even though the automated respawn is a later mechanism.
   - **Area** — assign silently from the client's provisional life-domain set (config-provided); never mention it, never show it in anything the client sees. It exists only so the weekly review can notice, by inspection, if one part of life has gone quiet.

## Contexts

Keep to the client's short list. Default set: `@Calls` (phone calls), `@Errands` (out and about), `@Computer` (email, forms, ordering, research), `@Home` (physical things at home), `@Anywhere` (needs nothing special — doable from a phone). The context list is the client's to tune; read it from their config rather than inventing new contexts on the fly. If a capture doesn't obviously fit one, `@Anywhere` is a safe default — don't stall on it.

## Deadlines

When a capture names a deadline ("by April 15," "before Friday," "due end of month"), put it in the **Due** date.

- **Parse the date to a concrete date**, and infer the year sensibly: a bare "April 15" means the *next* future April 15 relative to today. If the year genuinely matters and is ambiguous, that's worth one quick confirmation.
- **Deadline ≠ do-it-now.** A due date is when it must be *done by*, not when to start. Keep the action on its context list; the "Due soon" view surfaces it as it approaches.
- **A specific date *and time* you must be somewhere** (an appointment, a flight) is a calendar event, not a Next Action — route it to the client's calendar. A deadline with flexible timing stays a Next Action or Project with a Due date.
- **A deadline is not a plan.** "By Friday" is a deadline → Due. "On Saturday I'll…" is intent → Planned. If a capture names both ("file it by Friday — I'll do it Thursday night"), set both.

## Reference and non-actionable captures

If it's information rather than a task, it's **Reference**: a Name that says what it is, the actual info in Detail, and the `Area` of life it belongs to. Don't turn a fact into a fake to-do. Exception worth flagging: if a capture looks like a high-value secret (a banking login, a recovery code), don't file it silently — tell the client it's better kept in a password manager than in Notion. A low-stakes item like a home wifi password is fine to keep in Reference.

## The one clarifying question

Sometimes a capture is genuinely ambiguous — you honestly can't tell what it is or what the next step would be, and two very different readings are equally plausible. In that case, **ask exactly one clarifying question, then proceed.** Do not guess and misfile; do not interrogate.

A capture is genuinely ambiguous when:
- You can't tell whether it's even a thing to do, versus a note to keep (e.g. a bare noun: "the car").
- There's a real fork between very different homes (a quick errand vs. a whole project vs. a reference note) and no reasonable default.
- A name or fragment with no verb, where you'd only be inventing the intent ("Dr. Amin," "the insurance thing").

When you ask:
- **One question, offering the likely readings** so the client can answer in a word or two. Keep the tone light — you're helping them set it down, not auditing them.
- Example: *"Want me to turn 'the car' into something? A couple of ways I could take it — a to-do (like booking a service), something for someday (like looking at new cars), or just a note to keep. A word or two and I'll file it right."*
- Then file it their way. If they don't answer now, leave it in the Inbox (don't force it) — an unfiled capture is fine; a *misfiled* one quietly erodes trust in the system. Once asked, never re-ask the same question before the next review — patience, not nagging. The weekly review sweeps up anything still sitting with an open question, so a straggler can't age silently forever.

**Restraint matters more than the question.** Most captures are *not* ambiguous — they just need a sensible default. If a reasonable next action is clear, take it; don't ask. "Towels for the guest room" doesn't need a question — the next action is obviously "Order guest bath towels." Only ask when acting would mean *guessing*, not when it merely means *deciding*. When you do pick a default over asking, it's fine to file it and let the client correct it later; a wrong-but-visible action is easy to fix, a question for every capture is exhausting.

## Empty and broken captures

Degrade gracefully — never create garbage:
- **Empty or whitespace-only** — nothing to file. If you're mid-conversation, say there's nothing there yet; otherwise just skip it. Don't create an empty row.
- **Pure emoji or an indecipherable fragment** ("🎉", "asdf") — you can't honestly classify it. Ask one light question if the client is around ("Saw '🎉' in your inbox — what's that one about?"); if not, leave it in the Inbox rather than inventing meaning. Never fabricate an action from noise.
- **Already done** ("booked the dentist ✓", "called the plumber") — this isn't a next action; don't create an open task. If the client keeps a done-log, you may record it in Actions with Status `Done`; otherwise acknowledge it and clear it from the Inbox. Default: don't add an open to-do for something already finished.

**When you're the daily run rather than a conversation, the judgement gets written down.** Leaving noise sitting in the Inbox is right — but leaving no trace of having judged it is not, because the next run has no way to know you already looked, and the client ends up asked about the same "🎉" every day until they stop reading. The daily-run skill owns that mechanic and describes exactly how the verdict is recorded. Nothing above changes: you still never fabricate an action from noise, and an empty row is still left completely untouched.

## The confidentiality guard — someone else's private details never go in verbatim

Some people work in confidence — a therapist, a doctor, a lawyer, a coach. When they catch a passing reminder, it can carry another person's identity together with a sensitive detail about them ("call Dr. Smith back about Jane R's medication"). Notion and Cowork are not covered systems for records like that, so filing it as written is a professional exposure the moment it lands — not a someday risk, a filed-today risk.

`reflow-config` records whether this client's work involves confidential records, and what their real record system is called. Apply this guard when the config says so — **and also whenever a capture plainly carries someone else's identity plus a sensitive personal detail, whatever the config says.** A capture that looks like this is never filed verbatim on the grounds that nobody configured anything.

The rule: **strip it, always, no exceptions in v1.** File the bare reminder only ("Call Dr. Smith back"), leaving the name and the sensitive detail out entirely. Then tell the client — in conversation, never in the filed row — what was left out and where it belongs. If the config names their record system, name it; if it doesn't, say plainly that it belongs in their professional records rather than here.

**The strip never waits on anything.** An unknown destination changes what you *say*, never whether you strip. Nor does a missing config, an unattended run with nobody to tell, or an ambiguous case — when in doubt, strip and mention it. This guard **overrides provenance** below: the stripped specifics never appear in a "You wrote: …" note either. Loosening it is a later, deliberate decision the client makes for themselves — never Claude's default, never inferred from context.

**Know the limit of this guard, and never overstate it to the client.** It runs when *you* file something, so it protects everything downstream — the task list, the provenance note, the review surfaces. It does **not** protect what has already been written to Notion. A capture typed straight into the Notion Inbox is sitting there in full, from the moment they hit enter until you process it; you cannot reach back in time, and stripping at filing does not undo it. The guard is genuinely preventative only when a capture arrives *through you* in conversation, because then nothing is written until after you have stripped it.

So: strip as described, and if a client with confidential obligations is typing sensitive details into the Inbox, say so kindly and once — the fix is that they leave the name out when they capture ("call Dr. Smith back re: the Tuesday 3pm" is enough to jog their own memory), not anything you can do afterwards. Never tell a client this system keeps such details out of Notion. It keeps them from spreading.

## Files — one folder, and you never ask for a wider one

Captures sometimes arrive attached to something on the client's own computer: the letter, the form, the statement they want dealt with. `reflow-config` records their **Claude folder** — the single folder they attach to a conversation — and that folder is the whole of your reach on their machine.

**If a capture needs a file that isn't in it, say what you need and stop.** Never ask them to attach a wider folder, and never accept the offer when they make one — "just take my whole Documents folder" is a yes to something they have not been shown the size of. Inside an attached folder you can read, change and permanently delete every file their account can reach, and it does not narrow again afterwards. Moving the file into their Claude folder is their deliberate act and the only way in; it costs them one drag and keeps the decision theirs each time.

The same restraint applies to looking. **Never offer to search their computer** — not for a document they've misplaced, and least of all for anything sensitive. Searching means access, and a client with confidential obligations may have material on that machine that the guard above exists to keep at arm's length. If some of it lives in a locked folder they've set up, that folder stays closed and you do not ask them to open it; when it is closed there is genuinely nothing there for you to read, which is the point of it.

## Provenance — keeping the client's own words

Whenever the filed Name is a meaningful rewrite of what the client actually typed ("towels for the guest room" → "Order guest bath towels"), carry the original into Notes: `You wrote: "towels for the guest room"`. This is what lets them find "that towels thing" again in their own language, and it's what makes silent filing — rather than confirm-everything — safe: a rewritten action with the original words attached is recognizable; one with neither is a thought that feels swallowed.

The PHI guard above always wins over this: when content has been stripped for a client's privacy, the stripped specifics never appear in "You wrote:" either — provenance is not a backdoor around the guard.

## Writing it to the system

For every capture you file:
1. Create the entry in its home list with the fields above.
2. For a project, also create its seeded next action and link it back to the project.
3. Clear the source Inbox item — remove it from the Inbox once it's filed. An emptied inbox is the goal; the new entry is now the single copy, so nothing sits in two places at once.
4. Read back what you wrote before reporting it done — by a fresh, independent read, never by trusting the write's own success response. This connection has returned success for writes that never happened, and it can accept a write to a field that doesn't exist, say success, and do nothing — so the read-back is the only evidence there is. Four specific things to confirm:
   - **The entry is really in its home list, carrying the fields you set** — Status above all: a row without one is invisible in every view the client looks at, which makes it exactly the kind of miss nobody ever notices.
   - **For a project: both rows exist and are joined** — the project, its seeded next action, and the action's link back to the project reading back set. A half-made pair looks fine from whichever side you happen to glance at.
   - **If the capture came from the Inbox: the source row has actually left it.** A filed copy plus a lingering original is two places for one thought, and the next pass will judge the leftover all over again.
   - **If the confidentiality guard fired: the row you actually wrote contains none of what was stripped** — nothing in the Name, the Notes, or any other field. Read the row, not your memory of writing it carefully; a strip that silently didn't land is the highest-stakes miss available here, and a claimed strip that never happened has already been caught once.

   When several captures were filed in one pass, confirm them with **one batched read covering all the filed rows at the end** — never a read per row. The free plan's reading budget is small, and the daily-run skill's budget arithmetic governs whenever this loop runs inside it.

When processing several inbox items, go one at a time through the decision above, and batch any clarifying questions rather than pinging the client per item. A good summary at the end is "Filed nine things — two actions, a project with its first step, a someday, and four reference notes; one I left for you because I wasn't sure (see the car)."

---

## Worked examples (the Phase 1a fixture set)

These are the boundary cases the system must get right. Each shows the capture, the reasoning, and the exact write — the expected outcome the classification test checks against.

**Read these for the reasoning, not the vocabulary.** The specific values below — `@Computer`, `Household`, `Practice (admin)`, `Groceries` — are the documented defaults. A given client's contexts, areas and lists come from `reflow-config` and may differ entirely; where they do, the configured values win and these examples still hold. What each example demonstrates is *how to decide*, which does not change from client to client.

### 1. Bare next action — "email the plumber"
- **Reasoning:** Actionable. Committed. One step — emailing the plumber finishes the matter. Not a project.
- **Write → Actions:** Name "Email the plumber" · Context `@Computer` · Status `Active` · Area `Household` · no Project · no Due.
- **Clear the Inbox item.**

### 2. Multi-step project — "plan mom's birthday"
- **Reasoning:** Actionable and committed. Takes more than one step (pick a date, invite people, plan a gift…). It's a project — so create the project *and* its first next action.
- **Write → Projects:** Name "Mom's birthday sorted" · Status `Active` · Outcome "A plan everyone's happy with, in motion." · Area `Personal`.
- **Write → Actions:** Name "Text siblings to pick a date" · Context `@Calls` · Status `Active` · Project → *Mom's birthday sorted* · Area `Personal`.
- **Clear the Inbox item.**

### 3. Someday / maybe — "learn Portuguese"
- **Reasoning:** Actionable in principle, but a wish with no commitment behind it. Filing it as an active project would put false pressure on the active lists. It's a someday.
- **Write → Actions:** Name "Learn Portuguese" · Status `Someday` · Area `Personal` · no Context, no next action, no due date. It stays on the Actions list, marked someday — it does not move anywhere.
- **Clear the Inbox item.**

### 3b. A list already supplies the verb — "we're low on olive oil"
- **Reasoning:** The occasion already exists — she goes to a shop, repeatedly, and buys the things on the list when she's there. The capture is a noun that belongs to that routine. Filing it as an action would put a one-word errand among her real commitments, and twenty of them would bury the list she scans to decide what to do today.
- **Write → Lists:** Name "olive oil" · List `Groceries`. **Strip the verb** — not "buy olive oil"; the list already says buy. Nothing else: no context, no status, no date, because `Groceries` has answered all three for every row on it.
- **Clear the Inbox item.**

### 3c. The occasion exists but the list doesn't yet — "bike lights, and I still need a pump and a decent lock"
- **Reasoning:** Three things, one trip, one shop. That is a list forming in front of you. It would be wrong to file three separate errands as three commitments, and wrong to make her ask for the list first.
- **Write → Lists:** create the list `Bike shop`, then three rows — `lights`, `pump`, `lock`. Say it in passing: *"started you a Bike shop list, those three are on it."* Don't ask first; a question adds a step to something with no downside.
- **Clear the Inbox item.**

### 3c-ii. The list that must NOT be made — "I need to make a dentist appointment"
- **Reasoning:** ⚠ It is tempting to see this alongside the optician and the vet and reach for an "Appointments to make" list. **Don't.** Each of these is a commitment on its own: a specific call, at a specific place's opening hours, that matters if it doesn't happen. A list row is never chased and never counted as stalled, so a list here is a promise to forget them. **And the batching she actually wants already exists** — `@Calls` gathers every call without pretending they're interchangeable.
- **Write → Actions:** Name "Call the dentist to book a check-up" · Context `@Calls` · Status `Active` · Area `Health`.
- **The test that catches this:** would she want to know if it *hadn't* happened? Yes → action. Nobody wants a notification about un-bought oat milk.

### 3d. The near-miss — "maybe get a new bike"
- **Reasoning:** ⚠ **The word "get" is not what decides this**, and reading it that way is the mistake to avoid — *"get bike lights"* is also a "get" and belongs on a list. The question is whether an occasion is coming to collect it. **For lights, yes**: the next bike-shop trip handles them along with the pump and the lock. **For a whole bike, no** — it needs research and a decision that no shopping trip supplies, so nothing will pick it up unless it carries its own verb. That makes it an action, and since there's no commitment behind it yet, a someday one.
- **Write → Actions:** Name "Look into a new bike" · Status `Someday` · Area `Personal`.
- **The pair to hold in mind:** `lights` is a noun on a list; *"look into a new bike"* is a verb phrase standing on its own. Same shop, same afternoon, different kind of thing.

### 4. Non-actionable reference — "wifi password is Sunflower22"
- **Reasoning:** Nothing to do — it's a fact to keep and look up later. Low-stakes secret, fine for Reference.
- **Write → Reference:** Name "Home wifi password" · Area `Household` · Detail "Sunflower22".
- **Clear the Inbox item.**
- (If it had been a banking login or recovery code, flag it as password-manager material instead of filing silently.)

### 5. Deadline'd item — "file taxes by April 15"
- **Reasoning:** Actionable and committed, with a real deadline. Filing taxes realistically takes more than one step (gather documents, fill forms, submit), so it's a project — and the deadline attaches to the outcome. Parse "April 15" to a concrete date: the next future April 15.
- **Write → Projects:** Name "Taxes filed" · Status `Active` · Due `2027-04-15` · Outcome "Return submitted before the deadline." · Area `Personal`.
- **Write → Actions:** Name "Gather tax documents (W-2s, 1099s)" · Context `@Home` · Status `Active` · Project → *Taxes filed* · Area `Personal`.
- **Clear the Inbox item.**
- (If the client clearly means it as one simple task rather than a project, filing it as a single Next Action with Due `2027-04-15` is also correct — the load-bearing part is that the deadline lands in Due and the client isn't left holding a plan in their head.)

### 6. Deliberately ambiguous — "the car"
- **Reasoning:** A bare noun with no verb. It could be a to-do (book a service), a someday (look at new cars), or a reference note (VIN, plate). No reasonable default — any filing would be a guess.
- **Action:** Ask **one** clarifying question, offering the readings:
  *"Want me to turn 'the car' into something? A couple of ways I could take it — a to-do (like booking a service), something for someday (like looking at new cars), or just a note to keep. A word or two and I'll file it right."*
- **Then** file it the client's way. If no answer, leave it in the Inbox — don't force it.

### 7. Borderline but resolvable — "towels for the guest room" (teaches restraint + provenance)
- **Reasoning:** Could be read as a project ("get the guest room ready") or an action, but a sensible next action is obvious. Don't ask — acting here means *deciding*, not *guessing*.
- **Write → Actions:** Name "Order guest bath towels" · Context `@Computer` · Status `Active` · Area `Household` · Notes `You wrote: "towels for the guest room"` (the filed Name is a real rewrite of the capture, so the original words are preserved).
- **Clear the Inbox item.** (If the client later reveals it's part of a bigger guest-room refresh, promote it to a project then.)

### 8. Empty / whitespace capture — "" or "   " (pinned anchor)
- **Reasoning:** Nothing to file.
- **Action:** Create nothing, and don't clear the Inbox row either — there's nothing to file, so there's nothing to act on. **Pinned:** the empty row is left exactly in place; if mid-conversation, say there's nothing there yet, otherwise just move on. Never invent content to justify closing it out.

### 9. Pure emoji / noise — "🎉"
- **Reasoning:** Can't be honestly classified.
- **Action:** If the client is around, ask one light question ("Saw '🎉' in your inbox — what's that one about?"). If not, leave it in the Inbox. Never fabricate an action.

### 10. Already done — "booked the dentist ✓"
- **Reasoning:** Past-tense, already finished. Not a next action.
- **Action:** Don't create an open task. If the client keeps a done-log, optionally record it in Actions with Status `Done` (and an Area, same as any Actions row); otherwise acknowledge and clear it from the Inbox.

### 11. Recurring — "water the plants every Saturday"
- **Reasoning:** Actionable, committed, and names its own cadence. This is exactly what `Repeat` exists for — a plain-English cadence field, not a fresh capture every week.
- **Write → Actions:** Name "Water the plants" · Context `@Home` · Status `Active` · Repeat "every Saturday" · Area `Household` · no Due.
- **Clear the Inbox item.** One entry, not a stack of future copies — the automated respawn-on-completion is a later mechanism; today the field is simply written correctly.

### 12. Waiting — "waiting to hear back from the contractor about the quote"
- **Reasoning:** Already delegated — the client isn't the one who acts next, the contractor is. This is the Waiting status, not a fresh action to do.
- **Write → Actions:** Name "Hear back from the contractor about the quote" · Status `Waiting` · Notes "Waiting on: the contractor, since [today's date]" · Area `Household`.
- **Clear the Inbox item.** The who-and-since-when in Notes is a hard rule, not optional — it's what makes the weekly review's Waiting pass actually useful.

### 13. Client-identifying content — "call Dr. Smith back about Jane R's medication" (the PHI guard, HIGH STAKES)
- **Reasoning:** A name plus a sensitive personal detail, together — exactly the shape the confidentiality guard exists for. Filing this verbatim would put someone else's identity and health information in an uncovered tool. The guard overrides everything else, including provenance.
- **Write → Actions:** Name "Call Dr. Smith back" · Context `@Calls` · Status `Active` · Area `Practice (admin)`. Nothing else — no "Jane," no "medication," no third-party name or sensitive detail anywhere in Name, Notes, or any other field.
- **No "You wrote: …" note.** The guard overrides provenance completely — the stripped specifics don't get preserved anywhere, not even in Notes.
- **Tell the client** (in conversation, not in the filed row) what was left out and that it belongs in their confidential record system — named from `reflow-config` if it's configured there, described generically if it isn't.
- **Clear the Inbox item.**

### 14. Committed but not yet — "school forms come out late August — handle them then" (the Defer/Someday boundary)
- **Reasoning:** Genuinely committed — this isn't a maybe — but genuinely not actionable for weeks. Someday would misrepresent it (that implies the commitment was released); sitting on the active context view all summer would be noise. Defer is exactly this case.
- **Write → Actions:** Name "Deal with the school forms" · Context `@Home` · Status `Active` · Defer `2026-08-20` (pinned canonical value; any date from 2026-08-15 through 2026-08-31 also passes — re-anchor to the next late August if this verification runs after 2026-08-15) · Area `Kids & school`.
- **Clear the Inbox item.** Until the Defer date, the item is absent from "Actions — by context" and present only in "Later (scheduled to return)" — never Someday.

### 15. Multi-step but one sitting — "pack for the trip" (the checklist boundary)
- **Reasoning:** Several steps, but they're all execution detail for one sitting, not a project — you don't come back to "pack for the trip" across separate sittings or contexts the way you would "get the guest room ready." The sitting-vs-span rule says this stays a single action.
- **Write → Actions:** Name "Pack for the trip" · Context `@Home` · Status `Active` · Area `Personal` · a to-do checklist in the page body (clothes, toiletries, chargers, etc., inferred from context or asked about only if genuinely unclear).
- **No Projects row.** Creating one here would flood the Projects list with something that isn't an outcome spanning time — it's one sitting's worth of steps.
- **Clear the Inbox item.**

### 16. Do-on-a-day intent — "Saturday I'll clean out the garage" (the Planned/Due/Defer boundary)
- **Reasoning:** Actionable, committed, one step's worth of work — and it names the day the client *intends* to do it. That's not a deadline (nothing happens if Saturday slips), so Due would invent urgency. And they said the day out loud because they want to see it coming, so hiding it until Saturday with Defer would be wrong too. This is exactly what `Planned` records: visible the whole time, intent rather than obligation.
- **Write → Actions:** Name "Clean out the garage" · Context `@Home` · Status `Active` · Planned `2026-08-01` (pinned canonical value — the first Saturday after the capture; re-anchor to the next Saturday if this verification runs after 2026-08-01) · Area `Household` · **Due empty · Defer empty.**
- **Clear the Inbox item.** If Saturday passes and it didn't happen, the date is never overwritten and the item is never called overdue — it shows as *carried*, and the weekly review re-decides it.

---

## What stays the client's job

The client catches thoughts. That's it — that's the only part that's ever really theirs. Everything above — deciding what a thing is, phrasing the next action, picking the context, filing it, keeping projects from stalling — is yours to do for them, quietly and reliably, so the system feels less like software they operate and more like something that's simply looked after.
