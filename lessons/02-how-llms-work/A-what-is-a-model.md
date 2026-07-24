---
title: "What Is a Model"
description: "Learn what a model is, how neural networks use weights and parameters, and why open weights are just files full of numbers."
---

Before we can talk about LLMs, we need to understand what a model is. The word `model` sounds complicated, but the basic idea is actually pretty simple. A model takes some input, does a bunch of math with that input, and gives you an output.

You already write functions that do this every day. A function that converts Fahrenheit to Celsius takes a number and returns a number. The difference is that you write the formula for that function. With a model, we give it examples and let it learn the formula for itself.

## A Simple Model

Imagine we want to make a model that darkens a color by 10%. It receives the red, green, and blue values of a color and returns a slightly darker version of that same color.

![A neural network that receives red, green, and blue inputs and produces darker red, green, and blue outputs.](/fem-getting-started-with-local-ai-setup/images/01-how-llms-work/A-what-is-a-model/rgb-neural-network.svg)

For one specific input, we could just write the formula ourselves.

```js
function darkenColor(red, green, blue) {
  return {
    red: red * 0.9,
    green: green * 0.9,
    blue: blue * 0.9,
  }
}
```

That is a great solution when we know the exact rules. Models are useful when the rules are too hard to write down or are ambiguous. For example, creating a color that appears 10% darker is not actually as simple as multiplying each RGB component by 0.9 since how we perceive colors is subjective and context-dependent.

## Nodes, Layers, Weights, And Parameters

A neural network is made of small calculations called **nodes**. Nodes are organized into **layers**. Each node receives values from previous nodes, adds them together, and then passes a new value to the next layer.

The lines between nodes each have a number associated with them. That number is called a **weight**. A weight controls how much one value affects the next calculation. A model's **parameters** are all of the values it learned which in large models is mostly made up of its weights.

![A closer view of one node combining inputs with learned weights before passing a value forward.](/fem-getting-started-with-local-ai-setup/images/01-how-llms-work/A-what-is-a-model/weighted-node.svg)

Even in this very simple example, changing a weight changes the output. A larger red weight could make the output depend more on the red input. A smaller one could make it depend less. Training is the process of finding useful values for all of those weights.

Real models have far more layers and parameters than this diagram. An LLM has billions or even trillions of parameters. The core idea does not change, though. It still turns inputs into outputs by repeatedly applying learned numerical values.

## Training And Inference

There are two different times in a model's life that are easy to mix up.

During **training**, we show the model examples. For our color model, that may be an original RGB color and the correct color after it has been darkened. The model makes a prediction, compares it to the correct answer, and adjusts its weights a tiny amount. It repeats that process over and over.

During **inference**, the weights are fixed. We give the trained model a new input and ask it for an output. When you run a model, you are doing inference. You are not retraining the model every time you send a message.

## What Open Weights Actually Means

When people say a model has open weights, they mean you can download the learned parameter files. Those files are mostly arrays of numbers. They are not source code that explains how the model thinks.

Here is a tiny fictional example of what some weights could look like.

```json
{
  "layer_1.weights": [0.12, -0.81, 0.44, 0.03],
  "layer_1.bias": [0.19, -0.27]
}
```

Real weight files are much larger and use efficient binary formats, but the contents are still numerical values like these. A 7-billion-parameter model has roughly 7 billion learned values to store.

Open weights does not automatically mean open source. The training code, training data, and other components of the model may not be available openly. This doesn't really matter much, though, as the part you are using are the weights which is what needs to be open and accessible.

The main thing to remember is that a model is a learned function. Training creates the parameters, and inference uses those parameters to turn new inputs into useful outputs.
