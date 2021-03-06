---
title: Document
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_document.html
folder: classes
---

## Introduction

This class is used for all documents uploaded by roles within SafeTow. For example, a Tow Truck Driver needs to upload copies of his driver's license, tow truck license, and a photo of himself.

This class makes use of the Paperclip gem which works with file uploads. File attachments are uploaded directly to a specified AWS S3 bucket.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* Neo4j::UndeclaredProperties
* Neo4jrb::Paperclip
* ActionView::Helpers::NumberHelper
* [GraphQueries](/modules_graph_queries.html)
* [GenerateID](/modules_generate_id.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|in|document_owner||[Vehicle](/classes_vehicle.html),[Customer](/classes_customer.html),[TowTruckDriver](/classes_tow_truck_driver)|

## Properties

|Property|Type|
|+-+|
|name|String|
|description|String|
|document_type|String|
|verification_status|Boolean|
|attachment|["image/jpg", "image/jpeg", "image/png", "image/gif"]|

## Class Methods

## Instance Methods

### attachment_path

__Description__

Returns a url path to a direct link to that document's attachment.

__Parameters__

None

__Return Type__

String

### document_type_formatted

__Description__

Returns the document type in readable format, such as "Profile Picture" or "Driver's License"

__Parameters__

None

__Return Type__

String

### unverify

__Description__

Sets document verified property to false

__Parameters__

None

__Return Type__

None

### url_path

__Description__

Returns a url path to a direct link to that document, for example, "/documents/:id"

__Parameters__

None

__Return Type__

String

### verified?

__Description__

Determine whether the document is verified, return true/false.

__Parameters__

None

__Return Type__

Boolean

### verify

__Description__

Sets document verified property to true

__Parameters__

None

__Return Type__

None
