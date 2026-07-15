# Codex Usage Visibility Proposal

Codex users can see how much allowance remains, but a global number cannot answer the practical question: **which project or task used it?** This proposal adds opt-in attribution to the existing project and task hierarchy in the ChatGPT Windows app.

## The Proposal

- Keep a pinnable global allowance bar for remaining usage and reset timing.
- Show reset-window totals beneath each project and task in the sidebar.
- Update the task, parent project, and global allowance together when tagged usage events arrive.
- Label delayed data as provisional until metering reconciliation completes.
- Keep allowance or credit usage visibly separate from context-window fullness.
- Require tagged official events for authoritative attribution; never present local estimates as billing data.

The global bar complements [openai/codex#24182](https://github.com/openai/codex/issues/24182) and [openai/codex#30216](https://github.com/openai/codex/issues/30216). The distinct contribution is project- and task-level attribution. The delayed accounting described in [openai/codex#32827](https://github.com/openai/codex/issues/32827) motivates an explicit provisional state.

## Review Package

- [Live interactive mockup](https://h4xofficial.github.io/codex-usage-attribution-proposal/)
- [One-page UX specification](usage-visibility-spec.md)
- [GitHub issue draft](github-issue-draft.md)
- `usage-visibility-mockup.png`: normal attributed view
- `usage-visibility-provisional-event.png`: incoming provisional event

Open `index.html` directly in a browser. The controls switch between simulated, provisional, and reconciled-event states; receive a deterministic tagged event; reset the state; hide attribution; and collapse the global bar.

Repeatable capture states:

- Normal attributed view: `index.html?capture=1`
- Incoming tagged event: `index.html?state=event&capture=1&toast=1`
- Reconciled event detail: `index.html?state=official&capture=1`

Recommended capture size is 1440 x 900. Use the first two states in the issue; keep the reconciled state available for review or a short interaction recording.

## Trust Boundary

This is a frontend interaction prototype, not a billing estimator. Exact attribution requires official metering events tagged with stable project and task IDs. No backend, account connection, persistence, or production metering logic is included.

## Status

The proposal repository and interactive prototype are public. The approved request was published as [openai/codex#33433](https://github.com/openai/codex/issues/33433) on July 15, 2026.
