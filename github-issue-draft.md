# Proposed GitHub Issue

**Title:** Codex Desktop: opt-in usage attribution by project and task

## Feature Request

### Summary

Add opt-in usage attribution beneath projects and tasks in the Codex Desktop sidebar. A pinned global allowance indicator answers "how much is left?"; project and task totals answer the harder question: "which work used it?"

### Problem

The current global usage view cannot explain a spike or help users budget allowance across concurrent projects. Recent reports also describe delayed accounting, which makes local inference unreliable and can leave users unable to identify the thread or time interval responsible for consumption.

### Proposed UX

- Keep a compact, pinnable global allowance and reset indicator.
- Add reset-window totals to project rows, with task totals shown when a project is expanded.
- Make attribution opt-in so users can preserve a quieter sidebar.
- Show source and freshness in task usage detail.
- Label newly tagged events as **provisional** until server-side reconciliation completes.
- Keep context-window fullness in a separate working-memory section, never combined with plan or credit usage.

### Data and Trust Requirement

This should use official metering events tagged with stable project and task identifiers. Local token or activity estimates should not be presented as authoritative billing data. A useful event contract would include event, project, task, and optional thread IDs; metered amount and unit; model; execution location; event and receipt timestamps; reset window; and reconciliation status.

### Acceptance Criteria

- A user can identify the project and task behind recent consumption from the sidebar.
- A tagged event updates the task, parent project, and global total together.
- Delayed values remain visibly provisional until reconciled or adjusted.
- Hiding attribution removes project and task totals without removing the global allowance.
- Context-window fullness remains visually and semantically separate from allowance usage.

### Relationship to Existing Requests

- [#24182](https://github.com/openai/codex/issues/24182) and [#30216](https://github.com/openai/codex/issues/30216) request persistent global usage visibility.
- [#32827](https://github.com/openai/codex/issues/32827) describes delayed or unclear accounting and asks to identify the responsible model, thread, and time interval.

This request does not duplicate the global indicator. Its focus is attribution within the existing project and task hierarchy, including honest handling of delayed data.

### Prototype

- [Interactive prototype](https://h4xofficial.github.io/codex-usage-attribution-proposal/)
- [One-page UX specification](https://github.com/H4XOFFICIAL/codex-usage-attribution-proposal/blob/main/usage-visibility-spec.md)

Normal attributed view:

![Normal attributed view](https://raw.githubusercontent.com/H4XOFFICIAL/codex-usage-attribution-proposal/main/usage-visibility-mockup.png)

Incoming provisional event:

![Incoming provisional event](https://raw.githubusercontent.com/H4XOFFICIAL/codex-usage-attribution-proposal/main/usage-visibility-provisional-event.png)

All prototype values are simulated and visibly labeled.
