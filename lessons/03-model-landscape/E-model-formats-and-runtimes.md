---
title: "Model Formats And Runtimes"
description: "Learn why model files need a compatible runtime and how formats such as GGUF and MLX affect a local setup."
---

A model's weights are not useful by themselves. You need a runtime that understands the model file, loads its weights into memory, and performs the calculations needed for inference. LM Studio is the application we will use in this workshop, and it includes the runtime needed to run compatible local models.

## Formats And Runtimes Work Together

A **model format** is the way a model's weights and related data are stored in files. A **runtime** is the software that knows how to load those files and execute the model.

You cannot load every model file in every runtime. This is why the format listed on a download page matters just as much as the model family and parameter count.

## GGUF

`GGUF` is a format designed for efficient local inference. It is especially common for models that run through `llama.cpp`-based runtimes, including the workflow we will use with LM Studio.

`GGUF` is also a relatively universal format that works in many different runtimes.

## Apple Silicon And MLX

`MLX` is Apple's machine learning framework for Apple Silicon Macs. It is designed to take advantage of the unified memory shared by the CPU and GPU on M-series Macs.

`MLX` models are designed specifically for Mac computers with Apple Silicon chips and will often run much faster than their `GGUF` counterparts on the same hardware. If you have an Apple Silicon Mac, look for an `MLX` equivalent version of the model to gain some speed advantage.

LM Studio is compatible with `MLX` models.

## Other Formats

You may also see other formats such as `EXL2`, `AWQ`, `NVFP4`, and `TensorRT`. These formats are often optimized for specific hardware or runtime environments and may not be universally compatible.

## Choosing the Right Runtime

There are many different runtimes for loading your models. Some are optimized for specific hardware, while others are more general-purpose. Choosing the right runtime first will help you determine which model format you need.

### LM Studio

LM Studio is a great starting point for a runtime since it is easy to use, relatively customizable, and has a UI that makes configuring the model straightforward.

We will be using LM Studio throughout this workshop since I find it is the easiest to get started with for most users.

### vLLM

vLLM is a high-performance runtime for large language models, optimized for both single-GPU and multi-GPU setups. It is designed to maximize throughput and minimize latency, making it suitable for serving large models.

This is the runtime you would likely use if setting up a complex multi-GPU deployment for serving large models across an entire company since it is highly configurable and fast.

### Ollama

Ollama is another beginner friendly runtime. It is relatively easy to get setup and runs entirely in the terminal since it focuses more on exposing your models through an API to be consumed in other apps.

The main downside to Ollama is it is harder to customize since there is no UI and tweaking settings to fine tune your model is more challenging compared to LM Studio.

### `llama.cpp`

`llama.cpp` is a lightweight and highly portable runtime that powers many other runtimes. For example, LM Studio and Ollama both use `llama.cpp` under the hood for local model execution.

`llama.cpp` is harder to get setup since you need to manage all the configuration yourself, but it offers even greater configuration since you have full control over all aspects of the runtime.
