---
title: "LM Studio API Mode"
description: "Learn how LM Studio turns a loaded local model into an OpenAI-compatible API that developer tools can use."
---

Running a model in LM Studio's chat interface is useful for testing, but that is not how you actually use AI in agentic coding. This is where LM Studio's Developer tab comes in.

## Start The Local Server

Serving your model in LM Studio is as simple as going to the Developer tab and turning on `Start server`. The server will be available at this address:

```text
http://127.0.0.1:1234/v1
```

You can also start the server from the terminal with LM Studio's `lms` CLI.

```bash
lms server start
```

### Loading Models

Loading models in the server is as simple as clicking the Load Model button and configuring your setup options.

**IMPORTANT:** Make sure to toggle the `Remember settings for <model>` option so that your model configuration persists across server restarts.

## Configuring the Local Server

You have a few options for configuring the local server:

- **Server Port:** Change the port if `1234` is already in use or if you want to run on a different port.
- **Require Authentication:** Setup API key access. Only really useful if you plan to expose your server to others or run it on a network where security is a concern.
- **Server on Local Network:** By default, the server binds to `localhost`. You can enable `Serve on Local Network` if you want to access your server remotely. We will cover this in depth in the next module.
- **Allow Per-Request MCPs:** Enabling this option allows your models to access MCP servers not specified in LM Studio. I would recommend leaving this on.
- **Allow Calling Servers from mcp.json:** This option lets models run any MCP server in your LM Studio mcp.json file. I recommend leaving this off as it is best to just provide MCP access explicitly through your dev tools.
- **Enable CORS:** This just allows cross origin requests. I would recommend leaving this off unless you specifically need it for development purposes.
- **Just In Time Model Loading:** Enabling this option allows models to automatically be loaded when they are requested, which means you don't need to preload your models manually. I always leave this on.
- **Auto Unload Unused JIT Loaded Models:** This option will just unload any model that was automatically loaded if it hasn't been used within the idle timeout window. I always leave this on.
- **Only Keep Last JIT Model:** This option will ensure only one model can be JIT loaded at a time so it will unload any previously JIT loaded model. I recommend leaving this on since it will conserve your memory if you switch models often.

## Test Your Server

Testing our server is as simple as calling out to the API when it is running.

```bash
curl http://127.0.0.1:1234/v1/models
```

This will list all the models we have loaded. If you have JIT model loading enabled it will show all your available models instead. You can also see the output in the Developer Logs inside LM Studio.

## Different APIs Explained

You may notice that there are multiple API types listed:

- LM Studio API
- OpenAI-compatible
- Anthropic-compatible

Each API type has its own set of endpoints and expected request/response formats. In nearly all cases, though, you will be using the OpenAI-compatible API since that is what most providers support.

The OpenAI-compatible API also has multiple endpoints.

- **/v1/models:** Lists all available models.
- **/v1/responses:** A newer endpoint for handling interactions that manage some of the state on the server side, reducing the need to pass the entire conversation history each time.
- **/v1/chat/completions:** The standard chat style interaction endpoint, used for generating conversational responses.
- **/v1/completions:** Predict the next token given a prompt. This is considered deprecated.
- **/v1/embeddings:** Used specifically for creating embeddings for RAG (Retrieval-Augmented Generation) workflows.

In 99% of cases, you will be interacting with the OpenAI-compatible API using the `/v1/chat/completions` endpoint or the `/v1/responses` endpoint. Nearly all providers support `/v1/chat/completions`, but some may support both `/v1/chat/completions` and `/v1/responses`.
