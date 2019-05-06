---
title: SafetyContact
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_safety_contact.html
folder: classes
---

## Inheritance

[Person](/classes_person.html) > SafetyContact

## Introduction

The safety contact is set up for the purpose of a [Customer](/classes_customer) to send them a link to follow along the trip in real time in the application.

The safety contact is not a user, and exists just as a person with contact information as one single phone number.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:in|:customer||[Customer](/classes_customer)|

## Properties

## Methods

## Class Methods
