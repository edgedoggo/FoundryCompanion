# FoundryCompanion

Foundry VTT module that shows player-visible quests in a live, mobile-friendly companion page and can also export a static HTML snapshot.

This first pass targets Foundry VTT v11 and Forien's Quest Log v0.8.0. It is intentionally defensive about where quests are stored because Forien's v0.8.0 does not expose quests at `game.quests` in every world.

## What it does

- Adds **Configure Settings > Module Settings > FoundryCompanion**.
- Opens a live Foundry companion window that refreshes while it is open.
- Downloads a static `.html` snapshot when needed.
- Filters quests through Foundry permission checks when the quest/document exposes `testUserPermission`.
- Includes quests visible at `LIMITED` permission or higher.
- Groups quests by status and renders objectives, rewards, giver, location, and description where available.
- Copies a debug sample to the clipboard so we can wire the exporter to your exact Forien data shape.

## Install for local testing

1. Copy this folder into Foundry's `Data/modules/foundry-companion`.
2. Enable **FoundryCompanion** in your world.
3. Open **Configure Settings > Module Settings > FoundryCompanion**.

## Important permission note

The live page and snapshot are "as current user." If a player opens it, it should match that player's view. If a GM opens it, the GM can see nearly everything, so the page will also include nearly everything unless the underlying quest data has explicit ownership metadata.

## Why `game.quests` returned undefined

That means Forien's Quest Log v0.8.0 is storing quests somewhere else in your world. Use the **Copy quest debug sample** button in FoundryCompanion and paste the result back into Codex. The debug sample searches likely globals, Forien settings, journal flags, and known module API locations.

Then we can tighten the extractor to Forien's exact fields instead of leaning on generic guesses.
