# Selfcoder

**A VS Code extension for agent workflow with local AI models using LM Studio or Ollama.**

Selfcoder brings a local-first AI coding assistant into Visual Studio Code. It connects to your own LM Studio or Ollama backend, lets you choose the model that fits your machine, and keeps coding conversations close to your workspace.

This repository is the public home for Selfcoder documentation, Marketplace installation details, and issue tracking.

<p align="center">
  <a href="https://marketplace.visualstudio.com/items?itemName=coderoom.Selfcoder">
    <img alt="VS Code Marketplace" src="https://img.shields.io/badge/marketplace-Selfcoder-007ACC">
  </a>
  <a href="https://selfcoder.dev">
    <img alt="Selfcoder Website" src="https://img.shields.io/badge/website-selfcoder.dev-2f6f9f">
  </a>
  <a href="https://github.com/coderoomstudio/self-coder/issues"><img alt="GitHub Issues" src="https://img.shields.io/github/issues/coderoomstudio/self-coder"></a>
  <a href="#supported-backends"><img alt="Runtime: LM Studio or Ollama" src="https://img.shields.io/badge/runtime-LM%20Studio%20%7C%20Ollama-2f6f9f"></a>
</p>

## What Selfcoder Does

- Adds a dedicated chat panel for local AI coding sessions.
- Connects to local models served by LM Studio or Ollama.
- Supports model-aware workspace context, pinned files, attachments, and chat history.
- Includes sidepanel slash commands for help, context preview, review, model listing, export, compaction, and project initialization.
- Integrates with VS Code native chat through the `@Selfcoder` participant.
- Exposes supported local models to the VS Code model picker.
- Supports image attachments for vision-capable models.
- Includes managed OpenCode Agent mode for deeper workspace automation.

<p align="center">
  <img alt="Selfcoder sidepanel demo" src="https://raw.githubusercontent.com/coderoomstudio/self-coder/main/resources/img/general.gif">
</p>

## Installation

Install Selfcoder from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=coderoom.Selfcoder).

To install it from VS Code:

1. Open VS Code.
2. Go to **Extensions**.
3. Search for "Selfcoder".
4. Install the extension published by "Coderoom".
5. Reload VS Code if prompted.

After installing, start LM Studio or Ollama, pick a local chat model, and open Selfcoder from the VS Code activity bar.

## Supported Backends

| Backend | Default endpoint | Use case |
| --- | --- | --- |
| [LM Studio](https://lmstudio.ai/download) | `http://localhost:1234` | Easy setup, local model management, GUI friendly |
| [Ollama](https://ollama.com/download) | `http://localhost:11434` | CLI-driven model management, simple local runtime |

## Documentation

Project documentation is available in the [`docs`](docs/) directory.

Useful starting points:

- [Getting Started](docs/getting-started.md)
- [Core Workflows](docs/core-workflows.md)
- [Slash Commands](docs/slash-commands.md)
- [Context and Attachments](docs/context-and-attachments.md)
- [Models and Backends](docs/models-and-backends.md)
- [Settings and Privacy](docs/settings-and-privacy.md)
- [Troubleshooting](docs/troubleshooting.md)

## Reporting Issues

Use [GitHub Issues](https://github.com/coderoomstudio/self-coder/issues) to report bugs, request improvements, or share compatibility notes for specific models and backends.

## Marketplace

Use the [Visual Studio Marketplace page](https://marketplace.visualstudio.com/items?itemName=coderoom.Selfcoder) for the current version, installation, and changelog details.

## Website

Visit the [Selfcoder website](https://selfcoder.dev) for the product overview, installation links, and updates.
