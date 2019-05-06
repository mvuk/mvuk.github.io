---
title: Product
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_product.html
folder: classes
---

## Introduction

Products are used by Tow Truck Drivers. Tow Truck Drivers list the 'products' which they would offer to customer, and they set the prices for them accordingly.

Since all tow truck drivers should be prompted to list prices for the same standard products, there are class constants that define the specific products.

During onboarding, a tow truck driver is given a list of the products that are unset, and prompted to set prices for them. When he does so, it creates new Product objects and sets it as an association to him.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:in|:tow_truck_driver||[TowTruckDriver](/classes_tow_truck_driver.html)|

## Properties

|Property|Type|
|+-+|
|:name|String|
|:description|String|
|:price|String|

## Methods

## Class Methods

### list_default_products

__Parameters__

None

__Return value__

Array, the DEFAULT_PRODUCTS

__Description__

Returns an array of strings, which are the product names as set in the class constant `DEFAULT_PRODUCTS`.

For example, the method would return:
`["Towing service", "Flat tire", "Unlock vehicle", "Battery jumpstart", "Gas refill"]`
