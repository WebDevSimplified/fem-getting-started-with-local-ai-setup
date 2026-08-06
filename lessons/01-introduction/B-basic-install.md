---
title: "Basic Install"
description: "Install LM Studio and run a small local model so you have a working setup before we explore the details."
---

Before we dive into hardware, model formats, and all the choices involved in local AI, I want you to see a model running on your own computer. This gives us a simple starting point that we can refer back to.

We will be using LM Studio since it makes downloading and running a model straightforward. We are also using a very small version of Qwen 2.5 Coder for this demonstration. It is not the model I would use for pretty much any task in the real world, but it is small enough to run on nearly any modern machine (even quite low end devices).

## Install LM Studio

Go to the [LM Studio download page](https://lmstudio.ai/download) and download the version for your operating system. Once the download finishes, run the installer and follow the prompts. The default options are fine, but be sure to enable the option to view developer settings since we will use those settings to create our local AI setup. If you do not see this option during install, you can enable it in `Settings -> Developer -> Developer Mode`.

When the installation is complete, open LM Studio. You do not need to create an account or change any settings before continuing.

**IMPORTANT:** Do not install Bionic. Make sure to install LM Studio which is the lower level tool for running and hosting local AI models.

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

## Navigating LM Studio

LM Studio is relatively simple to navigate as it only has a few sections.

### Chat Screen

The first option in the sidebar is the chat option. Here you can load and chat with any model you have downloaded and you can even tweak certain parameters such as available tools and model parameters.

### Developer Server

The next option in the sidebar is the developer server. Here is where you load models to be served via an API and consumed in your favorite developer tools. This is the most important tab for agentic coding.

### Your Model Viewer

The third option in the sidebar is a model viewer. Here you can view the models you have downloaded and remove any that you no longer need.

### Model Search

The final main option in the sidebar is the model search. Here you can search for new models to download and add to your local collection. This makes it easy to find the latest models without leaving LM Studio, but is not my preferred way to find models.

### LM Link

Here is where you can setup LM Link for remote access to your local AI models. This is something we will cover at the end of the workshop.

### Options

Finally, the options menu lets you configure various settings for LM Studio, such as appearance, default model parameters, and other preferences.
