---
title: Customer
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_customer.html
folder: classes
---

## Inheritance

[Role](/classes_role) > [VehicleOperator](/classes_vehicle_operator) > Customer

## Introduction

The customer class covers the role of someone using the SafeTow application to order roadside assistance from a [TowTruckDriver](/classes_tow_truck_driver).

Customers can be independent of any organization, or belong to an [VehicleFleet](/classes_vehicle_fleet).

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:out|:safety_contact||[SafetyContact](/classes_safety_contact))|

## Properties

|Property|Type|
|+-+|
|:organization_confirmed|String|

## Methods

### vehicle_options_for_select

__Description__

This method returns an array of all vehicle options that a customer can select from when ordering a service. The list is returned in a readable format that involves license plate, makes, models, so that the customer can easily select which vehicle they need service for.

If the customer belongs to an organization where the vehicles are owned by the organization, then they are returned those vehicles in the array and can select them as well.

__Parameters__

None

__Return Type__

Array


## Class Methods

### active_customers

__Description__

Returns all customers who are currently active.

The state of being active is computed from the last time that they updated their location in the application. If a customer has been on the application with their location updated within the last 30 minutes, then they are determined to be active.

__Parameters__

None

__Return Type__

Array
