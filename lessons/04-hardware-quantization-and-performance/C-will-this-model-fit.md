---
title: "Will This Model Fit?"
description: "Estimate a model's memory needs before downloading it, then verify the estimate with a controlled load test."
---

Unfortunately, the size of a model is only one part of the memory equation. You also need to account for the operating system, runtime overhead, and the KV cache for your context and active chats.

## Determine Baseline Memory Usage

The first thing you should do is determine your baseline memory usage with your editor, browser, etc. running. This is extra important on unified memory systems since your entire computer shares the same memory pool.

Make a note of the amount of available RAM and VRAM after accounting for all running applications and the operating system.

## Calculate Actual Model Memory Usage

A model consumes memory in several ways:

- Model weights (the quantized model file)
- Runtime overhead (the memory needed by the framework to manage the model)
- KV cache (for your context and active chats)

Of those 3 by far the biggest 2 are the weights and KV cache.

Your KV cache grows with the context length and the number of active chats. Large context sizes (100K+ tokens) can easily consume as much memory as the full quantized weights themselves.

### Demo: View Memory Usage as Context Size Changes

Let's practice loading a model and observing how the memory usage changes as we adjust the context size. If you are able to load a model that has a large context window (`100k+` tokens), you can see firsthand how the memory usage grows rapidly.

### Determine Your Context Memory Needs

If you are doing simple chat a relatively small context window of `8k` or `16k` tokens is usually sufficient. Coding on the other hand can benefit from a larger context window (especially with more powerful models) and it isn't uncommon to need `100k` tokens or more. A simple autocomplete model can get away with just `2k` or `4k` tokens.

You need to determine what you are using this model for and choose an appropriate context length based on that usage. For coding I would recommend getting the most powerful model you can while still maintaining a decent context window size (`32k+` tokens). It does not usually make sense to use a smaller model with a larger context window in place of a more powerful model with a smaller context window unless that context window is so small it is impacting your ability to work effectively.

## Optimizing Memory Usage

Changing the size of your context window is one way to optimize your memory usage, but you can also modify how you KV cache is stored as well.

### KV Cache Offload

Offloading the KV cache to a slower but larger memory (like system RAM or disk) can help free up precious VRAM. This comes at the cost of increased latency when accessing the KV cache, so it's a trade-off between memory usage and performance.

If you are trying to load a model at your system's limits offloading the cache can actually increase your speed since the VRAM is freed up for the model weights and other critical operations.

### KV Cache Quantization

KV cache quantization reduces the precision of the stored key and value tensors, which can significantly lower memory usage. This comes at the cost of some potential loss in model accuracy. This is only something I would consider if the extra memory savings allow me to load a larger model than I could otherwise fit into memory.

### Unified KV Cache

You can setup your model to run multiple concurrent predictions to increase generation speed, but doing so will increase the memory footprint of your model significantly, as each concurrent request requires its own KV cache and working state.

Enabling a unified KV cache allows multiple concurrent requests to share the same KV cache, which can help reduce the overall memory footprint. However, this can impact performance slightly.

I would recommend always having this enabled as the memory savings usually outweigh the slight performance impact.

### Batch Sizes

You can configure the evaluation and physical batch sizes for your model. Larger batch sizes can improve throughput but will also increase memory usage, so it's important to find a balance that fits within your available resources.

This is probably one of the least important factors to worry.

### GPU Offload

One setting you should probably never set below the maximum is the GPU offload. By setting this anywhere below the max value your model will be partially loaded outside your GPU which will drastically reduce performance due to the slower memory access.

If you really want to use a model larger than your memory allows it should only be used for tasks that you do not care about speed on.

<!-- TODO: Demo showing the impact of different memory management strategies on model memory usage and performance -->
