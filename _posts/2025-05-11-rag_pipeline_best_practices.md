---
layout: post
title: Each step of a RAG pipeline has multiple implementation options
subtitle: Searching for Best Practices in Retrieval-Augmented Generation by Wang et. al.
tags: [llm, RAG, paper reading]
---

Arxiv link: [Searching for Best Practices in Retrieval-Augmented Generation](https://arxiv.org/pdf/2407.01219)

I wanted to read this paper to get a better idea of what a RAG pipeline looks like, given that I have not implemented one in my career plus it aligns with my current interests in information retrieval.

## Outline and major points
The RAG workflow has multiple steps, and each step gives the developer multiple implementation choices

1. Query classification: determining if the query even needs RAG or if the LLM already has enough information to handle the request
2. Chunking the documents: Chunking can be at different levels - token, sentence, semantic.
    1. Learned about two metrics that are normally used to evaluate the retrieval - Faithfulness and Relevancy. LlamaIndex has implementations for them.
3. Storing embeddings of chunks in a vector database
4. Retrieval
    1. Authors made an interesting point that the user-entered query is often not clear and not best suited for use as a base to do the retrieval off of.
    2. Hence, a possible step is query transformation - making the query more suited for RAQ
        1. Many possible approaches here as well - Getting an LLM to rewrite the query, create sub-questions from the OG query, and then retrieve documents for these sub-queries, HyDE (creating fake document that answers the query and then retrieve real documents most similar to the fake document)
    3. Rather than relying entirely on dense similarity, hybrid search is also an option - combining sparse retrieval and dense retrieval
5. Reranking the retrieved documents
    1. Even after you get the retrieved documents, you can add a reranking step on top of it
    2. Not sure what this adds compared to relying on the ranking produced by the retrieval mechanism, because I would assume that a good retrieval system would automatically give you the more relevant documents first
6. Document repacking
    1. Some other papers showed that performance can be impacted by where in the prompt the most relevant examples are provided. Eg: performance is usually best when the most relevant info is at the top or bottom of the prompt, and not the middle
7. Summarization
    1. The retrieved documents could have redundant information, or parts of them could be irrelevant to the query at hand. Before feeding into the prompt, one option is to summarize the information present in the retrieved documents.
8. Generator Fine-tuning
    1. The generator in a RAG pipeline is the LLM that takes in the augmented prompt and generates the final answer. The authors did experiments and found that fine-tuning the generator LLM with a mixture of relevant and irrelevant documents helps performance. The intuition behind this is that this teaches the generator how to better distinguish between relevant and irrelevant info making it more robust to imperfect retrieval.

## My takeaways from this paper

* I have not implemented a RAG pipeline yet so this was a good paper for me to learn about all the different steps involved. Some of them I knew already, such as retrieval, prompting, etc.. and some I hadn’t really thought about, such as document repacking and summarization.
* I am currently interested in information retrieval so the retrieval and reranking parts were the parts I found the most interesting.
* Lot of tweaking is possible when using RAG.
* My main goal with reading the paper was to learn the general contours of what a RAG pipeline looks like, so in that sense it was successful. Still, I appreciate that I have not had any practical experience yet.