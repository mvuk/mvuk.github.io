---
title: Vehicle
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_vehicle.html
folder: classes
---

## Introduction

The vehicle class is used for both tow trucks and customer vehicles. Vehicles are owned by [VehicleOperators](/classes_vehicle_operator). Information about vehicles is shared during a service, and customers select which specific vehicle that they own for each specific service. Vehicles can also be owned by organizations for use in fleets.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* Neo4j::UndeclaredProperties
* [GraphQueries](/modules_graph_queries.html)
* [GenerateID](/modules_generate_id.html)
* [DocumentOwner](/modules_document_owner.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|in|owner|[HasVehicle](/classes_has_vehicle)|[VehicleOperator](/classes_vehicle_operator)|
|has_one|out|service||[Service](/classes_service)|
|has_one|in|vehicle_photo||[Document](/classes_document)|
|has_one|in|license_plate_photo||[Document](/classes_document)|

## Properties

|Property|Type|
|+-+|
|description|String|
|serial_number|String|
|type|String|
|make|String|
|model|String|
|license_plate|String|
|color|String|
|year|Integer|
|fuel_type|String|
|vehicle_type|String|

## Methods

## Class Methods
