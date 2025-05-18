---
layout: post
title: Using LLMs for cold-start in content recommender systems
subtitle: Predicting Movie Hits Before They Happen with LLMs by Agah et. al.
tags: [llm, paper reading, recommender systems]
---

Arxiv link: [Predicting Movie Hits Before They Happen with LLMs](https://arxiv.org/pdf/2505.02693)

TL;DR - They use LLMs to take in metadata about recently-released movies and get it to predict their popularity.

I wanted to read this paper because it's attempting to use LLMs in an industry context which is infinitely more interesting for me than pure theory, and because it concerns recommender systems which I have some background in.

## Outline and major points
1. Dataset Creation
    - They work for Comcast so they have data about their viewer’s behaviors
    - Metadata used: genre, title, actors, plot,etc..
    - The label was a boolean flag indicating whether this movie became popular over not. Popularity was defined by hitting certain thresholds of views in certain time windows. Eg: One potential definition of popularity was “did this movie get 1M views within the first 2 weeks of release”
2. Using LLMs to predict popularity
    - They asked the LLM to rank the given movies based on how popular it thinks they will be based on the movie’s metadata
    - This ranking would be compared against other rankings
3. Other ranking approaches that were used as baselines
    - Random ranking
    - “Popular Embedding” - passing each movie’s metadata through an embedding model, and doing cosine similarity against the average embedding of the top-100 popular movies in the weeks leading up to the release
4. Metrics
    - Accuracy@1: did the most popular movie show up in the ranking’s first position
    - Reciprocal rank: the reciprocal rank of the position of the most popular item. Lower = better because that means the ground truth most popular item was placed higher up in the list
    - NDCG@3
    - Recall@3
5. Results
    - They experimented with passing in varying amounts of movie metadata in the prompt
    - More info in prompt is generally better, but bigger models can better handle larger prompts
    - The LLM-based approach outperforms both their baselines

## Thoughts:
- I wonder if their baselines are strong enough? The random is intuitive and a good floor. The Popular Embedding approach also makes intuitive sense but I wonder if averaging out a 100 embeddings flattens it out too much and loses a lot of information about the individual popular movies? I dont have alternatives though
- I imagine the reason they used LLMs instead of training a classification model is because they want this system to be a tool that human editorial teams can use. I can see the generated explanations being useful there. Otherwise, I’m not sure the extra toil with prompt engineering, plus relying on LLMs to generate popularity scores is worth it