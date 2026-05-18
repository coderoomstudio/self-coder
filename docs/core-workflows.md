# Core Workflows

Selfcoder gives you several ways to work with local models inside VS Code. The best surface depends on how much control you want and whether you prefer Selfcoder's dedicated UI or VS Code's native chat tools.

## Sidepanel Chat

The Selfcoder sidepanel is the main workspace for local coding conversations.

Use it when you want:

- a dedicated chat panel for one project or task
- model selection inside the extension UI
- streaming markdown responses
- code blocks with copy actions
- context chips showing what Selfcoder may include
- pinned files and manual attachments
- image attachments for vision-capable models
- chat history and conversation resume
- token usage visibility for local model context windows

Typical flow:

1. Open the Selfcoder activity bar view.
2. Select model.
3. Open the file you want to discuss.
4. Select code if the question is about a specific block.
5. Ask your question in the Selfcoder sidepanel.

Good sidepanel prompts:

```text
Explain the selected code and suggest a safer implementation.
```

```text
Use the active file and diagnostics to help me fix this error.
```

```text
Review my current changes and call out likely regressions.
```

## Model Selection

Selfcoder lists chat-capable models reported by the active backend.

Depending on backend metadata, the model list can show details such as:

- context length
- parameter size
- model size
- vision support
- reasoning support
- tool-use support

You can hide models you do not want to see in pickers and set aliases for easier recognition.

## `@Selfcoder` In VS Code Native Chat

Selfcoder also registers a native VS Code chat participant named `@Selfcoder`.

Use this when you want local model answers inside the built-in VS Code Chat panel.

Typical flow:

1. Open VS Code Chat.
2. Type `@Selfcoder` followed by your request.
3. Selfcoder uses the configured backend and the current session default model.
4. The answer streams inside native VS Code Chat.

Example:

```text
@Selfcoder Explain the active file and suggest the next refactor.
```

The native participant uses Selfcoder's backend configuration, system prompt, workspace instructions and request-scoped context pipeline.

## Session Default Model

The native chat participant uses a session default model shown in the VS Code status bar.

When Selfcoder is connected, click the Selfcoder status bar item to choose the default model for native chat. This choice is runtime-only, so it may reset after VS Code reloads.

The sidepanel has its own model selection and can be used independently.

## Local Models In The VS Code Model Picker

Selfcoder can expose eligible local models to VS Code's native model picker.

This is useful for native chat and agent-style workflows where VS Code expects a language model provider. Models usually appear only when they report the capabilities VS Code needs, especially tool support.

Use this workflow when you want:

- local models in VS Code's model dropdown
- VS Code native Ask or Agent mode
- tool-aware workflows with eligible local models
- a more native VS Code experience

If a model does not appear in the native model picker, see [Troubleshooting](troubleshooting.md#model-does-not-appear-in-the-vs-code-model-picker).

## Optional OpenCode Agent Mode

Selfcoder can work with an installed OpenCode CLI for users who want deeper workspace automation.

Use this when you want a more agentic workflow that can inspect files, propose changes, show activity, and work through a larger coding task.

OpenCode is optional. Selfcoder's regular sidepanel and native chat workflows do not require it.

## Choosing The Right Workflow

| Goal | Recommended workflow |
| --- | --- |
| Ask about the current file | Sidepanel chat |
| Use selected text as context | Sidepanel chat |
| Ask from VS Code's built-in chat UI | `@Selfcoder` |
| Use local models in native Agent mode | VS Code model picker |
| Attach files or images manually | Sidepanel chat |
| Resume older conversations | Sidepanel chat history |
| Work through a larger automated coding task | Sidepanel chat with installed OpenCode |
