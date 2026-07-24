---
title: "Model Families and Naming"
description: "Learn how to read a model name, use model cards, and identify the details that matter before you download a model."
---

Knowing which models to choose is one of the hardest parts of getting started, especially since new models come out all the time. We need to learn how to read model capabilities and understand the details that matter before downloading or using a model.

## Model Families

A **model family** is a group of related models released by the same organization. Models in a family usually share an architecture, training approach, and naming pattern. Some common model families for coding are:

- Qwen
- Llama
- Gemma
- Mistral
- GLM
- DeepSeek
- Kimi

Newer family versions usually improve on older ones, but a newer version is not automatically the best choice. A small new model can still be less capable than a large older model. This is why you need to look beyond the family name.

### Finding Up-to-Date Models

The most up to date models are constantly changing.

One of the best ways to find the latest coding models is to just do a Google/AI search for the best local/open source coding models. This will give you a starting point on the model families and versions that are currently the most relevant and from there you can narrow your search.

## Reading A Model Name

Not all model names follow a specific pattern, but you can often gleam some useful information about a model just from the name of the model itself. Let's look at the Qwen model we loaded earlier as an example.

```txt
Qwen2.5-Coder-7B-Instruct
```

- `Qwen` is the model family.
- `2.5` is the family version.
- `Coder` means this model was tuned for programming tasks.
- `7B` means it has roughly 7 billion parameters.
- `Instruct` means it was trained to follow instructions in a chat-like format.

Not every model is as helpfully named, though. For example, `GLM 5.2` does not indicate any information about the model other than the family and version.

## Base vs Instruct Models

One important thing to understand is the difference between base and instruct models since it affects how you should use them and what tasks they are best suited for.

### Base Model

A base model is the foundational model in a family. It has been trained on a large corpus of text but has not received additional fine-tuning for specific tasks. You generally want to avoid base models unless you plan to fine tune them yourself.

### Instruct Model

An instruct model starts with a base model and receives additional training to follow user instructions and conversations. If you want to chat with a model an instruct model is almost always the right starting point. Instruct models can also be used for coding tasks, but it is important to ensure these models have reasoning capability since without it they lack the ability to perform more complex tasks.

You may see names such as `Instruct`, `Chat`, or `IT`. These generally indicate an instruction-tuned model.

## The Model Card Is The Source Of Truth

One of the best places to find open-weight models is on [Hugging Face](https://huggingface.co/models). A model's page includes a model card written by its publisher or uploader. This is where you should look before downloading a model.

Check the model card for:

- The intended tasks and supported languages
- The parameter count and context window
- The recommended prompt or chat template
- Benchmark results and known limitations
- The license and commercial-use terms
- The supported formats and available quantizations

Benchmarks can help you compare candidates, but they are not a promise that a model will work well for your task. A coding benchmark does not tell you how well a model understands your codebase, follows your prompts, or runs on your hardware.

I mostly use these model cards as a way to determine if a model will fit my needs and if that model will fit within my hardware constraints. I also use these model cards to configure the model properly before running it since many models have specific settings you should follow to get optimal performance.

TODO: Maybe add a section where I show this information on hugging face (DO A DEMO)
