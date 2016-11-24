---
layout: doc
title: OKBQA Framework Overview
version: 1
permalink: /overview/v1/
---

One of the initial goals of the OKBQA collaboration was to devise a preliminary instantiation of a generic architecture for question answering on Linked Data. In the following, we begin by presenting key requirements to the architecture. We then present the architecture itself and describe the functionality of each of its module. We include preliminary implementations and identify components that must still be implemented. Finally, we describe our approach to evaluate our system.

## Key requirements

The architecture was designed to be as generic as possible while remaining easy to understand, implement and use. 
Our first key requirement was to ensure that no programming language is imposed on the user. The motivation behind this requirement was simply that certain programming language as better suited for certain tasks. Given the variety of tasks that are required to achieve high-quality question answering, enforcing a programming language would have been prohibitive to the functionality and extensibility of the framework. We thus decided that all modules would be implemented as web services.
Our second requirement was to reuse existing standards as much as possible. We thus decided that all services are to generate and consume JSON objects according to the architectural design below.
Our third requirement was that of provenance tracking. We thus chose to add the ID of each service to its JSON output, making the contribution of each module easy to track throughout the QA process.

## Architecture

Several types of architecture can be envisaged for QA. We assumed the QA process to be a workflow in which a controller decides on the workflow to employ, stores metadata on the current workflow and is free to call component in the order it requires. Each component on the other hand assumes a particular type of JSON object as input and returns JSON as output. Depending on their implementation, components are free to access as many other components as required.
Overall, 8 modules were specified as integral parts of the QA process.

* Core modules
  * [Template Generation Module (TGM)]({{ site.baseurl }}/template-generation-module/v1/): A TGM is responsible for analyzing a question in natural language to produce so called pseudo queries which determine the skeleton of SPARQL queries to be produced.
  * [Disambiguation Module (DM)]({{ site.baseurl }}/disambiguation-module/v1/): A DM is responsible for finding the URIs of the components of pesudo queries.
  * [Query Generation Module (QGM)]({{ site.baseurl }}/query-generation-module/v1/): A QGM is responsible for producing the final SPARQL queries to be submitted to endpoints.
  * [Answer Generation Module (AGM)]({{ site.baseurl }}/answer-generation-module/v1/): A AGM is responsible for consulting SPARQL end-points to get the answers.
* System modules
  * [Control Module (CM)]({{ site.baseurl }}/control-module/v2/): The workflow of a QA process is defined by a control module. On excution, a control module takes in a question in natural language, connects the components in the workflow to produce the answer to the question.
  * [Evaluation Module (EM)]({{ site.baseurl }}/evaluation-module/v1/): An evaluation module execute runs a contol module over a benchmark data set, and reports the performance of the QA process against the gold answers encoded in the data set.
* U/I modules
  * Input Guide module (IGM): A IGM may interact with a user to help or control the input questions.
  * Rendering module (RM): A RM may render the raw answers, a list of URIs or literals, to make them easier to read.

The figure below illustrates the components of OKBQA Framework:
![Components of OKBQA Framework]({{site.baseurl}}/img/okbqa-components.png)
