# Project context

Read [docs/project-brief.md](docs/project-brief.md) before planning or implementation. It is the source of truth for requirements, recommendations, milestones, open questions, and research links. Update it when decisions change; avoid duplicating it here.

Read [docs/implementation-handover.md](docs/implementation-handover.md) for the original execution order and acceptance checks. The user intends GPT-6-astra with high reasoning for planning/review and GPT-6-luna with medium reasoning for implementation/bug fixes in a later task. This records the user's workflow; it does not change the active model.

- This is a developer-portfolio proof of concept demonstrating WebMCP through a single-thread chat whose own interface can be changed conversationally.
- Current stage: milestone 1 typed-chat MVP is implemented and deployed. See [docs/implementation-status.md](docs/implementation-status.md) for verified results and pending checks.
- Keep scope small and documentation concise. Distinguish user requirements from proposed defaults.
- Standing user instruction (2026-10-03): at the end of each turn that changes project files, make one commit containing the changes from that turn and push it to the configured remote. Do this after the relevant checks, before the final response; no additional confirmation is needed. Do not create empty commits, include unrelated user changes, or force-push. If commit or push fails, report it explicitly.
- Scope clarification approved 2026-10-11: the automatic push rule above applies to ordinary authorized Talker work. Foundation setup, repository topology changes, Vanilla releases, and cross-repository adoption/promotion require explicit push authorization. The initial foundation setup is local only: commit the reviewed changes, but do not push. Vanilla work is committed locally; a future backup remote and any push require authorization.
- Keep API credentials server-side. Share validated UI actions between manual controls, chatbot tool calls, and WebMCP. Never execute arbitrary model-generated JavaScript or arbitrary HTML/CSS. Exception: user-authorized, reviewed Vitest test code may be executed with its named test scripts. Live Antigravity tests must be explicitly opt-in, target a locally running backend, and enforce a maximum of 7 model requests per rolling 60-second window. Never expose API keys to frontend code, test output, or logs.
- Standing user approval (2026-09-26): add and run Vitest/RTL tests and local test suites; run the opt-in live Antigravity test against the user's locally configured backend, with at most 7 real requests per minute. Never use the production API or expose the API key.
- Recheck evolving browser APIs, model availability, quotas, and hosting limits before implementation. Do not describe ordinary function calling as a verified WebMCP demonstration.

## User-provided environment instruction

You don't have a working Browser Use feature, because it's not available in Europe. When the user asks you to perform in-browser user actions, answer immediately why you can't.

## Talker family: architecture first

Before work involving foundations, shared functionality, repository topology, or cross-repository Git operations, read:

- [docs/talker-architecture.md](docs/talker-architecture.md) for binding design decisions, boundaries, and release policy.
- [docs/sync-workflow.md](docs/sync-workflow.md) for Git operating conventions and the approved local setup.

These documents govern the repository family; the project brief governs application behavior. Repository-specific role notes identify historical deployment information. If family documents are missing, request their paths or content rather than inventing the rules.

## Talker family: binding rules

1. Vanilla Talker is a separate, locally runnable, general-purpose application and a living foundation. It has no separate application deployment at present.
2. Existing Talker remains an independent descendant. Preserve its repository identity, origin, branch tracking, and deployment.
3. Vanilla owns generally useful capabilities; descendants own specialized behavior. Keep specialized code out of Vanilla.
4. Descendants extend rather than alter Vanilla core wherever reasonable. Prefer general core improvements in Vanilla first; document unavoidable descendant core changes and their merge cost.
5. Descendants adopt selected complete annotated Vanilla release tags through reviewed merges, never automatically and not normally through individual cherry-picks.
6. A reusable descendant feature may be promoted selectively into Vanilla after independent integration and testing. Reconcile duplicate logical patches on later adoption.
7. Preserve shared Git ancestry and avoid unnecessary rewrites. Keep Vanilla complete and locally runnable; do not introduce shared packages or a plugin framework prematurely.

## Talker family: execution safeguards

- Inspect status, remotes, tags, branch topology, and existing workflows before structural or synchronization operations.
- Preserve user changes. Do not delete/reset them, force-push, rewrite history, modify an existing remote, move release tags, create repositories, push, or trigger deployments without explicit authorization for the applicable action. Ordinary Talker pushes retain the standing authorization scoped above.
- Propose exact changes, targets, verification, and recovery before major repository setup or synchronization work. Approval of the 2026-10-11 local setup covers its named branches, repository, release tag, new fetch remote, and disposable adoption rehearsal; it does not authorize publishing or deployment.
- Preserve and merge existing agent guidance rather than replacing it.
- Do not copy ignored credentials or local configuration into another repository. Full history can retain committed secrets; inspect it before sharing or publication.
- Run available builds, tests, and local smoke checks when changes are permitted. Never fabricate results or claim mocked checks verify real providers, microphone behavior, or native WebMCP.
- Report discrepancies between the repository and architecture instead of silently changing agreed decisions.
- After successful handoff integration, remind the user to remove the temporary `talker-handoff/` directory. Do not commit or automatically delete it.
