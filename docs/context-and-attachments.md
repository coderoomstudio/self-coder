# Context And Attachments

Selfcoder is built around local-model-friendly context. Instead of sending everything in your workspace, it builds a request-specific context package based on the active model, current editor state, conversation history, and your prompt.

## What Selfcoder Can Use As Context

Depending on the request and available context window, Selfcoder can include:

- pinned files
- selected text from the active editor
- the whole active file, when it fits
- diagnostics from the active file
- a recently focused file
- git diff summaries or focused hunks
- repository search snippets
- workspace instruction files
- manually attached text files
- manually attached images for vision-capable models
- previous conversation turns

Automatic context is selected at send time. This keeps requests focused and avoids wasting limited local model context.

## Context Chips

The sidepanel shows context chips above the input.

These chips help you understand what Selfcoder is likely to use, such as:

- active file
- active selection
- diagnostics
- pinned files
- pending attachments

Some context sources, such as repository search and git diff packing, are finalized only after you send the prompt because they depend on the actual question and remaining token budget.

## Pinned Files

Pinned files are explicit context. They are useful when you know a file matters for the next few turns.

To pin a file:

1. Open the file in VS Code.
2. Use the editor title context menu.
3. Choose **Pin to Selfcoder Context**.

Pinned files are included before automatic context sources. Current behavior allows up to 3 pinned files.

Use pinned files for:

- implementation files related to a bug
- a test file and the source file it covers
- configuration files that affect the answer
- API contracts or schemas the model should respect

## Manual Text Attachments

The sidepanel can attach text files to a message.

Use attachments when:

- the file is not currently open
- you want to include a specific document or log
- the task depends on content outside the active editor

Current limits:

- up to 5 pending attachments
- text files up to 200 KB each
- unknown files are checked before being treated as text

## Image Attachments

Selfcoder supports image attachments when image support is enabled and the selected model supports vision.

Use images for:

- screenshots of UI bugs
- mockups
- error dialogs
- diagrams
- visual references

Current limits:

- images up to 2 MB each
- pasted clipboard images are supported
- images require `Selfcoder.enableVision` to be enabled
- images require a vision-capable model

If image upload is blocked, check the selected model and the vision setting.

## Workspace Instructions

Selfcoder can include workspace-specific instructions automatically.

It looks for the first matching instruction file in this priority order:

1. `local-instruction.md` (or `local-instructions.md`)
2. `copilot-instructions.md`
3. `CLAUDE.MD`

Use workspace instructions for stable project rules, such as:

- coding style
- test commands
- architecture constraints
- preferred libraries
- security rules
- "do not modify" areas

Instruction changes apply on the next request.

## Token Budgeting

Local models vary a lot in context length. Selfcoder uses model metadata when available to estimate how much context can safely fit.

When the conversation gets large, Selfcoder may omit older turns from the next request payload while keeping the visible history intact. The goal is to keep the model responsive without silently deleting your conversation.

The token indicator helps you see when a conversation is getting close to the model's context limit.

## Tips For Better Context

- Select the exact code before asking about a small section.
- Pin important files before asking a cross-file question.
- Attach the exact log or error text.
- Use larger-context models for repository-wide questions.
- Start a new chat when the topic changes.
- Ask for one task at a time.

Good prompt:

```text
Use the pinned test file and active implementation file. Find why this edge case fails and suggest the smallest fix.
```

Less effective prompt:

```text
Fix everything.
```
