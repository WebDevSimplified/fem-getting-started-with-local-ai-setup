---
title: "How LLMs Run On Hardware"
description: "Learn how CPUs, GPUs, RAM, VRAM, and unified memory affect whether a local model fits and how quickly it can generate text."
---

In order to properly run models locally we need to first learn how models use memory and compute resources. Knowing this ensures you can choose the optimal model for your exact hardware.

## CPUs

Your CPU is designed to handle many different kinds of work. It has a relatively small number of powerful cores that are great for general-purpose tasks. A model can run on a CPU, but it is going to be incredibly slow for any model of even modest size.

The exact CPU you have doesn't matter much when running models since most models will run on your GPU instead. Having a fast CPU can help with certain models that are too large to fit on your GPU and need to run partially on the CPU.

## GPUs

GPUs take a different approach. They contain a huge number of smaller processing units that can perform many similar calculations at the same time. This is perfect for neural-network inference, which has a lot of this type of work, and is why a compatible GPU can make a local model run much faster.

There are multiple companies that produce GPUs (Nvidia, AMD, Intel, etc.), but Nvidia GPUs are currently the most commonly supported for accelerated model inference due to their mature software ecosystem, specifically their CUDA cores. This means you will have better performance and wider model support on a Nvidia GPU compared to an AMD GPU or Apple Silicon GPU.

## RAM, VRAM, And Unified Memory

To run a model you need to load all the model's weights into memory while it runs. This is done in a few different ways depending on your hardware.

### VRAM

If you have a GPU with dedicated memory (VRAM), the model's weights and intermediate computations can be stored there, which usually results in the fastest instance possible since this RAM is specifically designed to integrate directly with the GPU with the lowest latency.

### RAM

If your system does not have a dedicated GPU or if the model is too large to fit entirely in VRAM, the model's weights and computations can be stored in the main system memory (RAM). This is much slower than using VRAM because the CPU has to handle more of the work and the memory access latency is higher.

### Unified Memory

Some machines, specifically M series Apple Silicon, utilize unified memory. This means that you don't have separate dedicated memory for your GPU and CPU and instead your CPU and GPU share the same memory pool.

This memory is not as fast as dedicated VRAM memory, but it is much faster than loading a model into RAM.

It is also much easier to buy hardware with large amounts of unified memory, while getting large amounts of dedicated VRAM is much more expensive and limited to high-end GPUs.

## Memory Considerations

When running a model, you need to consider not just the size of the model itself, but also the memory required for the context, the KV cache, and other system processes on your machine.

Models with a larger context window will take up much more memory compared to a model with a smaller context window and that all must be reserved and loaded up front. Also, if you have multiple async sessions with a single model that will increase the memory footprint as it needs to maintain separate caches for each session.
