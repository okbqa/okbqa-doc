---
layout: doc
title: Control Module
version: 2
prev_version: /control-module/v1/
permalink: /control-module/v2/
---

A control module (CM) is a module that links all of the I/Os of OKBQA modules and constructs and realizes an OKBQA pipeline to be work. A controller has a role of a pipeline constructor as well as a debugger for validating the result of a pipeline. CM works as follows: Initially, CM takes a question and language of that question as an input, and then executes an initial module on a pipeline, typically template generation module. Then, CM sequentially executes next modules of an initial module, typically, disambiguation module, query generation module, answer generation module, by transferring the output of a previous module into the input of a right next module. As a pipeline is executed, log messages are written, which are about I/Os, execution time, exceptional messages, and so on of each module. After a final result, typically answers of an input question, is obtained, CM returns the final answers and log messages that record the history of a pipeline execution.

## Main changes: 
- A configurable sequence of module execution
- A configurable time limitation of executing each module
- Enhanced contents of log messages
- Also refer to http://4.okbqa.org/development/documentation/controller

## I/O specification:
# Input

```JSON
{
    "input": {
        "string": "Which rivers flow through Seoul?",
        "language": "en"
    },
    "conf": {
        "address": {
            "TGM": ["TGM-ADD-1", "TGM-ADD-1", ..., "TGM-ADD-a"],
            "DM": ["DM-ADD-1", "DM-ADD-2", ..., "DM-ADD-b"],
            "QGM": ["QGM-ADD-1", "QGM-ADD-2", ..., "QGM-ADD-c"],
            "AGM": ["AGM-ADD-1", "AGM-ADD-2", ..., "AGM-ADD-d"],
            "KB": [["KB-ADD-1", "GURI-1"], ["KB-ADD-2", "GURI-2"], ..., ["KB-ADD-e", "GURI-e"]]
        },
        "sequence": ["QGM", "DM", "QGM", "AGM"],
        "timelimit": 10000    
    }
}
```
* ADD: address
* TGM: template generation module
* DM: disambiguation module
* QGM: query generation module
* AGM: answer generation module
* KB: knowledge base
* GURI: graph URI

# Output

```JSON
{
    "log": ["L-1", "L-2", ..., "L-f"],
    "result": [
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