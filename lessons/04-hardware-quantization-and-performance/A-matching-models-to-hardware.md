---
title: "Matching Models To Your Hardware"
description: "Learn which hardware details affect local models and how we will use them to find compatible models on Hugging Face."
---

Just because a model has open weights does not automatically mean you can run it on your hardware. Before we download anything, we need to know what our computer can realistically handle.

## Start With The Hardware You Have

We already covered why CPUs, GPUs, VRAM, RAM, and unified memory matter for running models. Now we are going to use that information to find models that fit your actual computer.

The details we care about are:

- Your GPU and its available VRAM
- Your system RAM, or total unified memory on Apple Silicon
- Whether you need real-time speed or can wait longer for a response

The last one matters more than it may seem. You can run a quite powerful model even on mediocre hardware if you are willing to wait for responses.

### Find Your Hardware Details

Depending on your operating system you will find your hardware specifications in different places.

#### Windows

On Windows you can open the **Task Manager** and use the **Performance** tab to see your hardware as well as the current load on your system.

#### Mac

On Mac you can open **Activity Monitor**, specifically the **Memory** tab, to view your total system memory and current usage.

#### Linux

On Linux, you can use the `top` or `htop` commands in the terminal to view your hardware details and memory usage.

## How to Find Models That Fit Your Hardware

Once you have your hardware details, you can input that data into [Hugging Face](https://huggingface.co) to find models that make sense for your machine.

[Set Your Hardware Details in Hugging Face](https://huggingface.co/settings/hardware)

You can also specify which runtimes you use most often to fine tune the list of download options from hugging face

[Set Your Preferred Runtimes in Hugging Face](https://huggingface.co/settings/local-apps)

### Filter Models

Now that you have this information it is much easier to find models that will specifically fit your hardware. You can even filter to only show models that fit within your hardware constraints or runtime.

In the next lesson, we will look at quantization, which will help us run large models on limited hardware.

### Quantizations

Once you have your hardware information on Hugging Face, it will show you which quantization files are most likely to fit within your hardware. This is a great way to see at a glance what models work best for your system.

### Try It Yourself

Go ahead and add your hardware details to Hugging Face and spend a bit of time using that data to filter models and view which quantizations work for your system.
