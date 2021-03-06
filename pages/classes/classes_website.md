---
title: Website
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_website.html
folder: classes
---

## Introduction

The purpose of the websites class is to contain information about website URLs that pertain to contact info of persons and organizations. Storing the value of a website in its own class gives it extensibility beyond being a single property in the 'Contact Info' class.

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
|url|String|
|https|Boolean|
|www|Boolean|

## Class Methods

## Instance Methods

### full_address

__Description__

Returns the full web address in a formatted manner, taking into account properties such as `https` and `www`. For example, `https://www.example.com` would be returned if those values were true, and `http://example.com` would be returned if both were false.

__Parameters__

None

__Return Type__

String
