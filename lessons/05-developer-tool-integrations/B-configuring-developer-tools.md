---
title: "Configuring Developer Tools"
description: "Learn the shared configuration pattern for connecting an editor, CLI, or coding agent to LM Studio."
---

Every developer tool uses a different UI and config-file format, but the connection itself is almost always the same. Once you understand the common pieces, you can configure nearly any developer tool to work with LM Studio.

## The Information You Need

To setup a connection to LM Studio you only need the following information.

1. **The server URL** - This is the address where your LM Studio server is running, typically `http://127.0.0.1:1234`.
2. **The API endpoint** - The specific endpoint you will be interacting with, usually `/v1/chat/completions` or `/v1/responses`.
3. **The API key** - If you set an API key use that, otherwise this can be left blank or filled with any string value if the tool you are configuring requires an API key.
4. **The model ID** - The identifier of the model you have loaded in LM Studio that you want the developer tool to use. This can be copied using the copy button next to the model when it is loaded.
5. **The context window** - The maximum number of tokens the model can handle in a single request. Sometimes this is separated between input and output token limits.
6. **Model capabilities** - Any specific capabilities or features of the model that the developer tool should be aware of, such as support for tool calling, reasoning, or vision.

Once you have this information the actual act of configuring each tool you use is nearly identical.

## General Setup Steps

To setup any tool you need to configure an OpenAI-compatible connection with the above information. Often this will be called `OpenAI`, `OpenAI-compatible`, `Custom OpenAI`, or something similar in your developer tool.

You then need to add the above information into the configuration file for the developer tool you are using. This will almost always be a JSON file that looks something like this:

```json
{
  "name": "LMStudio",
  "apiKey": "key",
  "apiType": "chat-completions",
  "apiUrl": "http://127.0.0.1:1234/v1",
  "models": [
    {
      "id": "qwen/qwen3.6-35b-a3b",
      "name": "Qwen 3.5 MoE",
      "toolCalling": true,
      "vision": true,
      "thinking": true,
      "maxInputTokens": 100000,
      "maxOutputTokens": 40000
    }
  ]
}
```

The first part of the JSON object will define the base information such as the API url, API key, and if you are doing a chat completions or responses API endpoint.

Then there will be an array of models which contain the model ID, a human readable name, and a list of capabilities, context, and any other custom specifications.

The exact property names will vary from tool to tool, but the structure and purpose of the information remain consistent. Usually the documentation for the tool will tell you exactly how to configure the custom models, but if you cannot find good details you can often have AI assist you in this setup.

## Using the Right Model For Agentic Coding

An agent does more than answer a question. It reads files, calls tools, tracks a larger conversation, and needs to follow structured instructions. This means we need specific models that are capable of handling these tasks effectively or they will not work in an agentic workflow.

### Required

These are the capabilities that your model needs to have to work effectively in an agentic coding workflow.

- Tool or function calling support
- Reasoning

Without the ability to call tools your model will not work. Without reasoning your model will struggle to make decisions and solve problems effectively making it essentially useless.

### Recommended

These are capabilities your model doesn't need, but can make your agentic workflow more efficient or higher quality.

- Trained or specialized for coding tasks
- A large context window (100k+ tokens)
- Vision capabilities for understanding images

If you do not have these capabilities your model will still work fine, but it could struggle. For example, if you context is small it may be difficult for the model to fit all the code in memory at once. Without vision capabilities working with your model on UI work will be more cumbersome.

## A Simple Troubleshooting Order

It is very common to mess up configuration since each tool expects your information in a slightly different format. I generally follow these steps when troubleshooting integration issues:

1. Confirm the LM Studio server is running and the model is loaded.
2. Make sure the model ID is the exact same as the model ID displayed by the LM Studio server.
3. Confirm the base URL ends in `/v1` when the tool expects OpenAI compatibility.
4. Ensure that any additional URL path, such as `/chat/completions`, is correctly appended to the base URL if required by the tool.
5. Ensure all model capabilities and context match the configuration in LM Studio.

The developer log is a great way to debug issues with your model not connecting properly since it will show the actual URL being sent to the LM Studio server. Some providers expect you to pass more or less of the full URL path so this is the most common issue you will run into and looking at the actual URL sent to LM Studio when you try to use your coding tool will often reveal the problem.

## Up Next

Next we are going to connect our local models to some of the more common developer tools used for agentic coding.

Notably Claude Code is not included in this list. Claude Code does not officially support local models so any workaround to configure Claude Code with local models is unreliable and prone to breaking with every Claude Code update.
