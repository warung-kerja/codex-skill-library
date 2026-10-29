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

Use the model routing below, subject to the selected tool and host advertising the exact model. Requests to save cost or quota mean choosing the smallest suitable worker, keeping assignments bounded and avoiding unnecessary delegation. Keep Astra as the preferred Mastermind; worker selection does not change the parent model. These are routing preferences, not a guarantee of measured savings. A specific user model override takes precedence.

### Models and roles

Model availability checked on **2026-10-29** against the active native `spawn_agent` and Codex app dispatch tool schemas. This is a local availability snapshot, not a claim about public releases or measured model performance. The role assignments below are workflow preferences.

| Role | Responsibility | Preferred model | Starting effort |
| --- | --- | --- | --- |
| Mastermind | Scope, architecture, tradeoffs, integration and final acceptance | `gpt-6-astra` in the current conversation | Preserve the current setting; medium for a new substantial task, high/xhigh for demanding decisions |
| Orchestrator / Builder | Implement features, investigate bugs and coordinate an assigned workstream | `gpt-6.1-sol` | medium for routine implementation; high for complex work |
| Optional coding specialist | Bounded coding or investigation when a Codex-focused worker is useful | `gpt-6.1-terra` | medium for routine coding; high for complex work |
| Independent Reviewer | Examine a separate worker's result, find regressions and assess acceptance evidence | `gpt-6.1-sol` | high |
| Muscle | Precise edits, focused coding, extraction and bounded checks with clear acceptance criteria | `gpt-6-luna` | low for mechanical edits; high for focused coding or checks |
| Optional development worker | Bounded implementation, investigation or checks with explicit acceptance criteria and independent review | `deepseek/deepseek-v4.1-flash` when advertised by the dispatch tool | low for mechanical work; high for development |

Use roles as needed; do not create one worker per table row. The Mastermind can implement small tasks and review ordinary results directly. A useful independent reviewer gets a separate context and evidence; it need not use a different model. Keep ambiguous architecture and unresolved high-impact findings with the Mastermind. Give Luna a bounded task; use Sol for work requiring broader judgment.

GPT-6.1 Sol remains the default for implementation and review. GPT-6.1 Terra is a current Codex-model alternative for coding; its label alone does not establish that it is better or cheaper than Sol. GPT-6 Luna handles focused work. Previous-generation models are compatibility choices, used only when explicitly selected or already approved for that project. These preferences do not change the current parent model.

### Advertised models and effort snapshot

| Dispatch surface | Models | Supported efforts |
| --- | --- | --- |
| Native subagents and persistent-chat model selection | `gpt-6.1-sol`, `gpt-6-astra`, `gpt-6.1-terra`, `gpt-6-sol` | `low`, `medium`, `high`, `xhigh`, `max`, `ultra` |
| Native subagents and persistent-chat model selection | `gpt-6-luna` | `low`, `medium`, `high`, `xhigh`, `max` |
| Persistent-chat model selection only | `gpt-5.6-sol`, `gpt-5.6-terra` | `low`, `medium`, `high`, `xhigh`, `max`, `ultra` |
| Persistent-chat model selection only | `gpt-5.6-luna` | `low`, `medium`, `high`, `xhigh`, `max` |
| Persistent-chat model selection only | `gpt-5.5`, `gpt-5.2` | `low`, `medium`, `high`, `xhigh` |
| Persistent-chat model selection only | `deepseek/deepseek-v4.1-flash` | `low`, `high`, `max` |

The persistent-chat list is advertised by the current host in `send_message_to_thread`; `create_thread` accepts model/effort overrides but does not itself enumerate model-specific support. Confirm the target host and chosen tool at dispatch. Generic schema values such as `none` or `minimal` are not evidence that a listed model supports them. Availability does not authorize creating a separate chat.

### Custom DeepSeek Flash routing

Checked against the local Codex dispatch schemas on **2026-10-29**: the persistent-chat host model list in `send_message_to_thread` advertises `deepseek/deepseek-v4.1-flash` with `low`, `high`, and `max` effort. It does not advertise `medium` for this model. Native `spawn_agent` does not currently advertise DeepSeek. Recheck the chosen tool at dispatch; availability can change.

The user may select DeepSeek Flash for suitable bounded development work. Keep the default Builder and Reviewer on Sol unless the user selects otherwise. Use DeepSeek only through a tool that advertises its exact ID. Do not create an extra persistent task merely to bypass native unavailability: separate-task authorization still applies. Do not infer subscription quota or cost savings from a custom model label. Give it the same isolation, tests, evidence and independent acceptance requirements as other workers.

### Cost-conscious work

For explicit “cheap” or “save quota” requests, prefer `gpt-6-luna` for precise edits, focused coding, extraction and bounded checks with clear acceptance criteria. Use `gpt-6.1-sol` when implementation, investigation or independent review needs broader judgment. Keep effort proportional to the task, share only necessary context and avoid workers whose overhead exceeds their useful contribution. Keep Astra as the preferred Mastermind. Model and effort choices alone do not prove subscription quota or cost savings.

### Availability and effort

Before dispatch, inspect the tool's current supported models, reasoning efforts and target host. Use exact advertised IDs; do not probe unlisted model names based on historical launch acceptance. If a preferred model is unavailable, use an already authorized alternative or ask for the missing choice. An ambiguous launch must be inspected before retrying.

The tool/client is authoritative for available effort values. Use `low`, `medium` or `high` as above; raise to `xhigh` only when task difficulty warrants it and the tool supports it. Do not enable Max/Ultra or extra workers by default. API reasoning options and desktop options can differ.

Distinguish **model requested**, **launch accepted**, **result returned**, and **execution model verified**. Agent self-identification is not verification. Report execution model as unverified when authoritative runtime metadata is absent. Do not silently inherit the parent model when a lower-tier worker was requested.

For a bounded native assignment, prefer `fork_turns="none"` with a self-contained brief and relevant file paths, especially when selecting a different model. The current tool supports only `"none"` and `"all"`, not a numeric turn count. Use `"all"` when the full conversation is needed and the tool permits the selected model/context combination.

For future refreshes, inspect live dispatch schemas and host model lists first. Consult official model guidance if capability or pricing claims require verification; public API model names and efforts need not match desktop aliases. Do not infer the next model ID from version naming.

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

For cost-conscious work: “Use $team-orchestration to save quota.” Prefer GPT-6 Luna for focused tasks and GPT-6.1 Sol where broader judgment is needed, with Astra remaining the preferred Mastermind.

For the alternative: “Use $team-orchestration with separate persistent Codex tasks.”
