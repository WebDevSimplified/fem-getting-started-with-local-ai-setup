---
title: "Connecting OpenCode"
description: "Configure OpenCode to use a local LM Studio model and verify it with a low-risk coding task."
---

TODO: Probably remove, but maybe add in if I need to fill more time. https://opencode.ai/docs/providers/#lm-studio

If you want a bit of a mix between VSCode and Pi, OpenCode is a good option. It has a simple terminal interface like Pi, but still provides many features and tools out of the box like VSCode.

## Add The Provider

Create or update `opencode.json` in your project directory.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "lmstudio": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "LM Studio (local)",
      "options": {
        "baseURL": "http://127.0.0.1:1234/v1"
      },
      "models": {
        "your-loaded-model-id": {
          "name": "Local Coding Model",
          "limit": {
            "context": 32768,
            "output": 8192
          }
        }
      }
    }
  }
}
```

Replace `your-loaded-model-id` with the ID returned by LM Studio. The `context` and `output` limits are not guesses. They tell OpenCode how much of the model's available token budget it can use, so set them to limits you have actually loaded and tested.

## Configure Authentication When Needed

When LM Studio does not require authentication, OpenCode can use the local endpoint without a real secret. When you turn on LM Studio API tokens, store the token through OpenCode's connection flow or configure it through the provider's `apiKey` option.

```json
{
  "provider": {
    "lmstudio": {
      "options": {
        "baseURL": "http://127.0.0.1:1234/v1",
        "apiKey": "{env:LM_STUDIO_API_KEY}"
      }
    }
  }
}
```

Keep the actual value in your environment instead of committing it to `opencode.json`.

## Select And Evaluate The Model

Open OpenCode and use its model picker.

```text
/models
```

Choose `LM Studio (local)` and your configured model. Then begin with a task that gives you a clear success condition and low risk.

```text
Inspect the project structure and tell me which command runs the production build. Do not edit files.
```

OpenCode's agent workflow depends heavily on tool calling. A model can be good at code completion and still be unreliable at choosing tools or formatting tool arguments. If it repeatedly fails this small task, test a coding model that explicitly supports tool use instead of assuming the provider configuration is wrong.

## Checkpoint

Your OpenCode setup is complete when the model appears in `/models`, can inspect the project, and follows a read-only instruction. From there, enable write and command permissions gradually for real work.
