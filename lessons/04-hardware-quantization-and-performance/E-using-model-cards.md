---
title: "Using Model Cards"
description: "Learn how to read a model card for the prompt template, chat template, and generation settings a local model expects."
---

After downloading a model, it is tempting to just load it and start chatting. This will work sometimes, but models are trained with very specific assumptions about how you will talk to them. A model card is where the publisher documents those assumptions.

The model card can tell you which prompt template to use, whether the model supports tool calls, and which generation settings make sense for the model. This is why I always read the model card before I start changing configuration settings. A great model with the wrong template can give you strange output that makes it look like the model is broken.

## Reading the Model Card

I would recommend reading (or at least skimming) the model card for the intended use, special capabilities, chat template, prompt format, and recommended generation settings. You can even throw another AI model at it to summarize the key points for you since these model cards can get very long.

Make sure to specifically look for which settings to use for your use case. For example, some models may have different generation settings for coding and chat tasks.

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

Those special tokens are part of the format the model was trained on. If you change them, leave them out, or use another model's template, the model may repeat your prompt, continue the user's message, or ignore your instructions.

LM Studio can often read the chat template directly from the model file. When it detects a template, use it. If it cannot find one, look in the model card and copy the documented template into LM Studio's manual template setting.

The only thing you need to be aware of is that a chat template is not the same as a system prompt. Your system prompt is an instruction you give the model. The chat template defines where that instruction belongs in the conversation.

## Use The Recommended Prompt Format

Some model cards document a prompt format for specific tasks. Make sure to follow this format to get the best results for those tasks.

This is not actually something you configure in the model settings. It is more about how you structure your prompts when interacting with the model.

## Choose Generation Settings

The model card may also recommend settings such as `temperature`, `top_p`, `top_k`, and `max_tokens`. These settings control how the model chooses the next token in its response.

Often there will be different settings recommended for different tasks. For example, a model card might suggest one set of generation settings for chat and another for complex coding.

You don't have to use the exact generation settings from the model card, but they are a great starting point that you can fine tune from based on your needs. Generally, I find the recommended settings don't need to be changed.

## Make Note of Output Length

When configuring your model with your agents you may need to specify the maximum output tokens. Many models will give a recommended size for this in the model card and may even suggest multiple values based on the work you are trying to do.

## Demo: Configure A Downloaded Model

Open the model card for one of the models you downloaded. Find its intended use, chat template or prompt format, and recommended generation settings. Configure those values in LM Studio, and then test to ensure it still works.

Once you have a working baseline, you can tweak the generation settings if you notice that the model's responses are not quite what you want, such as being too random, too repetitive, or too short.

After you finish that I will show you how I would configure [Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B).
