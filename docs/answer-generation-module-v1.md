---
layout: docs
title: Answer Generation Module
version: 1
prev_section: /query-generation-module/v1/
permalink: /answer-generation-module/v1/
next_section: /control-module/v2/
---

An answer generation module takes knowledge base addresses as an input from query control module. This module checks every queries on every input knowledge bases, and then gets and returns the final answers of the question.

## Input

```JSON
{
    "queries": [
        {"query": "query_1"},
        {"query": "query_2"},
        ...
        {"query": "query_a"}
    ],
    "conf": {
         "kb": ["kb_address_1", "kb_address_2", ..., "kb_address_b"],
    }
}
```

## Output

```JSON
{
    "answers": [
        {"query": "query_1", "answer": "answer_1"},
        {"query": "query_2", "answer": "answer_2"},
        ...
        {"query": "query_a", "answer": "answer_c"}
    ]
}
```