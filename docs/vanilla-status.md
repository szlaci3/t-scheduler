# Vanilla Talker: local status

Updated: 2026-10-11. This is the separate living foundation at `C:\Users\szala\Combine\VanillaTalker`. It has independent full-history Git storage, local `main`, no hosted remote, and no application deployment. Talker's origin, tracking, application code, and deployment configuration remain unchanged.

## Baseline and verification

- Application source: Talker `8c36eab99fe407e275ace4f30c3e5a6a0bc62aaa`, preserving its 76 commits and all general-purpose capabilities.
- Shared documentation commit: `5e1e6c3`; the family architecture and synchronization workflow are shared with Talker. Original README content and agent guidance are retained with explicit repository-role notes.
- Fresh frontend dependencies installed with `npm ci --no-audit --no-fund`; all 91 deterministic Vitest/RTL tests passed; `npm run build` passed with the isolated local API URL.
- Fresh Python 3.13 virtual environment installed from pinned `backend/requirements.txt`; all six mocked route tests passed with `python -B -m unittest -v test_speech` before creating `.env`. No dependency stubs or copied environments were needed.
- Actual local backend/frontend startup and HTTP checks passed: mock health; unauthorized API rejection; invalid/valid invitation and session validation; authenticated SSE deltas/completion; stream disconnect and next-request recovery; empty/oversized input rejection; configured-origin CORS preflight; Dialog refusal without local provider confirmation; Vite HTML/transformed module using the isolated API. Both smoke-test processes stopped afterward.
- Zero real model requests. Browser interaction, microphone capture, audible playback, and native WebMCP execution were not performed here. The automated UI suite covers shared appearance controls, reset, cancellation, and audio state behavior using mocks.
- Application, lockfile, and deployment-file contents are inherited unchanged. No framework, package extraction, or new extension mechanism was introduced.

## Run locally

Fresh ignored `backend/.env` contains independent invitation/session values, `CHAT_PROVIDER=mock`, no Google API key, `DIALOG_FREE_TIER_CONFIRMED=false`, `PORT=8081`, and `ALLOWED_ORIGINS=http://127.0.0.1:5174`. Do not copy Talker's `.env` or print credentials. Read the invitation code locally from this ignored file when opening the application.

In one PowerShell window:

```powershell
Set-Location C:/Users/szala/Combine/VanillaTalker/backend
& ./.venv/Scripts/python.exe server.py
```

In another:

```powershell
Set-Location C:/Users/szala/Combine/VanillaTalker/frontend
$env:VITE_API_URL = 'http://127.0.0.1:8081'
npm.cmd run dev -- --host 127.0.0.1 --port 5174 --strictPort
```

Use `npm.cmd` explicitly in Windows PowerShell. In the inspected environment, `npm` selects `npm.ps1` and the Vite flags are rejected by npm instead of forwarded to the dev server.

Open `http://127.0.0.1:5174`. The mock provider labels its replies and does not exercise conversational model tool calls. Appearance controls remain available; actual provider/chat/voice verification requires separately configured local access. Keep billing disabled, confirm the current provider/model availability before live implementation changes, and retain the opt-in local Antigravity test's seven-request rolling-minute limit. Do not infer Vanilla provider access or billing status from inherited Talker reports.

## Known limitations and next work

- Browser Use is unavailable here in Europe. Manual typed-chat, appearance/reset, microphone, audible playback, and native WebMCP checks remain explicit user checks.
- Inherited open issues include the speech-input fallback network problem, prolonged voice-session renewal, and unreported desktop/mobile combinations. Dialog remains visible and the older Live control remains hidden, as in the source application.
- Limits and caches are process-local; this is not durable quota enforcement. No new production readiness or public release claim is made.
- The original README, implementation handover, and implementation status contain historical Talker deployment and milestone statements. This file describes current Vanilla verification.
- Release/adoption operations follow [sync-workflow.md](sync-workflow.md). The initial release tag is created only after these checks and Git/content verification; its exact commit can be read with `git rev-parse 'refs/tags/vanilla/v1.0.0^{}'`.

## Local startup command correction — 2026-10-11

The documented `npm run dev -- ...` invocation failed under Windows PowerShell with npm 12.0.2: npm parsed Vite's host/port/strictPort flags as its own options. Reproduced the wrapper's parsing behavior and verified `npm.cmd run dev -- --host 127.0.0.1 --port 5174 --strictPort` forwards the flags to Vite 6.4.3, starts the actual server, and serves the application with HTTP 200. Stopped only the test-owned server process tree afterward. The local API URL remains `http://127.0.0.1:8081`; no browser interaction or real model requests were performed. Updated this startup example and both shared workflow copies; application code is unchanged.