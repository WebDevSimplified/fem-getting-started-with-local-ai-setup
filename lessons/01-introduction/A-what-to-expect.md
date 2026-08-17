---
title: "What To Expect"
description: "Learn what this workshop covers and how it will help you build a local AI workflow that fits your own hardware and use cases."
---

Setting up local AI can look deceptively simple if all I do is show you how to setup a model on my hardware. All you do is download a model, install an app, and start chatting. The problem is that this type of walkthrough only works when you have the same hardware, use the same tools, and want the same result as the me.

That is not how most of us actually use local AI. You may have a gaming PC, a MacBook, an older laptop, or a machine with no dedicated GPU at all. You may want a private chat assistant, a coding agent, or image generation. Each of those choices changes what setup makes sense.

This is why the main goal of this workshop is not to give you one exact setup to copy. I want to teach you how local AI works so you can make the right choices for your own hardware, tools, and use cases.

## What You Will Learn

Before we start installing anything, we need to understand the pieces involved. A local AI workflow has more moving parts than just a model, and knowing what each part does makes the setup process much less confusing.

In this workshop, you will learn:

- What models are, how they work, and what their names and sizes actually tell you
- How your CPU, GPU, memory, and storage affect which models you can run
- How quantization changes a model's size, speed, and quality
- How to choose a model based on the task you want it to perform
- How local runtimes and model formats fit together
- How to choose and configure an agent harness for coding and other workflows
- How to evaluate and improve a local AI setup when it is too slow or does not give you the results you want

By the end of this workshop, you will have a local AI setup running on your machine. More importantly, you will understand why you chose that setup and how to adjust it when your needs change.

## My Setup

During this workshop I will be using 2 different computers:

- **This Laptop:** Not at all optimized for local AI and has extremely limited GPU capabilities.
- **Remote Desktop Machine:** My main development machine at my house with a Nvidia 5070 Ti GPU. This machine is much more capable for running local AI and is what I will demo all larger models on.

My main machine is not optimized for local AI since I use this machine mostly for video recording/editing which is why I have the GPU I do. You can get away with a much cheaper GPU (that may even be better for larger AI models) if your primary use case is running local AI so don't be discouraged by the high price tag of the GPU I am using.

## Sneak Peek

Now I want to give you a quick sneak peek at what you will be able to accomplish by the end of this workshop. A 100% private, local AI workflow running on your own hardware that you can access remotely from any device no matter where you are.

I will prompt my remote machine from this laptop and everything will work just like if you were running a cloud model.

Let's just use this simple prompt for testing.

```
Create an HTML page that says "Welcome to my AI workshop"
```
