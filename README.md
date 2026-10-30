# OpenAI OAuth Proxy CLI

Run a local OpenAI-compatible API proxy using your ChatGPT account. The proxy supports `/v1/responses`, `/v1/chat/completions`, `/v1/images/generations`, `/v1/images/edits`, and `/v1/models`.

## Quickstart

```bash
npx openai-oauth@latest
```

The proxy listens at `http://127.0.0.1:10531/v1`. If you are not signed in with Codex locally, the CLI guides you through sign-in and stores credentials in the Codex auth file. Treat that file like a password.

Press `d` to keep the server running in the background or `q` to quit. Manage it from another terminal:

```bash
npx openai-oauth --detach
npx openai-oauth status
npx openai-oauth logs --follow
npx openai-oauth stop
npx openai-oauth login
```

## Configuration

| Option | Flag | Default |
| --- | --- | --- |
| Host | `--host` | `127.0.0.1` |
| Port | `--port` | `10531` |
| Model allowlist | `--models` | Account-specific models discovered from ChatGPT |
| Auth file | `--oauth-file` | `$CODEX_HOME/auth.json` or `~/.codex/auth.json` |
| Browser login | `--open` / `--no-open` | `--open` |
| Login timeout | `--login-timeout-ms` | `300000` |

Additional advanced options let you override the Codex client version, upstream base URL, OAuth client ID, and token URL.

Binding to a non-loopback host exposes the proxy to your network. Anyone who can reach it may be able to make requests using your ChatGPT account. Keep it bound to `127.0.0.1` unless network exposure is intended and controlled.

## Supported behavior

- Streaming and non-streaming responses
- Chat completions, tool calls, and reasoning traces
- Image generation and editing
- Account-aware model discovery

The `/v1/responses` endpoint is stateless and expects callers to send the full conversation history. Only models supported by Codex are available.

## Development

Requires Bun 1.3.11 and Node.js 20 or later.

Run the proxy from the repository root in PowerShell:

```powershell
bun install
bun run dev
```

The server listens at `http://127.0.0.1:10531/v1`. To build and verify the workspace:

```powershell
bun run build
bun run test
bun run typecheck
```

The proxy CLI lives in `packages/openai-oauth`; its `core`, `local`, and `ai-sdk` workspace packages provide required runtime functionality.

## Legal

OpenAI OAuth is an unofficial, community-maintained project and is not affiliated with, endorsed by, or sponsored by OpenAI. You are responsible for complying with OpenAI's Terms of Use and Usage Policies. Do not share account credentials or bypass restrictions or safeguards. Provided as-is with no warranties.