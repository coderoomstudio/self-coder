# Models And Backends

Selfcoder connects VS Code to local models served by LM Studio or Ollama. The extension does not require one specific model. You choose the backend and model that fit your machine, task, and preferred workflow.

## Supported Backends

| Backend | Default endpoint | Best for |
| --- | --- | --- |
| [LM Studio](https://lmstudio.ai/download) | `http://localhost:1234` | Visual model management, local server controls, model metadata, OpenAI-compatible APIs. |
| [Ollama](https://ollama.com/download) | `http://localhost:11434` | CLI-driven model management, simple local runtime, reproducible model pulls. |

Change the active backend with `Selfcoder.backend`.

Change the backend address with `Selfcoder.backendURL` if your server is not using the default endpoint.

## Choosing A Model

For coding work, start with a model that is tuned for code and has enough context for your project.

Look for:

- strong coding performance
- context length of 16K or higher for normal tasks
- context length of 32K or higher for larger files and multi-file work
- tool-use support if you want the model in Agent workflows
- vision support if you want to attach screenshots or images
- reasoning support if you want explicit thinking output for complex tasks

Smaller models are often faster and good for focused edits. Larger models are usually better for architecture questions, broad refactors, and harder debugging.

## LM Studio Notes

LM Studio usually works best when:

- the local server is running
- a chat model is loaded
- the endpoint is reachable at `http://localhost:1234`
- the model appears in LM Studio's local server model list

Selfcoder can use LM Studio's OpenAI-compatible chat endpoint and native metadata when available.

LM Studio model metadata may allow Selfcoder to display:

- context length
- parameter size
- vision support
- reasoning support
- tool-use support

## Ollama Notes

Ollama usually works best when:

- the Ollama service is running
- the model has been pulled locally
- the endpoint is reachable at `http://localhost:11434`
- `ollama list` shows the model

Example model pull:

```powershell
ollama pull qwen2.5-coder:7b
```

Selfcoder can use Ollama's native chat API and OpenAI-compatible endpoints where appropriate.

## Model Capabilities

Selfcoder filters and displays models based on backend metadata.

Common capability labels:

| Capability | Meaning |
| --- | --- |
| Context | How much input the model can consider at once. |
| Vision | The model can understand image attachments. |
| Tools | The model may support tool-calling workflows. |
| Reasoning | The model can produce separate thinking output when enabled. |

Embedding-only models are not useful for chat and are filtered out of chat pickers.

## Reasoning Models

Some models can stream a separate thinking or reasoning section before the final answer.

Control this with `Selfcoder.reasoning`:

- `disabled`
- `low`
- `medium`
- `high`

The exact behavior depends on what the selected backend and model support. If a model does not support reasoning, Selfcoder falls back to normal chat behavior.

## Tool-Capable Models

Tool support matters most for VS Code native model picker and Agent workflows.

If a model appears in the Selfcoder sidepanel but not in VS Code's native model picker, it may not report tool support. Use another model or check the backend metadata.

## Practical Model Tips

- For quick explanations, use a smaller coding model.
- For larger refactors, use a larger model with more context.
- For UI screenshots, choose a vision-capable model.
- For Agent mode, choose a tool-capable model.
- For long conversations, watch the token indicator and start a new chat when the topic shifts.
