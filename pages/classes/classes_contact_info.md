---
title: ContactInfo
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_contact_info.html
folder: classes
---

## Introduction

The ContactInfo class stores all of the contact information. It bridges actors and organizations to the actual units of phone numbers, email addresses, etc.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)
* [GenerateID](/modules_generate_id)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:in|:actor||[Actor](/classes_actor.html)|
|has_one|:in|:organization||[Organization](/classes_organization.html)|
|has_many|:out|:addresses||[Address](/classes_address.html)|
|has_many|:out|:phones||[Phone](/classes_phone.html)|
|has_many|:out|:emails||[Email](/classes_email.html)|
|has_many|:out|:websites||[Website](/classes_website.html)|

## Properties

## Methods

### email_address

__Parameters__

None

__Return value__

String or Array

__Description__

If there is one email address, it will return the formatted email address as a string. If there are multiple email addresses, it will return an array of properly formatted email addresses.

### phone_number

__Parameters__

None

__Return value__

String or Array

__Description__

If there is one phone number, it will return the formatted phone number as a string. If there are multiple phone numbers, it will return an array of properly formatted phone numbers.

### address

__Parameters__

None

__Return value__

String or Array

__Description__

If there is one address, it will return the formatted physical address as a string. If there are multiple addresses, it will return an array of properly formatted addresses.

### website

__Parameters__

None

__Return value__

String or Array

__Description__

If there is one website, it will return the formatted website URL as a string. If there are multiple websites, it will return an array of properly formatted website URLs.


## Class Methods
