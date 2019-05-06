---
title: Email
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_email.html
folder: classes
---

## Introduction

The email class covers the properties of storing email addresses of a person. Email addresses are always associated to 'ContactInfo' objects which are in turn associated to all 'Persons'.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:in|:contact_info||[ContactInfo](/classes_contact_info)|

## Properties

|Property|Type|
|+-+|
|:sort_order|String|
|:description|String|
|:address|String|

## Methods

## Class Methods
