---
title: "Connecting Pi"
description: "Configure Pi to use an LM Studio model through a local OpenAI-compatible provider."
---

Pi is a minimal terminal based agent harness. I personally find Pi to be great for local AI since it is the most minimal agent harness and thus has very low overhead.

## Add The Provider

Pi reads custom providers from `~/.pi/agent/models.json`. Create that file if it does not already exist, then add an LM Studio provider like this.

```json
{
  "providers": {
    "lmstudio": {
      // Custom name of the provider
      "baseUrl": "http://127.0.0.1:1234/v1", // Your LM Studio server URL (with /v1) appended
      "api": "openai-completions", // Use either openai-completions or openai-responses
      "apiKey": "key", // Your api key or any non-empty string if auth is disabled
      "models": [
        {
          "id": "your-loaded-model-id", // Model ID (the only required field in the model configuration)
          "name": "Local Coding Model",
          "contextWindow": 32768, // Total context size
          "maxTokens": 8192, // Max output tokens
          "reasoning": true, // Enable reasoning capabilities
          "input": ["text", "image"], // Supported input types
          "thinkingLevelMap": {
            // Map Pi thinking levels to model-specific settings
            "minimal": null, // null means not supported so the thinking level doesn't show up
            "low": "low",
            "medium": null,
            "high": "high"
          }
        }
      ]
    }
  }
}
```

Replace the model ID with your model ID and then adjust the rest of the settings to your liking. The most important settings are `reasoning`, `contextWindow`, and `maxTokens`. You can also set the `thinkingLevelMap` to control which thinking levels are selectable in the UI. Lastly, the `input` can be set to allow vision capabilities.

If you want to use the `responses` API instead of `completions`, change the `api` field to `openai-responses` and everything else can stay the same. It should just work out of the box.

## Try It Yourself

Just as we did with VSCode, I want you to try configuring Pi to use your local LM Studio model by editing the `models.json` file and then selecting the model within Pi. Once selected, you can start interacting with the model directly in the terminal to test its capabilities.

You will probably notice the model is much quicker. This is because Pi's system prompt is very short and its list of tools is incredibly minimal. This is part of the reason I really enjoy working with Pi for local AI.
