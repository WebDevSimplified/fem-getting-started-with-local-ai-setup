---
title: "Basic Install"
description: "Install LM Studio and run a small local model so you have a working setup before we explore the details."
---

Before we dive into hardware, model formats, and all the choices involved in local AI, I want you to see a model running on your own computer. This gives us a simple starting point that we can refer back to.

We will be using LM Studio since it makes downloading and running a model straightforward. We are also using a very small version of Qwen 2.5 Coder for this demonstration. It is not the model I would use for pretty much any task in the real world, but it is small enough to run on nearly any modern machine (even quite low end devices).

## Install LM Studio

Go to the [LM Studio download page](https://lmstudio.ai/download) and download the version for your operating system. Once the download finishes, run the installer and follow the prompts. The default options are fine, but be sure to enable the option to view developer settings since we will use those settings to create our local AI setup.

When the installation is complete, open LM Studio. You do not need to create an account or change any settings before continuing.

## Download A Model

LM Studio can download models directly from Hugging Face. Open the following link:

[Download Qwen 2.5 Coder 0.5B Q4_K_M](lmstudio://open_from_hf?model=unsloth/Qwen2.5-Coder-0.5B-Instruct-GGUF&file=Qwen2.5-Coder-0.5B-Instruct-Q4_K_M.gguf)

Your browser may ask permission to open LM Studio. Allow it to open the application. LM Studio will show you the exact model file we need. Click the download button and wait for it to finish.

The file name includes two details that will make more sense later:

- `0.5B` means the model has about 500 million parameters.
- `Q4_K_M` is the model's quantization level. It makes the model smaller without sacrificing too much quality.

This model is intentionally tiny, so the download should only be a few hundred megabytes. That is why it is a good first model, even if your computer does not have a powerful GPU.

## Load The Model

Open the chat screen in LM Studio. At the top of the screen, choose the Qwen model you just downloaded from the model picker and click **Load Model**. Its name should be something like `Qwen2.5-Coder 0.5B Instruct`.

LM Studio will load the model into memory. Once it is ready, type a message and send it. Since this is a coding model, try asking it something simple like this:

```text
Write a JavaScript function that returns the largest number in an array.
```

That's all it takes to get setup with your very first local AI model, but there is obviously much more to learn about optimizing performance, choosing the right models, and configuring your local AI environment for agentic coding.
