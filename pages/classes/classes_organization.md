---
title: Organization
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_organization.html
folder: classes
---

## Introduction

The organization class is the top level class for different types of organizations within the SafeTow application, such as [BodyShops](/classes_body_shop), [Insurance Companies](/classes_insurance_company), [Vehicle Fleets](/classes_vehicle_fleet) and [Tow Truck Fleets](/classes_tow_truck_fleet).

\#TODO there is more methods to be built out for working with members.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* Neo4j::UndeclaredProperties
* [GraphQueries](/modules_graph_queries.html)
* [GenerateID](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_many|:in|:managers||[Manager](/classes_manager)|
|has_many|:out|:members||[Role](/classes_role)|
|has_many|:out|:services||[Service](/classes_service)|
|has_many|:out|:transactions||[Transaction](/classes_transaction)|
|has_many|:out|:default_dropoff_addresses||[Address](/classes_address)|
|has_one|:out|:contact_info||[ContactInfo](/classes_contact_info)|

## Properties

|Property|Type|
|+-+|
|:name|String|
|:acronym|String|
|:logo|String|
|:branch|String|
|:employee_number_range|String|

## Methods

### manager_count

__Parameters__

None

__Return value__

Integer

__Description__

Numeric value of how many managers are set for the organization.

### active_services

__Parameters__

None

__Return value__

Array of services

__Description__

This method finds all services that members of the organization are involved in that are currently in an active state, and returns them as an array.

### complete_services

__Parameters__

None

__Return value__

Array of services

__Description__

This method finds all services that members of the organization are involved in that are complete, and returns them as an array.

## Class Methods
