# Codex Usage Visibility: Project and Task Attribution

## Product Decision

Add opt-in usage attribution directly beneath projects and tasks in the ChatGPT Windows app's Codex sidebar. A pinnable global allowance bar remains useful supporting context, but this proposal answers the more actionable question: **which work used my allowance?**

This extends, rather than duplicates, the persistent global visibility requested in [openai/codex#24182](https://github.com/openai/codex/issues/24182) and [openai/codex#30216](https://github.com/openai/codex/issues/30216).

## Evidence

- Discussion on [#24182](https://github.com/openai/codex/issues/24182) distinguishes persistent five-hour and weekly limits from the existing context-window status, validating the need to keep these concepts separate.
- [#30216](https://github.com/openai/codex/issues/30216) reinforces demand for an always-visible allowance and reset indicator.
- A July 13 usage-accounting report, [#32827](https://github.com/openai/codex/issues/32827), asks users to be able to identify the model, thread, and time interval responsible for consumption. It also shows why attribution may need a provisional state while delayed server-side accounting settles.

## Proposed Experience

1. **Pinned global allowance**
   Show plan allowance or credit consumption, progress, and reset time. Users can keep it pinned or collapse it. This provides orientation; it is not the proposal's primary differentiator.

2. **Opt-in sidebar attribution**
   Add the current reset-window total to each project row. Expanded projects show task totals and freshness as events arrive. A single setting hides project and task values without removing the global allowance.

3. **Task usage detail**
   Selecting a task total opens its attributed allowance, recent metering events, source, and freshness. A tagged event updates the task, its parent project, and the global allowance together.

4. **Separate context status**
   Show context-window fullness in a distinct section labeled as working memory. Never combine it with allowance, credits, billing impact, or reset timing.

## Attribution States

- **Off:** project and task totals disappear; the global allowance remains.
- **Pending:** a running task is awaiting a tagged metering event.
- **Provisional:** the event has project and task identifiers, but reconciliation is incomplete and totals may change.
- **Reconciled:** the server marks the event final and the hierarchy totals agree.
- **Unavailable:** attribution cannot be verified because official tagged events are absent.

## Data and Trust Contract

Exact attribution cannot be inferred reliably from local activity. Consumption varies with task complexity, model, context, and execution location, while current credit metering is token-based. An authoritative event needs at least:

- stable `event_id`, `project_id`, and `task_id`, plus `thread_id` where applicable;
- metered amount and unit, such as tokens or credits;
- model and execution location metadata;
- `occurred_at` and `received_at` timestamps;
- allowance reset-window identifier;
- `attribution_status`: `provisional`, `reconciled`, or `adjusted`.

The prototype simulates these events. Every simulated value is labeled, and local estimates must never appear as billing-authoritative data.

## Acceptance Criteria

- With attribution enabled, a user can identify the project and task behind recent consumption from the sidebar.
- A tagged event updates the selected task, parent project, and global total in one interaction.
- Delayed data is labeled provisional until reconciliation; adjusted totals preserve source and freshness.
- Hiding attribution removes project and task totals without removing the global allowance.
- Allowance consumption and context-window fullness remain visually and semantically distinct.

## Prototype Boundary

Deliver a single-screen mockup with a normal attributed view and an incoming provisional-event view. No production backend, persistence, account integration, or local usage estimator is in scope. Publication requires Alexander's review and explicit approval.
