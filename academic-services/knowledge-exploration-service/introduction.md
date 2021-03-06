---
title: About Microsoft Academic Knowledge Exploration Service
description: Microsoft Academic Knowledge Exploration Service enables self-hosted interactive search of entities in the Microsoft Academic Graph
ms.topic: overview
ms.date: 10/17/2018
---
# About Microsoft Academic Knowledge Exploration Service

Microsoft Academic Knowledge Exploration Service (MAKES) enables users to host private instances of an interactive academic search API, powered by [Knowledge Exploration Service (KES) engines](/azure/cognitive-services/KES/gettingstarted). The engines are generated by the Microsoft Academic engineering team using entities in the [Microsoft Academic Graph](../graph/index.yml), and distributed by the MAKES distribution service.

## About Knowledge Exploration Service

Knowledge Exploration Service (KES) offers a fast and effective way to add interactive search and refinement to applications. With KES, you can build a compressed index from structured data, author a grammar that interprets natural language queries, and provide interactive query formulation with auto-completion suggestions.

KES is available as a completely stand-alone project. For details and documentation please see [this website](https://docs.microsoft.com/en-us/azure/cognitive-services/KES/overview).

For the sake of this document it’s important to understand that when a KES “engine” is referenced it refers to a combination of a [compressed binary index](https://docs.microsoft.com/en-us/azure/cognitive-services/KES/gettingstarted#build-a-compressed-binary-index) and a [compiled SRGS grammar](https://docs.microsoft.com/en-us/azure/cognitive-services/KES/gettingstarted#compile-the-grammar), which are required for KES to operate. 

Each engine's index conforms to a [specific schema](https://docs.microsoft.com/en-us/azure/cognitive-services/KES/schemaformat), which defines what attributes are available and the operations that can be used to query them.

## Semantic interpretation engine

> [!IMPORTANT]
> Use the semantic interpretation engine if you plan to use the "interpret" API method

This engine is optimized for interpreting and offering suggestions for academic-oriented natural language queries. A working example of this can be seen on the [Microsoft Academic website](https://academic.microsoft.com/), which uses the interpret API to generate semantic completions (suggestions):

   ![Microsoft Academic query formulation using interpret](media/microsoft-academic-query-formulation.png "Microsoft Academic query formulation using interpret")

To optimize for this scenario the engine only focuses on indexing the lexical attributes for each academic paper entity in the MAG, including:

* Title
* Individual title words
* Publication year
* Full names of each author and their affiliations if available
* Venue information (journal/conference name)
* Field of study names

The engine also includes name synonyms (when available) and allows for prefix completions (i.e. suggestions). It notably **does not index entity IDs** and is generally used in tangent with the [Entity engine](reference-entity-engine.md) for executing the expressions corresponding to query interpretations.

## Entity engine

> [!IMPORTANT]
> Use the entity engine if you plan to use the "evaluate" or "histogram"/"calchistogram" API methods

This engine is optimized for the lookup and retrieval of all types of academic entities using a wide range of their available attributes.

Search results, filters and entity cards on [Microsoft Academic](https://academic.microsoft.com/) are a working example of the entity engine, using a combination of evaluate and histogram methods and semantic interpretations from the [semantic interpretation engine](reference-semantic-interpretation-engine.md):

   ![Microsoft Academic search results mapped to KES methods](media/microsoft-academic-search-results.png "Microsoft Academic search results mapped to KES methods")