---
title: Person
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_person.html
folder: classes
---

## Introduction

The person class covers all the properties of a physical person. [User](/classes_user.html) and [Actor](/classes_actor.html) inherit from it.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:out|:contact_info||[ContactInfo](/classes_contact_info.html)|

## Properties

|Property|Type|
|+-+|
|:first_name|String|
|:last_name|String|
|:nick_name|String|
|:prefix|String|
|:suffix|String|
|:gender|String|
|:race|String|
|:religion|String|
|:martial_status|String|
|:date_of_birth|Date|
|:height|String|
|:weight|String|
|:eye_colour|String|
|:hair_colour|String|
|:description|String|

## Methods

### full_name_gender_dob

__Parameters__

None

__Return value__

String

__Description__

Generates a string based on full name, gender, date of birth

## Class Methods
