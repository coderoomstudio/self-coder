# Troubleshooting

This guide covers common Selfcoder setup and usage issues.

## Selfcoder Cannot Connect To The Backend

Check:

1. The selected backend is running.
2. `Selfcoder.backend` matches your backend: `LMStudio` or `Ollama`.
3. `Selfcoder.backendURL` points to the correct endpoint.
4. A local chat model is loaded or available.
5. Your firewall or security software is not blocking local HTTP connections.

Default endpoints:

| Backend | Endpoint |
| --- | --- |
| LM Studio | `http://localhost:1234` |
| Ollama | `http://localhost:11434` |

After fixing the backend, use the Selfcoder reconnect action or reload VS Code.

## No Models Appear In Selfcoder

Possible causes:

- No chat model is installed in LM Studio.
- Ollama has no local models installed.
- The backend URL is wrong.
- The backend is running, but the selected backend setting is wrong.
- The model is an embedding model, not a chat model.
- The model was hidden from Selfcoder pickers. (Agent mode doesn't support models without tool capabilities)

For Ollama, check:

```powershell
ollama list
```

For LM Studio, check that the local server is running and a model is available.

## Model Does Not Appear In The VS Code Model Picker

The Selfcoder sidepanel and VS Code native model picker have different requirements.

A model may be available in the sidepanel but missing from the native picker if:

- it does not report tool-use support
- it is hidden in Selfcoder
- it is an embedding model
- `Selfcoder.privacyProtection` is set to `strict`
- VS Code needs to be reloaded after backend/model changes

Try a tool-capable model and reload VS Code.

## `@Selfcoder` Does Not Work In Native Chat

Check:

- VS Code is `1.100.0` or newer.
- `Selfcoder.privacyProtection` is set to `standard`.
- Selfcoder is installed and enabled.
- Your backend is connected.
- A chat-capable model is available.

If the participant still does not appear, reload VS Code.

## Agent Mode Issues

Agent mode runs an autonomous agent (OpenCode) that Selfcoder downloads and manages automatically on first use.

If Agent mode does not start:

- Open a folder or workspace first. Agent mode needs a workspace to act on and is disabled when no folder is open.
- Select a tool-capable model. Agent mode requires a model that reports tool-use support; if the selected model does not, switch to one that does.
- Make sure your backend is connected and the model is available.

## Image Attachments Are Rejected

Image support requires all of the following:

- `Selfcoder.enableVision` is set to `enabled`
- the selected model supports vision
- the image is within the current size limit
- the backend accepts image input for that model

Current image size limit is 2 MB per image.

## Responses Are Too Short, Confused, Or Missing Context

Try:

- selecting the relevant code before asking
- pinning important files
- attaching the exact log or error text
- using a model with a larger context window
- starting a new chat for a new topic
- asking for one task at a time
- enabling automatic context with `Selfcoder.contextMode`

Better prompt:

```text
Use the selected function and current diagnostics. Explain the error and suggest the smallest safe fix.
```

Less useful prompt:

```text
Fix this project.
```

## Reasoning Is Not Showing

Reasoning output appears only when the selected model and backend support it.

Check:

- the model reports reasoning support
- `Selfcoder.reasoning` is not set to `disabled`
- the backend supports reasoning events for that model

If unsupported, Selfcoder still works as a normal streaming chat.

## Reporting An Issue

Open a GitHub issue from the [Issues page](https://github.com/coderoomstudio/self-coder/issues).


