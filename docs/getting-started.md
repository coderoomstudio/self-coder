# Getting Started

This guide walks through installing Selfcoder, connecting a local model backend, and sending your first message from VS Code.

## Requirements

You need:

- VS Code `1.100.0` or newer.
- Selfcoder installed from the latest release package.
- One local model backend:
  - [LM Studio](https://lmstudio.ai/download), or
  - [Ollama](https://ollama.com/download)
- At least one chat-capable model available in the selected backend.

## Install Selfcoder

Selfcoder releases are published on the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=coderoom.Selfcoder).

1. Open VS Code.
2. Open the Extensions view.
3. Search for "Selfcoder" and install the extension published by "Coderoom".
4. Reload VS Code if prompted.

After installation, Selfcoder appears in the VS Code activity bar.

## Option A: Use LM Studio

LM Studio is a friendly way to download, manage, and serve local models.

1. Install [LM Studio](https://lmstudio.ai/download).
2. Download a chat or coding model.
3. Start the local server in LM Studio.
4. Confirm that the server is using the default endpoint:

```text
http://localhost:1234
```

5. In VS Code, open **Settings** and search for `Selfcoder`.
6. Set `Selfcoder.backend` to `LMStudio`.
7. Keep `Selfcoder.backendURL` as `http://localhost:1234`, unless your LM Studio server uses a custom address.

## Option B: Use Ollama

Ollama is a local model runtime with a CLI-focused workflow.

1. Install [Ollama](https://ollama.com/download).
2. Pull a chat or coding model. For example:

```powershell
ollama pull qwen2.5-coder:7b
```

3. Make sure Ollama is running.
4. Confirm that the default endpoint is available:

```text
http://localhost:11434
```

5. In VS Code, open **Settings** and search for `Selfcoder`.
6. Set `Selfcoder.backend` to `Ollama`.
7. Keep `Selfcoder.backendURL` as `http://localhost:11434`, unless your Ollama server uses a custom address.

## Send Your First Message

1. Open a project in VS Code.
2. Open the Selfcoder view from the activity bar.
3. Choose your backend and model from the Selfcoder controls.
4. Open a source file.
5. Ask a focused question, such as:

```text
Explain what this file does and point out any risky areas.
```

Selfcoder streams the answer from your selected local model.

## Good First Prompts

Try prompts that give the model a clear task:

```text
Explain the selected function.
```

```text
Find a simpler way to structure this code.
```

```text
Review the current git diff for possible regressions.
```

```text
Write tests for the behavior in the active file.
```

## Next Steps

- Learn the main product surfaces in [Core Workflows](core-workflows.md).
- Learn how Selfcoder gathers context in [Context and Attachments](context-and-attachments.md).
- Tune models and backend settings in [Models and Backends](models-and-backends.md).
