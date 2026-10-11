# Vanilla Talker releases

## vanilla/v1.0.0 — 2026-10-11

Initial local foundation from Talker application revision `8c36eab99fe407e275ace4f30c3e5a6a0bc62aaa`, retaining full history and the shared permanent documentation commit `5e1e6c3`. The annotated tag identifies the validated Vanilla commit containing these role/status notes, rather than the raw Talker revision. No hosted repository, application deployment, or push is part of this release.

### Included behavior

The inherited complete React/TypeScript/Vite frontend and Python/aiohttp backend retain streamed single-thread chat, authentication, interruption/error history, bounded appearance tools with WebMCP enhancement/fallback, Brian/browser speech output, Dictation, native Dialog, and the retained hidden Live implementation. Application code and deployment configuration are unchanged. These are inherited capabilities; local cloud and audio behavior is not newly verified by mock checks.

### Validation and limitations

All 91 deterministic frontend tests, six mocked backend tests, production build, and actual local mock backend/frontend HTTP smoke checks passed. See [vanilla-status.md](vanilla-status.md) for commands and exact coverage. No real model calls, interactive browser checks, microphone tests, or listening tests were performed. Existing session-renewal and speech-input-fallback limitations remain documented. No new extension-point or API changes were introduced.

### Descendant adoption

Fetch and merge the complete immutable annotated release tag on an integration branch; do not cherry-pick the release's individual commits. This first release shares Talker's application baseline and documentation commit, so its additional tracked changes are repository-role and Vanilla status/release documentation.

A clean merge can still import Vanilla identity text into a descendant. Inspect the role-note changes in `AGENTS.md`, `README.md`, and `docs/project-brief.md`, preserving the descendant's identity and workflow while retaining general architecture guidance. The Vanilla-specific status/release files describe the foundation, not a deployment or verification of the descendant. Rehearse in a disposable clone and verify both the resulting diff and application behavior before requesting actual adoption. Existing Talker's deployment, origin, and main tracking must remain intact.

Future fixes use a new release version. Never move or overwrite this tag.
