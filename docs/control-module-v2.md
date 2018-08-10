---
layout: doc
title: Control Module
version: 2
prev_version: /control-module/v1/
permalink: /control-module/v2/
---

A control module is a module to link all of the QA modules to construct an OKBQA pipeline for answering a question, as well as a debugger for validating the result of each module and entire pipeline. 

The workflow of the controller is as follows:
* Initially, the controller takes a question and written language as an input, and then executes a first module specified in the "conf" field in an input (If it is not given in the "conf" field, a template generation module will be a first module). 
* Then, CM executes following modules sequentially (according to "sequence" field in an input) by transferring the parsed output of a previous module into the input of the following module. 
* During the pipeline is executed by the controller, log messages on module I/Os, execution times, exceptions, and so on are accumulated and returned to users to check whether a pipeline works well or not.
* After all of the modules are executed by the controller, it returns the final results (answers for a input question) and log messages recording the history of the execution.

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
            "TGM": ["TGM-ADD(1)", "TGM-ADD(2)", ..., "TGM-ADD(n1)"],
            "DM": ["DM-ADD(1)", "DM-ADD(2)", ..., "DM-ADD(n2)"],
            "QGM": ["QGM-ADD(1)", "QGM-ADD(2)", ..., "QGM-ADD(n3)"],
            "AGM": ["AGM-ADD(1)", "AGM-ADD(2)", ..., "AGM-ADD(n4)"],
            "KB": [["KB-ADD(1)", "GIRI(1)"], ["KB-ADD(2)", "GIRI(2)"], ..., ["KB-ADD(n5)", "GIRI(n5)"]]
        },
        "sequence": ["TGM", "DM", "QGM", "AGM"],
        "timelimit": 10000   
    }
}
```
* ADD: Address
* TGM: Template Generation Module
* DM: Disambiguation Module
* QGM: Query Generation Module
* AGM: Answer Generation Module
* KB: Knowledge Base
* GURI: Graph IRI
* timelimit: Upper time (seconds) limitation for executing each module

# Output

```JSON
{
    "log": ["L(1)", "L(2)", ..., "L(n1)"],
    "result": [
        {"query": "Q(1)", "answer": "A(1)"},
        {"query": "Q(2)", "answer": "A(2)"},
        ...
        {"query": "Q(n2)", "answer": "A(n2)"}
    ]
}
```
* L: Log message
* Q: SPARQL query
* A: RDF triples retrieved by a given query