---
title: "Finding Models On Hugging Face"
description: "Learn how to search Hugging Face, evaluate a model repository, and identify the right files to download."
---

Hugging Face is the main place to find open models, but it can be overwhelming at first. There are thousands of uploads for the same model family, and the most downloaded result is not always the one you should use.

## Reading The Model Page

Before we start diving into search and filters it is best to look at a model card so we can understand what information we even want to filter by.

[Qwen3.6-35B-A3B Model Page](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)

The main page of the model will contain a detailed write up by the uploader of the model. This includes all the information about the model's intended use, limitations, capabilities, and any other relevant details that can help you decide if the model is suitable for your needs.

### Header

At the top of the model page you will see a header which contains the following:

- Model name
- Uploader name
- Tags/keywords associated with the model
- Like count

This information is useful for identifying if the model comes from a reputable source and if it is likely to meet your needs.

### Sidebar

Next to the main writeup is a sidebar which contains most of the important information you will need.

The top of the sidebar lists:

- Parameter count
- Download count
- Model format
- Model architecture

#### Quantizations

Some models are available in quantized formats and those will be listed next in the sidebar.

[Qwen3.6 Quantized Model Example](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF)

We will go into much more depth on quantizations in the next module.

#### Model Tree

The model tree is one of the most important parts of the model page since it tells you what models this model is based on and any derived models.

If you are viewing a top level (base) model you will often see the following in the tree.

- **Adapters:** These are additional modules that can be applied to the base model to extend its capabilities or fine-tune it for specific tasks.
- **Finetunes:** These are models that have been fine-tuned from the base model for specific tasks or datasets.
- **Merges:** These are models that have been created by merging two or more base models together.
- **Quantizations:** By far the most common, these are models that have been converted into a lower-precision format to reduce memory usage and improve inference speed.

If you are viewing a derived model, the tree will show the model it is based on (and any models that model is based on) as well as any models derived from it.

#### Collections

Collections are groups of models that are created by the uploader of the model. Collections often group together similar models, such as different sizes of the same model, or different formats and is a great place to look if you need a slightly different version of the model.

#### Evaluation Results

This is just a list of benchmark scores that you can use as a first pass to determine if a model is actually worth downloading or not.

## Search and Filtering

On the main [Hugging Face Models page](https://huggingface.co/models), you can filter for pretty much anything you want from the sidebar or filter by a specific model/family name if you know what model you want.

If you aren't sure what model you want I would recommend using the following filters.

- **Task:** Set this to `Text Generation` or `Image-Text-to-Text` for a chat or coding model. You can also leave this blank since many models don't specify a task and will not show up.
- **Parameters:** Filter the model by size to remove all the models too large or small for your system.
- **Base Only:** This will only show base models which will drastically reduce your list and make it easier to find the model you need.
- **Apps:** You can set this to LM Studio to only show models that are compatible with LM Studio, but this is not compatible with `Base Only` since base models will not work in LM Studio. Only use this when trying to find quantizations of models.
- **Libraries:** This lets you filter by the format of the model so you can match it to your specific hardware setup.

You can sort results by downloads, likes, recently updated, or trending, but just know that downloads/likes tend to not show great results since it skews towards much older models that were very popular on release. Trending is usually the best sorting option.

## Check Who Uploaded The Model

The uploader name is one of the first things I check. An official organization, such as `Qwen`, `meta-llama`, `google`, or `mistralai`, usually publishes the original model files and documentation. Those repositories are the best source for understanding what the model actually is.

For local use, you will also see community uploaders. They often convert official models into formats such as `GGUF`, create quantized versions, or package them for a particular runtime. You will start to notice there are some community uploaders that are very trusted and produce tons of models. `Unsloth`, for example, is a great source for quantizated versions of pretty much any model you will need.

## Downloading A Model

Downloading a model may seem simple, but it is a bit more complex then it first appears. Most likely you will end up on a base model page for your first model. [Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B), for example. There is no download button on this page and if you click `Use this model`, there is no option for LM Studio. This is because you need to find a version of the model that is supported by LM Studio first.

To do this click the `Browse Quantizations` link in the `Use this model` dropdown, or click `Quantizations` in the model tree. This will show you a list of all quantizations. From here I would recommend filtering by `Apps` and selecting `LM Studio` to ensure you only see models compatible with LM Studio. Now click on any of the options (I like to go with Unsloth if I have the option).

On this new quantized model page there is a list of all the quantized model options in the sidebar and you can click on any of those options or you can click `Use this model` and then `LM Studio` to download and use the model directly in LM Studio. Inside LM Studio you will have the option to choose any of the quantized versions you see on the model page from a dropdown.

### Try It Yourself

Now I want you to try downloading a model to use in LM Studio. [LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B) will be the base model I want you to start from. Remember you need to find a quantized version and download that (Unsloth is a great option for quantized models, but use whatever you want).

When downloading a quantized version, select any of the options in the `4-bit` category or use the `Use this model` dropdown which will default to quantization that fits best on your system.

**IMPORTANT:** Also, [download this model](lmstudio://open_from_hf?model=unsloth/Qwen3.5-9B-MTP-GGUF&file=Qwen3.5-9B-Q4_K_S.gguf) as we will be using it later.
