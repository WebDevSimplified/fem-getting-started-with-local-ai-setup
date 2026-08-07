---
title: "Model Configuration"
description: "Learn how to read a model card for the prompt template, chat template, and generation settings a local model expects."
---

After downloading a model, it is tempting to just load it and start chatting. This will work sometimes, but models are trained with very specific assumptions about how you will talk to them. A model card is where the publisher documents those assumptions.

## Generation Settings

The most common settings to configure are the generation settings recommended by your model. You can scan the model card or as an AI to scan the model card to find these settings for you.

The settings to look for are `temperature`, `top_p`, `top_k`, and `max_tokens`. These settings control how the model chooses the next token in its response.

Often there will be different settings recommended for different tasks. For example, a model card might suggest one set of generation settings for chat and another for complex coding.

You don't have to use the exact generation settings from the model card, but they are a great starting point that you can fine tune from based on your needs. Generally, I find the recommended settings don't need to be changed.

### Demo: Configure A Downloaded Model

I will show you how to find all these settings using [Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B).

Setting these values can be done from the models tab in LM Studio. Doing it there will set them as the default for your model and will be used every time your model is loaded.

## Make Note of Output Length

When configuring your model with your agents you may need to specify the maximum output tokens. Many models will give a recommended size for this in the model card and may even suggest multiple values based on the work you are trying to do.

This is not something you set in LM Studio, but will be something you need when we setup developer tools.

## Configure The Chat Template

By far the most important thing to look for is the **chat template**. This is the exact format used to turn your conversation into the tokens the model sees.

Here is a simplified example of a template for a chat model:

```text
<|system|>
You are a helpful assistant.
<|user|>
Explain quantization in one paragraph.
<|assistant|>
```

This will almost always be in the model files and should be automatically loaded by LM Studio. If for some reason your model is not working properly, check to ensure the chat template is set to the expected value for the model.
