# Models And Backends

Selfcoder connects VS Code to models served by LM Studio, Ollama, or an OpenAI Chat Completions-compatible endpoint. The extension does not require one specific model. You choose the backend and model that fit your machine, task, and preferred workflow.

## Supported Backends

| Backend | Default endpoint | Best for |
| --- | --- | --- |
| [LM Studio](https://lmstudio.ai/download) | `http://localhost:1234` | Visual model management, local server controls, model metadata, OpenAI-compatible APIs. |
| [Ollama](https://ollama.com/download) | `http://localhost:11434` | CLI-driven model management, simple local runtime, reproducible model pulls. |
| OpenAI compatible | `http://localhost:8000` | [vLLM](https://vllm.ai/), [llama.cpp](https://llama.app/), and other servers that expose `/v1/models` and streaming `/v1/chat/completions`. |

Change the active backend with `Selfcoder.backend`.

Change the backend address with `Selfcoder.backendAddress` if your server is not using the default endpoint.

If the selected server requires bearer authentication, set `Selfcoder.backendAuthorizationToken`. The token applies to model discovery and chat requests for all three backend choices, including authenticated LM Studio or Ollama proxies.

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

## OpenAI-Compatible Servers

Choose the `OpenAICompatible` backend to connect vLLM, llama.cpp, or another compatible server.

Selfcoder expects:

- `GET <base-url>/models`, returning an OpenAI-style top-level `data` array with non-empty model IDs
- streaming `POST <base-url>/chat/completions`
- OpenAI-style tool calls from the model and chat template when you use Plan, Agent, or VS Code native tool flows

Set `Selfcoder.backendAddress` to either the server root or a base URL ending in `/v1`. Selfcoder normalizes both forms:

| Server | Server root | Equivalent `/v1` value |
| --- | --- | --- |
| vLLM | `http://localhost:8000` | `http://localhost:8000/v1` |
| llama.cpp | `http://localhost:8080` | `http://localhost:8080/v1` |
| Other compatible server | Its configured host and port | The same address ending in `/v1` |

Minimal VS Code `settings.json` example for vLLM:

```json
{
  "Selfcoder.backend": "OpenAICompatible",
  "Selfcoder.backendAddress": "http://localhost:8000"
}
```

For llama.cpp, change the address to the port used by your server, commonly `http://localhost:8080`.

When bearer authentication is required, add the machine-scoped token setting in your user settings:

```json
{
  "Selfcoder.backend": "OpenAICompatible",
  "Selfcoder.backendAddress": "https://models.example.com/v1",
  "Selfcoder.backendAuthorizationToken": "your-token"
}
```

The generic compatible API has no portable way to report whether a model is currently loaded, so Selfcoder does not show loaded-model status, warm-up progress, or pre-warm generic models. It also has no portable tool-capability field. Selfcoder exposes compatible chat models optimistically to tool workflows unless recognized metadata explicitly says otherwise, but the model and server chat template must still produce valid tool calls.


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

Tool support matters most for Plan, Agent, and VS Code native model-picker workflows.

If an LM Studio or Ollama model appears in Chat but not in Plan, Agent, or VS Code's native model picker, it may not report tool support. Use another model or check the backend metadata.

OpenAI-compatible model lists do not define a portable tool-support field, so Selfcoder normally makes those chat models selectable. Selection alone cannot add tool support: if Plan or Agent fails while normal Chat works, use a model and server chat template that support OpenAI-style tool calls.

## Practical Model Tips

- For quick explanations, use a smaller coding model.
- For larger refactors, use a larger model with more context.
- For UI screenshots, choose a vision-capable model.
- For Plan or Agent mode, choose a tool-capable model 
- For long conversations, watch the token indicator and start a new chat when the topic shifts.
