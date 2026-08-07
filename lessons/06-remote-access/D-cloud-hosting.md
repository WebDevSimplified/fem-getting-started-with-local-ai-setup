---
title: "Running Models In The Cloud"
description: "Rent a more powerful machine to run your own local model server when buying new hardware does not make sense yet."
---

Buying a powerful GPU can be expensive, especially when you are still figuring out if local AI is right for you. You may want to run a larger model, but it is difficult to justify spending thousands of dollars on hardware before you know you will use it.

This is where cloud hosting comes in. You can rent a machine with a powerful GPU, run your model on that machine, and access it from your own computer. You are still self-hosting since you choose the machine, install the runtime, download the model, and control the server. The only difference is that someone else owns the hardware.

## How It Works

You start by choosing a cloud provider that rents GPU machines. Rent a machine with enough VRAM for the model you want to run, install your runtime, and download your model. You can then connect to your machine with SSH or even view a web based UI for managing the server.

Some cloud providers even have runtime configuration baked into the UI for easier setup and management of your model server.

## Why You May Choose This

Cloud hosting is useful when you need more VRAM than your computer has, want to test a larger model for a short project, or need a model server that stays available while your main computer is off. It lets you try powerful hardware without paying for it all at once.

I especially like it as a way to learn what hardware you actually need. After running a few models in the cloud, you will have a much better idea whether buying a GPU is worth it for your workflow and which GPU you should buy.

## The Tradeoffs

By far the biggest benefit is flexibility. You can rent a machine with the exact GPU you need, use it for a few hours, and shut it down when you are done.

The biggest downside is cost. GPU machines charge by the hour, and leaving one running can become more expensive than buying hardware over time. You also need an internet connection, and every prompt you send travels to the rented machine. This is not ideal if you are working with sensitive data, so make sure you understand and accept the provider's security and privacy policies.

You are also responsible for keeping the machine updated, limiting who can access it, and deleting the machine or its data when you are finished. Renting hardware means you do not need to maintain the physical computer, but you still need to maintain the server running on it.

## When To Use It

Cloud hosting is a good middle ground when you need more power now but are not ready to commit to new hardware. I recommend starting small, tracking what each session costs, and shutting down the machine when you are not using it. If you find yourself using it constantly, buying your own hardware may eventually be the cheaper option.
