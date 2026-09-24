# Configure journey settings

Use when the user wants audience, schedule, goal, rename, or description changes on an existing journey
(`references/identify-journey.md` first).

Only run steps the user asked for (or explicitly confirms now). Follow each set tool's workflow in its MCP
description — do not duplicate parameter rules here.

---

## Audience — `Pendo:setOrchestrateJourneySegment`

Follow `Pendo:setOrchestrateJourneySegment`'s **`WithWorkflow`** in its MCP description — do not guess `segmentId`.
In practice:

1. `references/identify-journey.md` — resolve `journeyId` (and `subId` / `appId` if needed).
2. **`Pendo:segmentList`** — pass a `substring` from the user's segment name or phrase (e.g. "power users"). Do not
   pass a display name as `segmentId`.
3. **One match** — use that segment's `id`. **Two or more** — STOP; list candidates (`id`, `name`) and ask the
   user to pick. **Zero matches** — see segment creation below (or ask for a different name).
4. **`Pendo:setOrchestrateJourneySegment`** — `journeyId` + chosen `segmentId`. Pass `reachInactiveVisitors` or
   `retainVisitorsAfterEntry` only when the user explicitly asked; omit otherwise.

Map plain language to segment flags when the user asks:

| User might say | Parameter |
|----------------|-----------|
| "include inactive visitors", "new signups without activity yet" | `reachInactiveVisitors: true` |
| "entry segment only", "don't kick people out if they leave the segment" | `retainVisitorsAfterEntry: true` |
| "must stay in the segment", "drop if they leave the segment" | `retainVisitorsAfterEntry: false` |

### Segment creation (when `Pendo:segmentList` returns zero matches)

If the user wants a **new saved segment** and `Pendo:buildPendoSegment` / `Pendo:createSegment` are on your MCP tool list:

1. Draft audience rules with the user in plain language.
2. **`Pendo:buildPendoSegment`** — validate the definition; read the tool description for the `definition` shape.
3. Confirm the segment name and rule summary with the user.
4. **`Pendo:createSegment`** — persist; use the returned `id` as `segmentId`.
5. **`Pendo:setOrchestrateJourneySegment`** — attach to the journey.

If those tools are not on your tool list, say you have no MCP tool to create segments — user can create one in
Pendo and retry with the segment name.

---

## Schedule — `Pendo:setOrchestrateJourneySchedule`

**Tip:** aim for the top of the hour (`:00`) when setting a start time — reduces friction at activation (not
enforced by MCP).

---

## Goal — `Pendo:setOrchestrateJourneyGoal`

Search for the goal (page, feature, or track event) with `Pendo:listCountables` or `Pendo:searchEntities` per the tool's
`WithWorkflow`, disambiguate if multiple matches, then set — do not guess `itemId`.

---

## Name and description

Use `Pendo:setOrchestrateJourneyName` and `Pendo:setOrchestrateJourneyDescription` — read each tool's MCP description when
you call it.

After configuration, summarize what was set. Do not claim the journey is ready to activate — see
**Do not infer unobservable state** in `SKILL.md`. Use `references/handoff.md` if the user asks about go-live.
