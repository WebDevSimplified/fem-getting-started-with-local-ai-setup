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

The Qwen 3.5 9B model is a great option since its max context size is over 256K tokens. LFM2.5 8B A1B also has an over 100K token context size if you cannot load the larger Qwen model.

### Determine Your Context Memory Needs

Depending on your use case you may need more or less context.

- **Simple Chat:** When just chatting with an AI you can get away with relatively small context windows of `8k` or `16k` tokens.
- **Coding:** When using the model for coding tasks, larger context windows of `100K` tokens or more are often beneficial so the model can fit your code into context, but you can get away with smaller contexts of `32K` tokens for simpler tasks.
- **Autocomplete:** For simple autocomplete tasks (tab completion), smaller context windows of `2k` or `4k` tokens are usually sufficient since the autocomplete only needs to know the immediate context of your code.

## Optimizing Memory Usage

Changing the size of your context window is one way to optimize your memory usage, but you can also modify how you KV cache is stored as well.

### KV Cache Offload

Offloading the KV cache to a slower but larger memory (like system RAM or disk) can help free up precious VRAM. This comes at the cost of increased latency when accessing the KV cache, so it's a trade-off between memory usage and performance.

If you are trying to load a model at your system's limits offloading the cache can actually increase your speed since the VRAM is freed up for the model weights and other critical operations.

### KV Cache Quantization

KV cache quantization reduces the precision of the stored key and value tensors, which can significantly lower memory usage. This comes at the cost of some potential loss in model accuracy. This is only something I would consider if the extra memory savings allow you to load a larger model than you could otherwise fit into memory.

### Unified KV Cache

You can set up your model to run multiple concurrent predictions to increase generation speed, but doing so will increase the memory footprint of your model significantly, as each concurrent request requires its own KV cache and working state.

Enabling a unified KV cache allows multiple concurrent requests to share the same KV cache, which can help reduce the overall memory footprint. However, this can impact performance slightly.

I would recommend always having this enabled as the memory savings usually outweigh the slight performance impact.

### Batch Sizes

You can configure the evaluation and physical batch sizes for your model. Larger batch sizes can improve throughput but will also increase memory usage, so it's important to find a balance that fits within your available resources.

This is probably one of the least important factors to worry about and can just be left as the default.

### GPU Offload

One setting you should probably never set below the maximum is the GPU offload. By setting this anywhere below the max value your model will be partially loaded outside your GPU which will drastically reduce performance due to the slower memory access.

If you really want to use a model larger than your memory allows it should only be used for tasks that you do not care about speed on.

### Try It Yourself

Try loading any model and play around with modifying the context size, KV cache configurations, and GPU offload to see how the different changes impact your performance and memory usage.
