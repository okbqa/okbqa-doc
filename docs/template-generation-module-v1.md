---
layout: docs
title: Template Generation Module
version: 1
prev_section: /overview/v1/
permalink: /template-generation-module/v1/
next_section: /disambiguation-module/v1/
---

A Template Generation module is supposed to take in a natural language query, and to produce what we call pseudo queries. A pseudo query determines the structure of a SPARQL query which may represent the input query. At this stage, query entities are extracted from the natural language query, and a SPARQL structure is constructed using them. While resolution of the entities to URIs will be performed by the following module, a Disambiguation module, construction of the scaffold of SPARQL query, and delivery of structurized information about the query entities are the responsibility of a Template Generation module.

## Input

An input to a TGM consists of a question (string) and a language tag (string):

```JSON
{ "string": " ", "language": " " }
```

## Output

Output is a list of pseudo queries together with slot descriptions. A pseudo query with corresponding slot descriptions is supposed to represent the input query. In a pseudo query, all the terms are represented as variables which we call slots. While the slots are to be replaced with corresponding terms by a following module, a disambiguator, providing information about the slots is a reponsibility of a template generation module. Optionally, a pesudo query with slot descriptions may be scored, for later use for disambiguation or answer evaluation.

```JSON
[
  {
    "query": "SELECT|ASK v1 WHERE {v1 ...}",
    "slots": [ { "s": "v1", "p": "...", "o": "..." } ],
    "score": 0.0
  }
]
```

## Example

```JSON
[
  {
    "query": "SELECT ?v4 WHERE { ?v4 ?v2 ?v6 ; ?v7 ?v3 . } ",
    "score": "1.0",
    "slots": [
      {
        "o": "rdf:Property",
        "p": "is",
        "s": "v2"
      },
      {
        "o": "flow",
        "p": "verbalization",
        "s": "v2"
      },
      {
        "o": "rdf:Resource|rdfs:Literal",
        "p": "is",
        "s": "v6"
      },
      {
        "o": "Seoul",
        "p": "verbalization",
        "s": "v6"
      },
      {
        "o": "<http://lodqa.org/vocabulary/sort_of>",
        "p": "is",
        "s": "v7"
      },
      {
        "o": "rdf:Class",
        "p": "is",
        "s": "v3"
      },
      {
        "o": "rivers",
        "p": "verbalization",
        "s": "v3"
      }
    ]
  }
]
```