---
title: Manager
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_manager.html
folder: classes
---

## Inheritance

[Role](/classes_role) > Manager

## Introduction

The manager class is parent to all roles that are 'managers' to organizations.

This class contains the relationship to the organization to which it is a manager of as a 'has_one' relationship. If an actor was ever to become a manager of different organizations, he would have a unique 'role' generated for each.

This class also determines the access level to which the manager is granted over the organization. More extensibility to which permissions are allowed by active status will be elaborated on.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:out|:organization||[Organization](/classes_organization)|

## Properties

|Property|Type|
|+-+|
|:access_level|String|

## Methods

## Class Methods
