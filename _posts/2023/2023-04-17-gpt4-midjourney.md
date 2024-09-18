---
layout: single
title: "Prompting Midjourney with GPT-4 (Part I)"
date: 2023-04-17 21:45 -0400
categories: art
published: true
---

One of a series of little experimental projects that I have been doing with [Midjourney v5](https://docs.midjourney.com/docs/quick-start) and GPT4 (via [OpenAI ChatGPT Plus](https://openai.com/blog/chatgpt-plus)). Sometimes it’s tough to find the right words to convey an idea.So why not leverage an LLM that knows all the words and ask it to help us talk to the other LLM? It’s pretty rad.

GPT4 Prompt: Give me a 10-15 word sentence summarizing the compositions and subjects of _La Città Nuova_ by [Antonio Sant'Elia](https://en.wikipedia.org/wiki/Antonio_Sant%27Elia), followed by 10 to 15 short phrases, comma-separated, describing the style and aesthetics, then a list of the methods and materials used by the artist in creating the works.

GTP4 Response: […] depicts innovative urban structures featuring interconnected, multi-level living spaces. Futuristic, dynamic, geometric, bold lines, vertical, industrial aesthetic, monumental, integrated infrastructure, elevated transportation, modern metropolis. Ink on paper, architectural drawings, perspective sketching.

Midjourney Prompt: innovative urban structures featuring interconnected, multi-level living spaces. Futuristic, dynamic, geometric, bold lines, vertical, industrial aesthetic, monumental, integrated infrastructure, elevated transportation, modern metropolis. Sepia, ink on paper, architectural drawing, perspective sketch, white background –v 5

Midjourney gave these as the responses:

{% include figure popup=true image_path="/images/2023-04-17_01.jpg" alt="Midjourney Result 1 of 2" caption="Midjourney Result 1 of 2" %}
{% include figure popup=true image_path="/images/2023-04-17_02.jpg" alt="Midjourney Result 2 of 2" caption="Midjourney Result 2 of 2" %}

For comparison, here are two of Sant'Elia’s drawings from _La Città Nuova_:

{% include figure popup=true image_path="/images/2023-04-17_03.jpg" alt="La Città Nuova Example 1 of 2" caption="La Città Nuova Example 1 of 2" %}
{% include figure popup=true image_path="/images/2023-04-17_04.jpg" alt="La Città Nuova Example 2 of 2" caption="La Città Nuova Example 2 of 2" %}