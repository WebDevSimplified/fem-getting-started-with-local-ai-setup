---
title: "Model Types By Task"
description: "Learn the common types of AI models and how to choose one that matches the task you want to perform."
---

It is easy to treat every model as a chatbot, but many models are trained for specific jobs. This is becoming less the case with newer, larger models that are more general-purpose, but understanding the model's intended task can still help you choose the best one for your needs.

## General-Purpose And Coding Models

A **general-purpose model** is a good default for conversation, rewriting, summarizing, extracting information, and answering general questions. These models are flexible, but they are not always the strongest option for specialized work.

A **coding model** receives extra training on programming languages, code explanations, and common development tasks. Use one when you want help writing code, reviewing a function, explaining an error, or working through a technical problem.

A coding model won't always be the best option for coding, though. A larger or newer general purpose model will often outperform an older/smaller coding model.

## Instruct Models

An **instruct model** is trained to follow detailed instructions and provide responses that align closely with user intent. These models excel at tasks where you need precise control over the output, such as generating structured content, following step-by-step instructions, or adhering to specific formatting requirements.

These models are often labeled as `Instruct`, `Chat`, or `IT`.

## Reasoning Models

Some models are tuned to spend more time working through difficult problems before giving you an answer. These are often called **reasoning models**.

They can be useful for multi-step logic, planning, and difficult debugging. The tradeoff is that they usually take longer to respond and can use more tokens. For a simple task, that extra work is often unnecessary.

Most programming tasks benefit from reasoning models, especially when the task involves multiple steps or complex logic.

These models are often labeled as `Reasoning` or `Thinking`.

## Vision And Multimodal Models

A **vision model** can accept images along with text. These models can describe an image, read a screenshot, or answer questions about a diagram.

A **multimodal model** is a broader term for a model that accepts or produces more than one kind of data (for example text, images, videos, audio, etc).

In order to use these multimodal capabilities, though, you need to be running the model in an environment that supports the additional data types, such as images or audio.

## Function And Tool Calling

Many instruction models are trained to support tool calling as well. If you are doing any coding task then tool calling support is a must have and if a model does not support tool calling it will not work with your development workflow.

## Embedding And Reranker Models

An **embedding model** turns text into a list of numbers called an embedding. Similar pieces of text create similar embeddings, which makes these models useful for semantic search and retrieval.

A **reranker model** receives a search query and a small list of possible results. It scores those results so your application can put the most relevant ones first.

These models are not useful for coding or chat, but are ideal if you are trying to build a RAG (retrieval-augmented generation) system.

## Combinations

Most medium or larger models will support more than one of these capabilities. For example, Qwen 3.6, a model we will use later, supports reasoning, vision input, and tool calling. Our Qwen 2.5-Coder model which we used earlier does not support any of these features since it is an older and much smaller model.
