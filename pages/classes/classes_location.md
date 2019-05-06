---
title: Location
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_location.html
folder: classes
---

## Introduction

The location object is a latitude/longitude pair. While a service is running, the application polls for location services constantly.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|out|address||[Address](/classes_address.html)|

## Properties

|Property|Type|
|+-+|
|longitude|Float|
|latitude|Float|

## Methods

## Class Methods
