---
title: Address
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_address.html
folder: classes
---

## Introduction

Address stores data about physical addresses.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)
* [GenerateID](/modules_generate_id.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:in|:contact_info||[ContactInfo](/classes_contact_info.html)|
|has_one|:out|:location||[Location](/classes_location.html)|
|has_many|:out|:service||[Service](/classes_service.html)|

## Properties

|Property|Type|
|+-+|
|:sort_order|String|
|:description|String|
|:street|String|
|:city|String|
|:nick_name|String|
|:state_prov|String|
|:country|String|
|:postal_code|String|
|:precinct|String|
|:ward|String|
|:region|String|
|:active|Boolean|

## Methods

### full_address

__Parameters__

None

__Return value__

String

__Description__

Returns the full formatted address.

### set_location(latitude, longitude)

__Parameters__

* latitude - string or float
* longitude - string or float

__Return value__

Location object

__Description__

A latitude and longitude set of parameters are passed through the method. A new [Location](/classes_location.html) object is created, and associated to the address.

## Class Methods
