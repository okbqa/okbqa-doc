---
layout: docs
title: Evaluation Module
version: 1
prev_section: /control-module/v2/
permalink: /evaluation-module/v1/
---

Evaluation of QA systems typically involve having a set of pre-defined questions, example queries, and answers to the questions. The Question Answering over Linked Data (QALD) is an evaluation campaign on multilingual question answering over linked data. QALD-4 provides a set of biomedical questions drawn from DrugBank, SIDER and Diseaseome. We wanted to extend this evaluation to a broader set of questions of increasing complexity, and to consider the data from DBpedia, Bio2RDF and BioGateway. Towards this goal, we 

1. established a set of descriptors to characterize questions [document][spreadsheet]
1. created questions, queries, and answers over our KB.

At the moment, evaluation module uses NLP-1 dataset for the evaluation of the full module.

## Input

Input is a language tag with configuration containing the address of the module and the number of maximum answers.

```JSON
{
    "language": "en",
    "conf": {
        "tgm" : ["http://121.254.173.77:1555/templategeneration/templator"],
        "dm"  : ["http://121.254.173.77:2357/agdistis/run"],
        "qgm": ["http://121.254.173.77:38401/queries"], 
        "kb"   : ["http://dbpedia.org/sparql"], 
        "answer_num": "5"
    }
}
```

## Output

```JSON
Output includes accuracy of the full system applying it to the full NLP-1 dataset.
{
    "accuracy":0
}
```