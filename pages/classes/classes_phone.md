---
title: Phone
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_phone.html
folder: classes
---

## Introduction

At this time, the Phone class accepts phone numbers in the format of (333) 444-5555. It parses them to save 333 as the 'area code', and 4445555 as the 'number'.

Support for phone numbers that do not fall within the scope of North America will be added in the next version.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|in|contact_info||[ContactInfo](/classes_contact_info.html)|

## Properties

|Property|Type|
|+-+|
|sort_order|String|
|description|String|
|calling_code|String|
|area_code|String|
|number|String|
|extension|String|

## Class Methods

## Instance Methods

### formatted_number

__Description__


__Parameters__

None

__Return Type__

String, phone number in format of (333) 444-5555
