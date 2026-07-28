---
title: "Dense Models, MoE, And MTP"
description: "Learn what dense models, mixture-of-experts models, and multi-token prediction mean for local model performance."
---

Model architecture labels can make a model page feel more complicated than it needs to be. You do not need to understand every internal detail to choose a model. You only need to know how these labels affect memory use, speed, and the way you compare models.

## Dense Models

Most models you will encounter are **dense models**. When a dense model processes a token, it uses all of its parameters for that calculation. This is how all the frontier models you are used to work.

A `7B` dense model has roughly 7 billion parameters, and each generated token uses the whole model. This makes the parameter count a useful starting point for estimating how much memory the model needs and how fast it might run.

Dense models are straightforward to compare, but parameter count is still not a quality score. A newer `7B` model can outperform an older or differently trained `13B` model on a specific task.

Since dense models require all of their parameters to be used for every token, they tend to be the slowest option and the most memory intensive, but they often produce better results.

## Mixture Of Experts

A **mixture-of-experts**, or `MoE`, model has multiple expert networks inside some of its layers. Each expert is essentially a smaller neural network that works very similar to the full model.

The model also has a router. For every token, the router decides which few experts should process that token. This is where the name mixture of experts comes from.

Imagine you ask a model to create a React component and write a Python test for it. One expert may have learned patterns that are especially useful for frontend JavaScript, while another may be better at Python. The router can activate both of those experts while leaving unrelated experts inactive.

![A code prompt enters a router, which activates frontend JavaScript and Python experts while leaving SQL and translation experts inactive.](/fem-getting-started-with-local-ai-setup/images/03-model-landscape/C-dense-moe-and-mtp/moe-routing.svg)

This example is abstract. Experts are not labeled `frontend` or `Python` inside a real model, and one expert can help with many kinds of patterns. The useful mental model is that the router learns which experts are most useful for the current token.

You may see an MoE model named like this:

```txt
8x7B
or
A3B
```

In the first example this says the model has 8 experts that are each 7B parameters large. The second example doesn't say how many experts the model has but is says each expert is 3B parameters large.

TODO: Do demo showing MOE with large model that barely fits and also MOE with model that comfortably fits.

### Why MoE Can Be Faster

MoE models are great for lower-end hardware since they require less computation for each token. This means even if the full model does not fit on your GPU, it may still be able to generate tokens efficiently since the lower parameter count experts can run somewhat efficiently on the CPU.

Also some of the experts may not be needed for each token which may mean the entire computation is done on just the GPU if the experts utilized live fully on the GPU. This selective activation is what allows MoE models to be both large in capacity and efficient in computation.

TODO: Do demo showing how small models can still run fast on CPU by using the Qwen 2.5 model from earlier.

### MoE Tradeoffs

The biggest tradeoff with an MoE model is that it will not give quite as high quality responses as a dense model of the same size since an MoE model is only using a portion of its total parameters for each token. Overall this isn't a massive drop in quality and usually you will have better responses by using a larger MoE model vs a smaller dense model for the same hardware constraints.

## Multi-Token Prediction

Most language models predict one token at a time. **Multi-token prediction**, or `MTP`, is an architecture feature that lets a model predict more than one future token during a generation step.

The goal is to improve generation speed. A model that can accurately predict multiple upcoming tokens may need fewer full passes through the model to produce the same response which can result in 1.5x-2x increases in speed.

`MTP` models may not always increase speed, though, so I recommend testing it with your specific prompts and hardware to see if it provides a benefit. Also, `MTP` models take up more memory since they need to store multiple predicted tokens at once which can be a limiting factor on devices with less memory.

TODO: Use prompt `Write a JavaScript function that returns the largest number in an array.` with model `qwen-3.5-9B-mtp` to compare MTP to non-MTP (also show configuration options for draft tokens and so on).
