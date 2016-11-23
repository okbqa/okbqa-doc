---
layout: docs
title: Control Module
version: 1
prev_section: /answer-generation-module/v1/
permalink: /control-module/v1/
next_section: /evaluation-module/v1/
---

A control module takes an question, language, and addresses of modules as an input, and then transfers input and output of all modules (template generation modules, disambiguation modules, query generation modules, answer generation modules, and knowledge bases) sequentially, and then returns final answers of the input question. This module allows users to configure multiple addresses of each module by setting the "conf" field of the input. The progress (return values, errors, and so on) of each module will be notified by "log" field of the output.

## Input

```JSON
{
    "string": "Which rivers flow through Seoul?",
    "language": "en",
    "conf": {
        "tgm": ["tgm_address_1", "tgm_address_2", ..., "tgm_address_a"],
        "dm": ["dm_address_1", "dm_address_2", ..., "dm_address_b"],
        "qgm": ["qgm_address_1", "qgm_address_2", ..., "qgm_address_c"],
        "agm": ["agm_address_1", "agm_address_2", ..., "agm_address_d"],
        "kb": ["kb_address_1", "kb_address_2", ..., "kb_address_e"]
    }
}
```

## Output

```JSON
{
    "log": ["log_1", "log_2", ..., "log_f"],
    "answers": [
        {"query": "query_1", "answer": "answer_1"},
        {"query": "query_2", "answer": "answer_2"},
        ...
        {"query": "query_g", "answer": "answer_h"}
    ]
}
```