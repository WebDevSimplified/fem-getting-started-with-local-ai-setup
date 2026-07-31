---
title: "Why Choose Local AI?"
description: "Learn when local models make sense, where cloud frontier models are stronger, and why local AI skills matter to companies."
---

Running AI locally on your machine for _free_ sounds like a dream come true, but in reality there are certain tradeoffs you need to consider when working with local models that you don't have to worry about with cloud models.

## Why Run Models Locally

Before we dive into some of the negatives of local AI, let's first look at the benefits.

Local AI can give you:

- **Privacy**: Your model and data stay on your machine. This is useful for private code, HIPAA, personal documents, or data that your company cannot send outside its own systems. Even if you use a Chinese model your data is never actually sent to China.
- **Offline access**: You do not need an internet connection to run local models.
- **Control**: You can choose the model, decide how it runs, adjust its settings, and customize it to your exact needs.
- **Fine Tune**: You can fine-tune and retrain local models on your own data, improving their performance for your specific use cases (even small models will outperform larger models when tuned properly).
- **Provider independence**: You are not tied to one provider changing its prices, rate limits, available models, or policies.
- **Lower usage costs**: A cloud API charges for every request and every token it processes. Once you have the hardware, a local model has no per-request API cost other than the energy required to run the hardware itself.

## Local Models Are Not Always Better

The best cloud frontier models are generally more capable than models you can run on your own (even with very powerful hardware). Cloud models are often the better choice when you need:

- Difficult reasoning
- Complex coding tasks
- Large amounts of context
- The highest possible quality
- Fast response times (running large local models can be quite slow)

When it comes to coding specifically you need to be a bit more careful with local models since they struggle with more ambiguous or larger tasks compared to cloud frontier models.

In my experience local AI models that you can run on consumer hardware tend to be 3-12 months behind the latest cloud frontier models depending on your hardware and the model you choose.

## Use The Right Model For The Task

Most AI work does not need a frontier model. A local model can often handle:

- Parsing/writing documentation
- Writing tests
- Implementing simple or well documented features
- Fixing bugs
- Answering questions

For example, you could use a large frontier model to parse difficult or ambiguous tasks, but have that model spin up sub-agents running local models to implement the code.

You do not need to pick local or cloud and use that choice forever. Use both:

- Route easy and medium tasks to a local model.
- Use a cloud frontier model when its extra capability is worth the cost.

The goal is not to avoid cloud models. The goal is to understand the tradeoffs well enough to use local and cloud models where each one makes the most sense.

## A Valuable Company Skill

As AI API usage costs increase, companies need people who can create local AI setups. Running every request through the largest available cloud model is easy, but it is often far more expensive than necessary.

Someone who understands local models can:

- Evaluate which tasks need a frontier model and which do not.
- Choose a model that is good enough for a specific task.
- Build a workflow around the available hardware.
- Keep sensitive data under the company's control.
- Avoid depending entirely on a single AI provider.
- Save significant money when simple or medium-difficulty tasks happen thousands of times each day.

### Example Cost Savings

Imagine your company has 10 developers who each use $1,000 worth of tokens per month (a conservative estimate). That is $10,000 in AI costs each month and a huge chunk of those costs could potentially be saved by routing simpler tasks to local models. Even if only 30% of all tasks were handled locally, that could save $3,000 each month.

It isn't hard to see how as AI prices increase, companies grow, and developers use more tokens that this cost-saving approach could become increasingly valuable over time. Bringing these skills to a company will easily make you a highly valuable team member and more than likely pay for your entire salary in how much money you could save the company each year.

Companies also have the capital to buy much more powerful machines that can run local models that are able to compete with even the best cloud frontier models, meaning you can potentially replace 90-100% of your cloud AI usage with local models which can bump that savings number up to $9,000-$10,000 each month. Within a year that is over $100,000 in potential savings which can purchase a very high end server for your local AI needs.
