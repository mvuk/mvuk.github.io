---
title: Comment
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_comment.html
folder: classes
---

## Introduction

Comments are left on transactions. Comments are the equivalent of _reviews_.

Comments are left with a rating between 1-5 and a text component.

At this time, there is the limitation that only customers are rating tow truck drivers. It is in development to have the reviews system work both ways.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)
* [GenerateID](/modules_generate_id.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|out|customer||[Customer](/classes_customer.html)|
|has_one|out|tow_truck_driver||[TowTruckDriver](/classes_tow_truck_driver.html)|
|has_one|in|transaction||[Transaction](/classes_transaction.html)|

## Properties

|Property|Type|
|+-+|
|rating|Integer|
|text|String|

## Methods

### rating_formatted

__Description__

Returns the rating formatted in a string out of 5. For example, the method would return '4/5' if the rating value was '4'

__Parameters__

None

__Return Type__

String

### associate_to_transaction(transaction_id)

__Description__

Associates the comment to a particular transaction, and also adds the associations for the customer and tow truck driver.

A limitation is that it does not distinguish the author at this time, and transactions are set to just have a single comment written about the tow truck driver.

__Parameters__

transaction_id - String

__Return Type__

Transaction object

## Class Methods
