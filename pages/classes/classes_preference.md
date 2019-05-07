---
title: Preference
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_preference.html
folder: classes
---

## Introduction

Whenever a new [User](/classes_user.html) (or [Actor](/classes_actor.html), which inherits from User) is created, a new preference object is created and associated with it.

The preference contains all of the settings that a user can adjust that will change their experience within the SafeTow application.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)
* [GenerateID](/modules_generate_id.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|in|user||[User](/classes_user.html)|
|has_one|out|safety_contact||[SafetyContact](/classes_safety_contact.html)|

## Properties

|Property|Type|
|+-+|
|language|String|
|country|String|
|currency|String|
|flat_rate|Integer|
|refresh_rate|String|
|radius|String|

\#TODO, should radius be moved from preference to being a property of [VehicleOperator](/classes_vehicle_operator.html)?

## Class Methods

## Instance Methods
