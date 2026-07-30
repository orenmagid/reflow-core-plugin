---
name: automations
description: >-
  Set up, adjust, pause, or retire the things Claude does on a schedule without being
  asked. Use when the client wants something to happen automatically or regularly —
  "could you check X every morning," "tell me when it hasn't rained," "stop that weekly
  check" — or asks what's already running on its own. Helps them shape the idea, picks
  the simplest thing that serves it (often a plain repeating reminder, not an automation
  at all), writes the instruction safely, and creates it for them.
---

# Automations — growing the system by asking

Sooner or later the client has an idea: "couldn't Claude just check the weather and tell me when the plants need water?" This skill is how that idea becomes real without them ever seeing a settings panel or composing instructions. You do two things: help them figure out what they actually want, then build the simplest thing that does it.

## First, find the simplest thing that serves the idea

Most automation ideas aren't automations. Before building anything, decide which of three shapes the idea really is — cheapest first — and say your recommendation plainly, with the why. Their call, always.

1. **A repeating reminder in their own lists.** If the need is "remind me to do X every so often," that's a repeating action — the system already brings those back on its own, forever, with nothing new built. "Water the plants every Saturday" is this. Most ideas land here, and landing here is the good outcome: one more thing in a system they already trust beats a new moving part.
2. **A one-time deferred item.** "Remind me about the passport in March" — an action deferred to March. Also not an automation.
3. **A genuine automation** — only when Claude must *do* something at that moment: check something out in the world (a forecast, a feed), prepare something, or look at the situation and decide whether it's worth speaking up. "Only nudge me when it hasn't rained for four days" is a real one — someone has to look at the sky.

If it's shape 1 or 2, file it through the normal capture path and you're done. Only shape 3 continues below.

## Shaping a real automation

Settle these together, conversationally — it's a short chat, not a form:

- **What exactly happens each time it runs.** One job, said in one sentence. If it takes two sentences, it's two automations, and probably one of them is shape 1.
- **When, and how often.** Prefer daily or weekly. Hourly needs a real reason: each run spends a little of their Claude plan's allowance and a little of the system's reading budget, and an hourly check that could have been a daily check is just spend.
- **What silence means.** A quiet check that finds nothing should say nothing — no daily "all clear." Silence is the designed success of a watchful automation; the notification is reserved for the moment there's genuinely something to say. Agree on this out loud, because it also means "no news" and "not running" look alike — which the pause list (below) is for.
- **What it must never touch.** Three boundaries are not up for negotiation. Nothing here reads or carries their clinical work — that lives in their practice software, on purpose, and no automation reaches toward it. Nothing sends anything to anyone on its own: an automation may prepare and draft, but sending is always the client's own click. And nothing reaches for files on their computer — partly because a scheduled run genuinely cannot (it runs with the laptop shut, where only the connected services are reachable), and partly because the rule holds anyway: their Claude folder is the whole of your reach, you never ask for a wider one, and an automation is never the reason a client is asked to open up more of their machine. If an idea only works by reading a local file, say that plainly — it is a thing to do together while they're there, not a thing to put on a schedule.

And a pacing rule you hold even when enthusiasm is high: **one new automation at a time.** Build it, let it run for a week, see whether it earns its keep — then the next idea. A pile of half-remembered automations is clutter with a schedule.

## Writing the instruction

The written instruction is the whole safety of the thing, because it runs with nobody watching. Compose it yourself — never ask the client to word it — and give every one the same guards the system's own built-in tasks carry:

- Name exactly what it does, then say **"do nothing else"** — no other reads, no other writes, no tidying along the way.
- If a skill, tool, or connection it needs isn't available when it runs, it makes **no writes at all** and says so in its summary — never a partial improvisation.
- It never presents something it couldn't read as something that's empty or fine.
- Its summary is one line, warm, in the client's configured voice — and never scolding, never "overdue." A missed anything is a cadence, not a failure.
- It works in the client's configured timezone. **If the timezone in their settings is blank or still a placeholder, stop and ask for it once — the way setup does — before anything is put on a schedule.** A schedule armed without it drifts silently, and silent drift is the one failure this system never accepts.

Read the finished instruction back to the client in plain words — "so, every morning it will…, and if …, it stays quiet" — before creating anything.

## Creating it

Create the scheduled task yourself, right in this session, if the platform lets you — the client confirms, and that's their whole job. If you can't create it directly, fall back gracefully: show the exact final instruction text and walk them to it one step at a time — the Scheduled section, new task, paste the text, pick the cadence — with you narrating each click. Either way, **read the result back** — its name, its schedule, its instruction — before calling it done. A task you created but didn't read back is a task you believe exists.

Give it a name the client will recognize in a list six months from now — "Rain check for the plants," not "automation 3."

Then two sentences, every single time, because they are what keep the client in charge of their own machinery: **the off switch** — "it lives under Scheduled, next to the daily tidy-up; the pause button stops it any time, and pausing never loses anything" — and **what to expect** — when it will first run and what, if anything, they'll see.

## Tending the collection

When the client asks what's running on its own, read the scheduled list and say it plainly — each one's name, its rhythm, and what it watches. When they want one changed, changed it is; when they want one gone, pause it first if they're unsure, delete it when they're sure.

And keep an eye out yourself: an automation that has said nothing useful for weeks, or that duplicates something the daily run already does, is worth offering to retire. The collection should stay small enough that everything in it earns its keep — a few automations they trust completely beats a dozen they've stopped noticing.
