---
title: "Choosing Hardware for Local AI"
description: "Learn how to choose local AI hardware based on memory, speed, cost, power use, and the models you want to run."
---

There is no single best computer for running local AI. A machine that is perfect for a small coding model can be a frustrating choice for a large reasoning model, and a machine with huge memory can still feel slow if it does not have enough compute power.

This is why you should choose hardware based on the work you actually want to do. Before looking at a single GPU or laptop, answer these questions:

- What size models do you want to run?
- Do you care more about fast responses or fitting larger models?
- Will you use one model at a time, or serve several people and applications?
- Do you need to run models away from your desk?
- How much are you comfortable spending up front and each month?

## Start With The Model You Want To Run

The most important hardware specification for local AI is usually available memory. You need enough memory for the model weights, the context window, the KV cache, and the rest of your operating system. If the model does not fit, no amount of extra GPU speed will fix that problem.

For most people, this creates three broad hardware targets.

| Hardware target | Good for | Typical tradeoff |
| --- | --- | --- |
| Smaller memory pool | Small chat, coding, autocomplete, and embedding models | Fast and affordable, but limits the model sizes and context lengths you can use |
| Large dedicated VRAM pool | Fast local inference and several concurrent requests | Excellent speed, but high-VRAM GPUs get expensive quickly |
| Large unified memory pool | Larger models on a single consumer machine | More memory per dollar at the high end, but usually less raw inference speed than a comparable dedicated GPU setup |

Quantization changes these boundaries. A quantized model uses less memory than the original full-precision model, which is why a model that would normally be impossible to run can fit on consumer hardware. You still need to leave room for the KV cache and your other applications, though. A model that barely fits will often be slow or unstable once you use a longer context.

## Hardware That Optimizes For Memory

If your goal is to run the largest possible model locally, prioritize memory capacity first.

### Unified Memory Machines

Apple Silicon machines are a common choice for this use case because the CPU and GPU share one large unified memory pool. You can buy a machine with far more usable model memory than you would get from a typical consumer GPU, without needing to build a multi-GPU desktop.

This makes unified memory especially appealing for developers who want to run larger quantized models, work from a laptop, and keep their setup simple. The tradeoff is that unified memory is shared with everything else on the machine. If your model uses most of it, you have little room left for your editor, browser, Docker containers, or other applications.

Unified memory also does not automatically make a machine faster. It solves the problem of fitting a larger model. A dedicated high-end GPU can often generate tokens more quickly when both machines can fit the same model.

### Dedicated High-VRAM GPUs

Dedicated GPUs use their own VRAM. This is generally the best option when you care about speed, especially for interactive coding assistants, tool use, image generation, or serving multiple requests at once.

The problem is that VRAM gets expensive fast. Mid-range GPUs often have enough memory for smaller quantized models, while workstation and data-center GPUs can hold much larger models but may cost several times as much as the rest of the computer. Before buying a GPU, check its VRAM capacity first and benchmark results second. A very fast GPU with too little VRAM is still the wrong GPU for the model you want to run.

### System RAM And CPU Inference

You can also run models in system RAM with your CPU. This is the lowest-cost way to experiment because every computer already has a CPU and RAM. It is a reasonable option for small models, occasional use, or testing whether local AI is useful to you.

CPU inference is much slower than GPU inference for most LLM workloads. I would not build a daily coding workflow around a large CPU-only model unless you are comfortable waiting for responses. It is often better to run a smaller model quickly than a larger model so slowly that you stop using it.

## Hardware That Optimizes For Speed

If you already know your target model fits in memory, speed becomes the deciding factor. A compatible dedicated GPU is usually the strongest option here because neural-network inference involves a huge number of parallel calculations.

Nvidia GPUs are the easiest path for many local-AI tools because CUDA support is widespread. AMD and Intel hardware can still work, but software support and setup quality vary more by operating system and runtime. Apple Silicon is also very capable for personal local inference, especially when you value portability and memory capacity, but it uses a different acceleration stack than CUDA.

When comparing speed, look for measurements that match your workload:

- **Time to first token** matters when you are chatting or waiting for an agent to begin work.
- **Tokens per second** matters when you are reading longer responses or generating code.
- **Concurrent throughput** matters when several people or applications share one server.
- **Prompt-processing speed** matters when you send long files, retrieval results, or large conversation histories.

