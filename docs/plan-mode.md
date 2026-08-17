# Plan Mode

Plan mode lets Selfcoder investigate a repository and design an implementation without changing the workspace. It is useful when you want the model to understand the problem, trace the relevant code, identify risks, and produce a concrete plan before any implementation begins.

## What Plan Can Do

Plan can:

- read files in the open workspace
- search the repository through structured tools
- use editor context, pinned files, attachments, conversation history, and workspace instructions
- ask clarifying questions
- show reads, searches, fetched pages, reasoning, and structured plan entries in the activity timeline
- request approval for permitted read-only actions when your permission tier requires it

Plan cannot:

- edit, create, rename, or delete files
- run terminal commands, even commands that appear read-only
- use project-defined or forwarded OpenCode slash commands that could select a mutation-capable agent
- switch itself into Agent mode

These restrictions apply in every permission tier, including `autonomous`.

## How It Works

Plan and Agent use Selfcoder's managed OpenCode runtime over the Agent Client Protocol (ACP). Before a Plan request is sent, Selfcoder requires the runtime to advertise and accept its native Plan mode. If Plan is unavailable or the mode switch fails, the request stops instead of falling back to a prompt-only read-only promise.


Your `Selfcoder.permissionMode` still controls permitted reads, external-directory access, web access, and related approvals. It cannot grant file edits or terminal access while Plan is active.

## From Plan To Agent

Plan and Agent share the same OpenCode session while the workspace, backend, credential, model, managed runtime, and permission tier stay the same. This preserves the investigation context when you switch modes.

Switching to Agent does not run the plan automatically. You remain in control: select **Agent**, review or adjust the request, and send the implementation prompt when you are ready. Agent can then edit files and run commands according to the selected permission tier.

Sending a Chat request uses a separate backend conversation path and resets the warm OpenCode session.

## Requirements

Plan requires:

- an open folder or workspace
- a connected backend
- a model and chat template that support OpenAI-style tool calls
- Selfcoder's managed OpenCode runtime


For generic OpenAI-compatible servers, Selfcoder may list a model as tool-capable because `/v1/models` has no portable tool-capability field. Plan still requires the served model and its chat template to produce valid tool calls.

## Typical Workflow

1. Open the repository in VS Code.
2. Select a tool-capable model in the Selfcoder sidepanel.
3. Choose **Plan** in the composer mode selector.
4. Describe the outcome, constraints, and questions you want investigated.
5. Follow the activity timeline and answer any clarifying or read-only permission prompts.
6. Review the proposed implementation plan.
7. Stay in Plan to refine it or switch to Agent and send an implementation request.

Example prompt:

```text
Investigate how authentication state flows through this project. Identify the files that need to change to add session expiry, call out compatibility risks, and propose a testable implementation plan. Do not implement it.
```

## Commands In Plan

Plan supports the read-only Selfcoder command set:

- `/help`
- `/context`
- `/new`
- `/review`
- `/export`
- `/models`

`/compact`, `/summarize`, `/init`, and custom `.opencode/commands/*.md` commands are Agent-only because forwarded or project-defined commands can select a mutation-capable agent.
