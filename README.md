# reflow-core

The client-facing Claude Cowork plugin for a personal, AI-assisted task system that lives in the client's own Notion.

**This repo is published output. Do not edit it by hand.**

The source of truth is `core/` in the private factory repo, which also holds the design record, the Notion schema specification, and the plans — none of which should ever reach a client. Publishing is one command there: `./scripts/publish-plugin.sh`. Editing here would be silently overwritten by the next publish.

## Installing

Add this repo as a plugin marketplace in Claude Cowork, then install `reflow-core` from it.

## What's inside

Four skills — capture, the daily run, the weekly review, and setup — plus a declared Notion connector. No client data, ever: this carries system logic and structure only.