Do not compare a benchmark result without checking the model, quantization, context size, runtime, and batch size. Those details can change the result dramatically.

## One GPU, Multiple GPUs, Or A Remote Server?

A single GPU is the simplest dedicated local-AI setup. It is easier to configure, easier to cool, and usually gives you the fewest surprises. For most individual developers, this is the best desktop starting point.

Multiple GPUs can combine their memory for some runtimes and model formats. This can let you run models that would not fit on one card, but it adds hardware cost, power draw, heat, noise, and setup complexity. The connection between GPUs can also become a performance bottleneck. Only consider this once you have a specific model that does not fit on your single-GPU setup.

A remote server is another option. You can rent a GPU by the hour, keep a more powerful machine at home, or use a private server at work. This avoids carrying expensive hardware everywhere, but you need reliable networking and you need to secure the model endpoint. We will cover remote access later in the course.

## Comparing Up-Front Costs

Hardware prices move constantly, but the shape of the decision is fairly stable.

| Option | Up-front cost | Strength | Main limitation |
| --- | --- | --- | --- |
| Use your existing computer | $0 beyond possible RAM upgrades | Best way to learn and test small models | CPU-only inference can be slow |
| Consumer GPU desktop | Moderate | Strong speed for models that fit in VRAM | VRAM capacity is limited at lower prices |
| High-VRAM workstation GPU | High | Large models and high throughput | The GPU can cost more than the entire rest of the computer |
| High-memory Apple Silicon machine | High | Large unified-memory pool in a quiet, portable computer | Less upgradeable and not always the fastest option |
| Rented GPU server | Low up-front cost | Access to powerful hardware when needed | Ongoing hourly cost and a network dependency |

I generally recommend starting with the hardware you already own. Run a few models, measure how often you use them, and identify the exact limitation you hit. You may discover that a smaller local model handles most of your tasks, or you may discover that you need more memory far more than you need more speed. That information is much more useful than buying the most expensive hardware you can afford.

## Operating Costs Matter Too

The purchase price is not the full cost of a local setup. A powerful desktop can use a meaningful amount of electricity when it runs models for hours each day. It also produces heat, which can increase cooling costs and make a home office less comfortable.

You can estimate electricity cost with this formula:

$$
\text{monthly cost} = \frac{\text{watts}}{1000} \times \text{hours per month} \times \text{electricity price per kWh}
$$

For example, a computer that averages $400\text{ W}$ while generating and runs for $60$ hours per month uses about $24\text{ kWh}$. At $0.15$ per kWh, that is about $3.60$ per month. The actual number depends on your hardware, workload, idle time, and local electricity price, but this calculation gives you a useful baseline.

Local hardware also has maintenance costs. You may eventually need more storage for models, more RAM, better cooling, or an upgrade when your current machine no longer fits the models you want to use.

## Local Models Can Reduce Frontier Token Costs

Running a model locally is not free, but it can reduce your usage of paid frontier APIs. This is especially useful for repetitive tasks such as autocomplete, summarization, classification, embeddings, local document search, and first-pass code review.

The best setup is often a hybrid one:

- Use a local model for private, frequent, or lower-stakes tasks.
- Send difficult reasoning, high-quality writing, or tasks that need the strongest available model to a frontier API.
- Route work based on quality, privacy, latency, and cost instead of assuming every task needs the same model.

You should compare the cost of your hardware against the API spending it replaces, not against all API spending. If a local model handles $50$ of frontier-model requests each month, it does not matter that you still use a frontier model for a few difficult tasks. The local system is still saving you money and keeping more of your data on your own machine.

## A Practical Buying Checklist

Before buying hardware, write down the model you want to run, its quantization, your target context length, and how many simultaneous requests you need. Then check these items in order:

1. Confirm the model and context fit in available memory with room for the rest of your system.
2. Confirm that your operating system and runtime support the hardware acceleration you expect to use.
3. Find a benchmark using a similar model, quantization, and context size.
4. Include the full system cost, power use, storage, cooling, and possible upgrades.
5. Compare that total with the frontier token cost you realistically expect to avoid.

This may seem like a lot to consider, but it prevents the most common expensive mistake in local AI: buying hardware based on a single impressive specification instead of the models and workflows you actually plan to use.