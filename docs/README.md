# Selfcoder User Documentation

Welcome to the public documentation for Selfcoder, a VS Code extension for chatting with local AI models using LM Studio or Ollama.

Selfcoder is designed for developers who want practical AI assistance inside VS Code while keeping model choice, backend configuration, and workspace context under their own control.

## Documentation Map

| Guide | What it covers |
| --- | --- |
| [Getting Started](getting-started.md) | Install Selfcoder, connect LM Studio or Ollama, and send your first message. |
| [Core Workflows](core-workflows.md) | Use the sidepanel chat, Agent mode, `@Selfcoder` in native VS Code Chat, and local models in the VS Code model picker. |
| [Slash Commands](slash-commands.md) | Use built-in sidepanel commands and custom project commands. |
| [Context and Attachments](context-and-attachments.md) | Understand pinned files, editor context, diagnostics, attachments, vision models, workspace instructions, and token budgeting. |
| [Models and Backends](models-and-backends.md) | Choose between LM Studio and Ollama, select useful models, and understand model capabilities. |
| [Settings and Privacy](settings-and-privacy.md) | Configure Selfcoder behavior, privacy mode, history, reasoning, vision, and workspace context. |
| [Troubleshooting](troubleshooting.md) | Fix common connection, model, native chat, attachment, and response quality issues. |

## What You Can Do With Selfcoder

- Chat with local models from a dedicated VS Code sidepanel.
- Switch the sidepanel into Agent mode to let a local model read files, make edits, and run commands across your workspace, with change tracking and one-click revert.
- Use local models through LM Studio or Ollama.
- Ask questions about the current file, selected code, diagnostics, recent work, or repository changes.
- Pin files into the conversation context when a task needs specific source files.
- Attach text files and images, when supported by the selected model.
- Run sidepanel slash commands such as `/context`, `/review`, `/models`, `/export`, `/compact`, and `/init`.
- Add custom Agent mode slash commands with Markdown files in each workspace folder's `.opencode/commands/`.
- Use `@Selfcoder` inside VS Code native chat.
- Expose eligible local models to VS Code's model picker for native chat and agent-style workflows.
- Keep conversation history globally or scoped to the current repository.

## Recommended First Setup

1. Install Selfcoder from the [latest release](https://marketplace.visualstudio.com/items?itemName=coderoom.Selfcoder).
2. Install and start either [LM Studio](https://lmstudio.ai/download) or [Ollama](https://ollama.com/download).
3. Load a chat-capable local model.
4. Open the Selfcoder sidepanel in VS Code.
5. Select your model.
6. Ask a small, focused question about the current file.

For the full walkthrough, start with [Getting Started](getting-started.md).
