# Settings And Privacy

Selfcoder is local-first: requests are sent to the backend endpoint you configure, usually LM Studio or Ollama running on your own machine.

This page explains the main settings and how they affect behavior.

## Privacy Model

By default, Selfcoder sends chat requests to your configured backend URL.

For a typical local setup, that means:

- LM Studio at `http://localhost:1234`, or
- Ollama at `http://localhost:11434`

If you configure `Selfcoder.backendURL` to point to a remote server, requests go to that server. Treat the backend URL as the boundary for where prompts, attached files, and selected workspace context are sent.

## Privacy Protection Mode

`Selfcoder.privacyProtection` controls native integration behavior.

| Value | Behavior |
| --- | --- |
| `standard` | Enables native VS Code chat integrations and normal Selfcoder model listings. |
| `strict` | Disables native chat integrations and hides cloud-tagged models from Selfcoder model lists when that metadata is available. |

Use `strict` when you want to keep Selfcoder completely local and avoid any potential data sharing with VS Code's native chat features or cloud-tagged models.

## Main Settings

All settings are under the `Selfcoder` namespace.

| Setting | Default | What it does |
| --- | --- | --- |
| `Selfcoder.backend` | `LMStudio` | Selects the active backend: `LMStudio` or `Ollama`. |
| `Selfcoder.backendURL` | backend default | Sets the backend server URL. |
| `Selfcoder.privacyProtection` | `standard` | Controls native chat integration and cloud-tagged model visibility. |
| `Selfcoder.systemPrompt` | helpful coding assistant prompt | Sets the base instruction sent with requests. |
| `Selfcoder.enableVision` | `enabled` | Enables image attachment support for vision-capable models. |
| `Selfcoder.reasoning` | `medium` | Sets reasoning effort for models that support it. |
| `Selfcoder.historyScope` | `global` | Shows all saved conversations or only conversations for the current repository. |
| `Selfcoder.historyRetention` | `100` | Sets the maximum number of conversations kept in history. |
| `Selfcoder.contextMode` | `enabled` | Enables or disables automatic editor and workspace context. |
| `Selfcoder.agent.command` | empty | Explicit path to an OpenCode executable for Agent mode. Overrides the managed binary and PATH detection. |
| `Selfcoder.agent.autoDownload` | `true` | Automatically download and manage the Agent mode runtime on first use. |

## Backend URL

Use `Selfcoder.backendURL` when your backend is not running on the default address.

Examples:

```text
http://localhost:1234
```

```text
http://localhost:11434
```

```text
http://192.168.1.20:1234
```

Make sure the endpoint matches the selected backend.

## System Prompt

The system prompt is the base instruction Selfcoder sends with each request.

Use it for stable preferences, such as:

- concise answers
- preferred language
- testing expectations
- code style
- security posture
- "ask before making broad changes" rules

Keep the system prompt short enough that it does not waste too much model context.

## Context Mode

`Selfcoder.contextMode` controls automatic context collection.

| Value | Behavior |
| --- | --- |
| `enabled` | Selfcoder may include active editor content, diagnostics, recent files, git diffs, or repository snippets when useful. |
| `disabled` | Selfcoder skips automatic context providers. Explicit context still works. |

Even when automatic context is disabled, Selfcoder can still use pinned files, manual attachments, workspace instructions, system prompt, and chat history.

## History

Selfcoder can save completed sidepanel conversations so you can resume them later.

`Selfcoder.historyScope` controls what appears in history:

- `global`: show conversations across workspaces
- `repo`: show conversations created for the current repository

`Selfcoder.historyRetention` controls how many conversations are kept.

Image binary content is not kept in conversation history, which helps avoid storing large image payloads in VS Code state.

## Workspace Instructions

Workspace instruction files let you define project-specific behavior without repeating it in every prompt.

Selfcoder checks for:

1. `local-instruction.md` (or `local-instructions.md`)
2. `copilot-instructions.md`
3. `CLAUDE.MD`

Use these files for project rules and stable context that should apply to every request.

## Sensible Defaults

For most users:

- use `standard` privacy mode
- keep `contextMode` enabled
- keep `enableVision` enabled
- use `medium` reasoning
- keep history scope as `global` unless you work across many repositories

Switch to stricter settings when you need a narrower, more controlled workflow.
