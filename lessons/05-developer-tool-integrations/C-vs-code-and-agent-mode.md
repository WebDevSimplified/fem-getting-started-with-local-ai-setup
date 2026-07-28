---
title: "VS Code And Agent Mode"
description: "Connect VS Code to LM Studio in both Agent mode and regular chat mode."
---

VS Code is one of the easiest IDEs to setup with local models since you can download an extension to do it automatically for you or just manually set it up yourself. Both options are very easy.

## Using an Extension

Finding an extension to add LM Studio to VSCode chat is as simple as searching for `tag:"language-models" lm studio` in the Extensions view. From here you can select any provider you want, but we will use [LM Studio for Copilot Chat](vscode:extension/DanLambiase.lmstudio-copilot-provider) as our example

### Using the Extension

Once you install the extension you may need to restart VSCode, but you should now see a list of all your LM Studio models in the chat provider dropdown. You can configure some settings from the extension in case you are using a different base URL or anything like that, but otherwise it should work out of the box.

## Configure Models Manually

Using an extension to load your models may be the simplest approach, but manually configuring them is not much harder and gives you full control over all the model information. This is my preferred approach.

To manually configure a model all you need to do is:

1. Click the gear icon in the model provider drop down.
2. Click "Add Models" and choose the "Custom Endpoint" option.
3. Enter a custom name for this model group (I use "LM Studio").
4. Enter an API key or leave it blank
5. Choose "Chat Completions" as the type of API.

Once that is done VSCode will open a file that looks something like this.

```json
{
  "name": "LM Studio",
  "vendor": "customendpoint",
  "apiType": "chat-completions",
  "models": [
    {
      "id": "",
      "name": "",
      "url": "",
      "toolCalling": true,
      "vision": true,
      "maxInputTokens": 128000,
      "maxOutputTokens": 16000
    }
  ]
}
```

All you need to do is fill in the appropriate information based on your LM Studio configuration. Here is an example:

```json
{
  "name": "LM Studio",
  "vendor": "customendpoint",
  "apiType": "chat-completions",
  "models": [
    {
      "id": "qwen/qwen3.6-35b-a3b", // Model ID
      "name": "Qwen 3.6-35B", // Human readable name
      "url": "http://127.0.0.1:1234/v1/chat/completions",
      "toolCalling": true,
      "vision": true,
      "thinking": true, // I added `thinking: true` since this is a reasoning model
      "maxInputTokens": 222144, // This should be `totalContext - maxOutputTokens`
      "maxOutputTokens": 40000 // Set this based on recommendations from the model card
    }
  ]
}
```

You can also use the responses API if you want instead. I would experiment with both to see which gives the best speed/quality. To do so you only need to change a few things in your config file.

```json
{
  "name": "LM Studio",
  "vendor": "customendpoint",
  "apiType": "responses", //  Change to responses
  "models": [
    {
      "id": "qwen/qwen3.6-35b-a3b",
      "name": "Qwen 3.6-35B",
      "url": "http://127.0.0.1:1234/v1/responses", // Change to /responses
      "toolCalling": true,
      "vision": true,
      "thinking": true,
      "maxInputTokens": 222144,
      "maxOutputTokens": 40000
    }
  ]
}
```

If you change the `apiType` and the `url` you can now use that model with the responses API instead of chat completions.

**IMPORTANT:** VSCode currently has an issue with how their `read/terminalLastCommand` and `read/terminalSelection` tools are formatted which may break certain models in response mode. If you are getting an error related to tools whenever you try to make a request, it is likely due to this formatting issue. Just disable those tools in your chat window or swap back to chat completions mode and everything will work fine.

## Try It Yourself

If you haven't already try connecting one of your models from LM Studio to VSCode. Try both chat completions and responses API to see which works best for your use case.

You may notice slow initial load times when making your first request. This may be caused by having too many tools enabled (since all tool information is sent with the first request) or because the system prompt from GitHub is quite long which needs to be read in its entirety on the first prompt.
