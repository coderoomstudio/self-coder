# Getting Started

This guide walks through installing Selfcoder, connecting a local or self-hosted model backend, and sending your first message from VS Code.

## Requirements

You need:

- VS Code `1.100.0` or newer.
- Selfcoder installed from the latest release package.
- One supported model backend:
  - [LM Studio](https://lmstudio.ai/download), or
  - [Ollama](https://ollama.com/download), or
  - an OpenAI Chat Completions-compatible server such as vLLM or llama.cpp
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
7. Keep `Selfcoder.backendAddress` as `http://localhost:1234`, unless your LM Studio server uses a custom address.

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
7. Keep `Selfcoder.backendAddress` as `http://localhost:11434`, unless your Ollama server uses a custom address.

## Option C: Use vLLM, llama.cpp, Or Another Compatible Server

Selfcoder can connect directly to a server that implements OpenAI-style model discovery and streaming Chat Completions.

1. Start the server with a chat model. Common local roots are:

```text
vLLM:      http://localhost:8000
llama.cpp: http://localhost:8080
```

2. Verify that the server exposes both `GET /v1/models` and streaming `POST /v1/chat/completions`.
3. In VS Code, open **Settings** and search for `Selfcoder`.
4. Set `Selfcoder.backend` to `OpenAICompatible`.
5. Set `Selfcoder.backendAddress` to the server root or its `/v1` base URL. Selfcoder accepts both `http://localhost:8000` and `http://localhost:8000/v1` and appends the route itself.
6. If the server requires bearer authentication, enter its token in `Selfcoder.backendAuthorizationToken`. Otherwise, leave the setting empty.
7. Reconnect Selfcoder and select a model from the server.

Do not enter a full route such as `/v1/models`. Plan, Agent, and VS Code native tool flows also require the served model and chat template to support OpenAI-style tool calls.


## Send Your First Message

1. Open a project in VS Code.
2. Open the Selfcoder view from the activity bar.
3. Choose your backend and model from the Selfcoder controls.
4. Open a source file.
5. Ask a focused question, such as:

```text
Explain what this file does and point out any risky areas.
```

Selfcoder streams the answer from your selected model.

When you are ready to explore beyond a normal chat response, use the composer selector:

- **Plan** actively reads and searches the repository while enforcing a no-edit, no-terminal boundary.
- **Agent** can implement and verify changes according to your permission setting.

Plan and Agent require an open workspace and a tool-capable model. On their first use, Selfcoder downloads and verifies its managed OpenCode runtime.

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
- Learn the read-only investigation workflow in [Plan Mode](plan-mode.md).
- Learn how Selfcoder gathers context in [Context and Attachments](context-and-attachments.md).
- Tune models and backend settings in [Models and Backends](models-and-backends.md).
