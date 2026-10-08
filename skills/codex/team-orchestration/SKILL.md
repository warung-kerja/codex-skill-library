---
name: team-orchestration
description: Coordinate explicitly requested project work from one Astra Mastermind conversation using native subagents with task-appropriate models. Separate persistent Codex tasks are an explicit alternative. Opt-in only; not automatic on every project.
---

# Team orchestration

## Activation and preferred mode

Use only when explicitly invoked, for example: “Use $team-orchestration for this project.” Do not activate for all projects. Inspecting or updating this skill does not request new agents or implementation work.

Keep the current conversation as **Mastermind**, the user's sole point of contact. The user's preferred Mastermind model is **Astra**; do not silently change the parent model or claim this skill can change it. When another model is active, disclose the mismatch if relevant.

**Native subagents are the default.** Delegate bounded tasks directly from Mastermind, collect their results, review and integrate. Role names describe responsibilities; they do not require permanent workers or a separate Orchestrator layer. Do not create sidebar tasks, recurring automations, worker ledgers or a polling loop merely to enable delegation. If the user requests setup without an implementation objective, record the chosen workflow and remain idle.

## Model routing

Choose the route from the user's explicit invocation. Ordinary invocation uses the standard route below. Select **cheap / save-quota mode** only when the user explicitly requests it, for example “use team orchestration skill for cheap” or “use $team-orchestration to save quota.” Generic efficiency discussion or an unavailable standard model does not activate this mode. Keep Astra as Mastermind in both routes; this changes delegated model selection, not the parent model. These are routing preferences, not a guarantee of measured savings.

### Standard route and roles

Model choices checked on **2026-10-09** against [Codex model guidance](https://learn.chatgpt.com/docs/models) and the active Codex tool schemas. The role assignments below are this skill's workflow preferences.

| Role | Responsibility | Preferred model | Starting effort |
| --- | --- | --- | --- |
| Mastermind | Scope, architecture, tradeoffs, integration and final acceptance | `gpt-6-astra` in the current conversation | Preserve the current setting; medium for a new substantial task, high/xhigh for demanding decisions |
| Orchestrator / Builder | Implement features, investigate bugs and coordinate an assigned workstream | `gpt-6.1-sol` | medium for routine implementation; high for complex work |
| Independent Reviewer | Examine a separate worker's result, find regressions and assess acceptance evidence | `gpt-6.1-sol` | high |
| Muscle | Precise edits, focused coding, extraction and bounded checks with clear acceptance criteria | `gpt-6-luna` | low for mechanical edits; high for focused coding or checks |

Use roles as needed; do not create one worker per table row. The Mastermind can implement small tasks and review ordinary results directly. A useful independent reviewer gets a separate context and evidence; it need not use a different model. Keep ambiguous architecture and unresolved high-impact findings with the Mastermind. Give Luna a bounded task; use Sol for work requiring broader judgment.

GPT-6.1 Sol replaces the older Sol/Terra defaults for implementation and review. GPT-6 Luna handles focused work. Older models may remain selectable, but use them only when explicitly selected or already approved for that project. These preferences do not change the current parent model.

### Explicit cheap / save-quota route

Preserve the user's separately requested provider route:

| Work | Requested provider model | Effort guidance |
| --- | --- | --- |
| Standard coding and mechanical edits | `deepseek-v4.1-flash:cloud` | supported effort appropriate to the task |
| Higher-reasoning work or bounded orchestration | `kimi-k3:cloud` | high if supported |

These are provider-specific preferences, not models verified as available in the current native Codex tools. Use this route only if the active execution tool/provider explicitly supports those exact IDs and the user has authorized that execution surface. DeepSeek v4 is not a substitute for v4.1. If unavailable, report that limitation and ask before switching to the standard route; do not create a provider integration to satisfy the request. Keep Astra as the preferred Mastermind in both routes. Model and effort choices alone do not prove subscription quota or cost savings.

### Availability and effort

Before dispatch, inspect the tool's current supported models, reasoning efforts and target host. Use exact advertised IDs; do not probe unlisted model names based on historical launch acceptance. If a preferred model is unavailable, use an already authorized alternative or ask for the missing choice. An ambiguous launch must be inspected before retrying.

The tool/client is authoritative for available effort values. Use `low`, `medium` or `high` as above; raise to `xhigh` only when task difficulty warrants it and the tool supports it. Do not enable Max/Ultra or extra workers by default. API reasoning options and desktop options can differ.

Distinguish **model requested**, **launch accepted**, **result returned**, and **execution model verified**. Agent self-identification is not verification. Report execution model as unverified when authoritative runtime metadata is absent. Do not silently inherit the parent model when a lower-tier worker was requested.

When overriding a native agent model, use the tool-supported minimal context fork (none or a bounded number of turns). Provide a self-contained brief and relevant file paths. Use a full-history fork only when permitted without an incompatible override.

For future refreshes, consult [current model guidance](https://learn.chatgpt.com/docs/models) and [model selection](https://developers.openai.com/api/docs/guides/model-selection), then confirm support in the execution tool. Do not infer the next model ID from version naming.

## Dispatch and ownership

Read project AGENTS.md and the relevant plan first. Inspect live agents before reusing or spawning work. Every delegated task should have:

- A concrete objective and bounded output, independent of useful work Mastermind can do concurrently.
- Relevant context, input paths, writable paths or read-only scope, and acceptance checks.
- Authorization limits and a reporting destination.

Native agents may share the checkout: assign disjoint write ownership, account for uncommitted changes, and do not run conflicting writes. If isolation is needed, explicitly establish worktrees and integration ownership. Never assume a native agent gets an isolated filesystem. Keep within tool concurrency limits and avoid speculative or ceremonial workers.

Workers may fix routine bugs and necessary adjacent issues inside the assigned objective without asking Mastermind for every small repair. Escalate material scope/architecture changes, repeated failures (normally two unsuccessful repair rounds on the same blocker), and new authorization needs. Use independent review when meaningful, not for every label or formatting change. Paid generation, ambiguous retries, deployment and destructive changes remain bounded by actual user authorization.

Report once on a completed deliverable or meaningful blocker, with changed paths, checks and limitations. Batch routine repair details. Mastermind inspects the result and performs appropriate integration/verification before claiming completion. Do not merely dispatch work and label it delivered. Native work is tied to the current tool/runtime lifecycle; do not promise unattended future resumption or invent a heartbeat to keep it alive.

## Durable state and optional persistent mode

For substantial work, use the project's existing plan/queue and a short team-workflow note. Record model requests and verification limits when useful. Do not create a full multi-task ledger structure for a small native assignment. Keep mutable project state, IDs, paths and secrets out of this global skill.

If the user explicitly asks for persistent separate Codex tasks, read [Separate-task mode](references/separate-tasks.md). This mode is useful for independently resumable work across days. It is not an automatic fallback when a native model is unavailable. Discover/reuse existing tasks before creation. Never archive old tasks or alter existing automations solely because native mode is now preferred; do so only within the user's authorization. Preserve paused goals and timers.

If documenting durable preferences in a shared Wiki, follow its contributor rules: a sourced raw handoff for its curator, not project progress duplicated as global knowledge. Wiki stores preference and rationale; this skill stores procedure; project docs store execution state.

## Invocation

“Use $team-orchestration for this project. Keep Astra as Mastermind and delegate suitable work to native subagents.”

For cheap mode: “Use $team-orchestration to save quota.” This selects Kimi K3 / DeepSeek v4.1 Flash for delegated work, with Astra remaining Mastermind.

For the alternative: “Use $team-orchestration with separate persistent Codex tasks.”
