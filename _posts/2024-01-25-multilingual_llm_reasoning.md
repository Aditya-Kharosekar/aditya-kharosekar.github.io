---
layout: post
title: Curriculum learning and bilingual training could help LLMs do math in Hindi
subtitle: Multilingual Mathematical Reasoning - Advancing Open-Source LLMs in Hindi and English by Anand et. al.
tags: [llm, paper reading]
---

Arxiv link: [Multilingual Mathematical Reasoning: Advancing Open-Source LLMs in Hindi and English](https://arxiv.org/pdf/2412.18415)

## Outline and major points
* LLMs are good at linguistic tasks, less good at mathematical tasks. Even within math tasks, they struggle with complex math questions. LLMs are good in English, but less good at other languages like Hindi.
* This paper focuses on improving LLM performance on math tasks in Hindi, and also in bilingual settings.
* The paper's contributions:
    - **Decomposition strategy**: This paper focuses on improving LLM performance on math tasks in Hindi, and also in bilingual settings.
        - Break down multiplication and division problems into segments - hundreds, tens, ones - and then combine the results in an appropriate manner
        - Seems like chain-of-thought: trying to force the model to think in steps
    - **Structured Solution Generation**: A template which the model should return results in. The hypothesis is that forcing the model to adhere to this template will reduce hallucinations and compel the model to focus on the theory underlying the math problem
        - Feels like this is just prompt engineering
    - **Curriculum Learning**: An iterative way to fine-tune the model. First train and evaluate it on easy problems, then on easy+medium problems, etc.. The idea is that this mimics how people learn new mathematical concepts so it could help LLMs as well
        - This ties in with an interesting hypothesis that fine-tuning LLMs on a dataset that contains identical question-answer pairs in English and Hindi will improve the model’s performance on Hindi math problems. The idea is that the model can map its strengths in English, a language it is good in to Hindi, a language it is less good in, and form helpful associations

## The paper is not technically difficult but very hard to read

* Honestly a very difficult paper to read because of how it was formatted. The decision to titlecase the paper’s contributions every time in the paper - Decomposition Strategy, Structured Solution Creation,  etc - made the paper very hard to read. Italics or acronyms would have been so much better.

* Figures and tables are hard to interpret
    - I would have preferred if Tables 3 and 4 came into the narrative after table 2. In the current paper, there’s a lot of back and forth between 2,3, and 4 and because they are referencing different training datasets, models, and are on different pages, this back and forth gets tiring. I gave up after my second attempt reading the paper.
    - In the Results & Analysis section, they talk a lot about changes in performance. But it is not at all easy to follow that back to the tables and charts they are referencing. I think creating more focused tables and charts, even at the cost of some redundancy, would have helped tremendously. Or some charts that are solely focused on showing the performance improvements.

## My takeaways from this paper

* Curriculum Learning is an intuitive concept and the idea of bilingual training is an interesting way to improve LLM performance in non-English languages.
* A broader learning for me: Because I’m new to reading LLM papers, it took me a long time to understand the difference between few-shot examples vs instruction-tuning. But I now understand that instruction-tuning is when you fine-tune a model. And few-shot examples are when you just include a small number of examples in the prompt.
