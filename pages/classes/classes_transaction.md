---
title: Transaction
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_transaction.html
folder: classes
---

## Introduction

A transaction is created for every complete service. It comes into play for the final component of the process of ordering a service. The transaction contains all of the information about the monetary transaction between the customer and the tow truck driver.

Reviews are also attached to the 'transaction', rather than the 'service'.

### Status Code System

There is a status code system that corresponds to which stage of the transaction it is in.

__0__ - The transaction has been created with a number value assigned, but no details of payment have been entered in yet.

__1__ - A payment amount, transaction type and description of services are submitted by the tow truck driver, but not yet confirmed by the customer.

__2__ - The customer has confirmed the details that have been submitted by the tow truck driver to be accurate.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)
* [GenerateID](/modules_generate_id.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|in|customer||[Customer](/classes_customer.html)|
|has_one|in|tow_truck_driver||[TowTruckDriver](/classes_tow_truck_driver.html)|
|has_one|in|service||[Service](/classes_service.html)|
|has_one|out|comment||[Comment](/classes_comment.html)|

## Properties

|Property|Type|
|+-+|
|number|Integer|
|description|String|
|payment_type|String|
|amount|Float|
|status|Integer|

## Methods

### submit_details

__Description__

This method is called when a tow truck driver enters in the details of the service for the transaction, where it will update the status code to 1.

__Parameters__

None

__Return Type__

None

### confirm

__Description__

This method is called when the customer confirms the details that are input by the tow truck driver. It updates the transaction status to 2 and the [service](/classes_service.html) status to 6.

__Parameters__

None

__Return Type__

None

### make_editable

__Description__

If a customer rejects the transaction details, this method returns the status code to 0, so that the details will become editable again.

__Parameters__

None

__Return Type__

None

### has_review?

__Description__

Evaluates if a review has been written yet for the transaction.

__Parameters__

None

__Return Type__

Boolean

## Class Methods

### generate_transaction_number

__Description__

Returns a number to be used for a new transaction. The system numerically counts up from 0. For example, transaction #1, #2, #3 ... and so on.

__Parameters__

None

__Return Type__

Integer
