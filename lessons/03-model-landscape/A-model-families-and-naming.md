---
title: "Model Families and Naming"
description: "Learn how to read a model name and what model families are."
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

## Finding Up To Date Models

Finding the most up to date models is difficult since it changes so fast. I recommend a Google/AI search for the best current local model families and then from there you can find the best model in each of those families for your specific needs.

The best place to find models once you know what you want is [Hugging Face](https://huggingface.co/models) which we will cover in depth in the next lesson.
