---
layout: doc
title: Control Module
version: 1
permalink: /control-module/v1/
---

A control module (CM) is a module that links all of the I/Os of OKBQA modules and constructs and realizes an OKBQA pipeline to be work. A controller has a role of a pipeline constructor as well as a debugger for validating the result of a pipeline. CM works as follows: Initially, CM takes a question and language of that question as an input, and then executes an initial module on a pipeline, typically template generation module. Then, CM sequentially executes next modules of an initial module, typically, disambiguation module, query generation module, answer generation module, by transferring the output of a previous module into the input of a right next module. As a pipeline is executed, log messages are written, which are about I/Os, execution time, exceptional messages, and so on of each module. After a final result, typically answers of an input question, is obtained, CM returns the final answers and log messages that record the history of a pipeline execution.

## I/O specification:
# Input

```JSON
{
    "string": "Which rivers flow through Seoul?",
    "language": "en",
    "conf": {
        "tgm": ["TGM-ADD-1", "TGM-ADD-1", ..., "TGM-ADD-a"],
        "dm": ["DM-ADD-1", "DM-ADD-2", ..., "DM-ADD-b"],
        "qgm": ["QGM-ADD-1", "QGM-ADD-2", ..., "QGM-ADD-c"],
        "agm": ["AGM-ADD-1", "AGM-ADD-2", ..., "AGM-ADD-d"],
        "kb": ["KB-ADD-1", "KB-ADD-2", ..., "KB-ADD-e"]
    }
}
```
* ADD: address
* TGM: template generation module
* DM: disambiguation module
* QGM: query generation module
* AGM: answer generation module
* KB: knowledge base

# Output

```JSON
{
    "log": ["L-1", "L-2", ..., "L-f"],
    "answers": [
        {"query": "Q-1", "answer": "A-1"},
        {"query": "Q-2", "answer": "A-2"},
        ...
        {"query": "Q-g", "answer": "A-h"}
    ]
}
```
* L: log
* Q: query
* A: answer