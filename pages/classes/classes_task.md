---
title: Task
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_task.html
folder: classes
---

## Introduction

Tasks are used by administrators in their dashboards. When any administrator signs into their dashboard, they will see a list of tasks that are incomplete.

At this stage of development, they are used as assignments to specific roles that need to be worked on. An example situation where tasks is used is the onboarding of tow truck drivers.

Right now, class methods are used to return lists of target pages where incomplete work must be addressed by the administrator. In the next stage of development, this class will evolve into the creation of specific task nodes that are created with the outlined properties.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|out|role||[Role](/classes_role.html)|

## Properties

|Property|Type|
|+-+|
|description|String|
|complete|Boolean|

## Methods

## Class Methods

### verify_tow_truck_driver_documents

__Description__

This method looks up all tow truck drivers who have any documents that are unverified. It collects all of their unique identifiers and returns them as an array. The administrator receives formatted links in his dashboard that go to the specific tow truck driver profile page where he will verify the documents individually.

__Parameters__

None

__Return Type__

Array of IDs belonging to tow truck drivers who have unverified documents

### incomplete_tasks

__Description__

*(Not yet implemented)*

__Parameters__

None

__Return Type__

Returns all task objects that have not been marked as complete.
