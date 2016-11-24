---
layout: doc
title: Query Generation Module
version: 1
permalink: /query-generation-module/v1/
---

A query generation module is responsible for generating SPARQL queries based on the outputs of preceding two modules, a template generation and a disambiguation modules. 

## Input

Example query: How many students does the Free University in Amsterdam have?
one pseudo query (from the output of template generation)
one set of disambiguation (from the output of disambiguation)

```JSON
{
  "template":{
  "query": "SELECT ?v2 WHERE { ?v1 ?p1 ?v2 . }", 
  "slots":[
    {"s":"v1", "p":"a", "o":"owl:NamedIndividual"},
    {"s":"v1", "p":"verbalization", "o":"owl:NamedIndividual"},
    {"s" "var": "v1", "form": "Free University in Amsterdam", "annotation":  }, 
    {"var": "p1", "form": "students", "annotation": "owl:DatatypeProperty" } 
  ], 
  "score": 0.5
 },
 "disambiguation":{
   "score":0.3,
   "entities": [
     {
       "var": "v1", 
       "value": "http://dbpedia.org/resource/Free_University_of_Berlin",
       "type": "DBpedia:University",
       "score": 0.3
     }
   ],
   "properties": [
     {
       "var": "p1",
       "value": "http://dbpedia.org/property/students",
       "score": 0.7
     }
   ]
 }
}
```

## Output

list of SPARQL queries

```JSON
[
  {"query":"SELECT ...", "score":0.5},
  ...
]
```