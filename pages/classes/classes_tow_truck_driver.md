---
title: TowTruckDriver
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_tow_truck_driver.html
folder: classes
---

## Inheritance

[Role](/classes_role) > [VehicleOperator](/classes_vehicle_operator) > TowTruckDriver

## Introduction

The customer class covers the role of someone using the SafeTow application to offer roadside assistance and towing services to [Customers](/classes_customer).

Tow Truck Drivers belong to their companies or organizations, called [TowTruckFleets](/classes_tow_truck_fleet).

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_many|out|products||[Product](/classes_product)|
|has_one|out|profile_picture||[Document](/classes_document)|
|has_one|out|drivers_license||[Document](/classes_document)|
|has_one|out|tow_truck_license||[Document](/classes_document)|

## Properties

|Property|Type|
|+-+|
|price_per_unit_distance|String|
|unit_distance|String|

## Class Methods

### active_tow_trucks

__Description__

Returns an array of all tow truck drivers who have an active status.

The state of being active is computed from the last time that they updated their location in the application. If a customer has been on the application with their location updated within the last 30 minutes, then they are determined to be active.

__Parameters__

None

__Return Type__

Array

### local_active_tow_trucks(user_id)

__Description__

This method finds all active tow trucks as in the `active_tow_trucks` method. Then, it finds the role associated with the actor that has the 'user_id' value that is passed through, and determines the 'search radius' defined in its 'preference'.

Each tow truck that is active is evaluated as to whether it is within the correct search radius, and then an array is returned for all tow trucks that satisfy the requirement.

This method can be used by users with either Customer or TowTruckDriver as their role, allowing anyone to see the location of other tow truck drivers in the system.

__Parameters__

user_id - String

__Return Type__

Array

### local_active_tow_trucks_green(user_id)

__Description__

Returns array of 'green' status tow trucks. This means that these tow trucks are available for service trips and are not currently engaged with any customers.

The 'user_id' is calculated like the `local_active_tow_trucks` method to ensure that the tow trucks are within an appropriate radius as set in preferences.

__Parameters__

user_id - String

__Return Type__

Array

### local_active_tow_trucks_red(user_id)

__Description__

Returns array of 'red' status tow trucks. This means that these tow trucks have just become engaged in other services and likely will not become available for an extended period of time.

The 'user_id' is calculated like the `local_active_tow_trucks` method to ensure that the tow trucks are within an appropriate radius as set in preferences.

__Parameters__

user_id - String

__Return Type__

Array

### local_active_tow_trucks_yellow(user_id)

__Description__

Returns array of 'yellow' status tow trucks. This means that these tow trucks are currently engaged in service trips but will become available soon.

The 'user_id' is calculated like the `local_active_tow_trucks` method to ensure that the tow trucks are within an appropriate radius as set in preferences.

__Parameters__

user_id - String

__Return Type__

Array

## Instance Methods

### average_rating

__Description__

Returns the average rating of the tow truck driver, formatted as `3.5/5`

__Parameters__

None

__Return Type__

String

### complete_documents

__Description__

Returns an array of all documents objects that have been uploaded.

__Parameters__

None

__Return Type__

Array

### current_day_transactions

__Description__

Returns array of transaction objects that have been complete on that day.

__Parameters__

None

__Return Type__

Array

### daily_billing_total_amount

__Description__

Returns the monetary value of the total revenue from services in that day.

__Parameters__

None

__Return Type__

Float

### daily_billing_total_quantity

__Description__

Returns the number of services complete in that given day for the driver.

__Parameters__

None

__Return Type__

Integer

### has_products?

__Description__

Evaluates if the tow truck driver has set any products.

__Parameters__

None

__Return Type__

Boolean

### incomplete_documents

__Description__

Returns an array of pending documents that need to be uploaded by the user.

__Parameters__

None

__Return Type__

Array

### price_per_unit_distance?

__Description__

Evaluates if the tow truck driver has set their `unit_distance` and `price_per_unit_distance` properties.

__Parameters__

None

__Return Type__

Boolean

### price_per_km

__Description__

Calculates the price per kilometer based on the `unit_distance` and `price_per_unit_distance` properties.

__Parameters__

None

__Return Type__

String

### price_per_mile

__Description__

Calculates the price per mile based on the `unit_distance` and `price_per_unit_distance` properties.

__Parameters__

None

__Return Type__

String

### profile_picture_path

__Description__

Looks up the value of the attached profile picture document that is stored in AWS S3 and returns the path to access it.

__Parameters__

None

__Return Type__

String

### onboarding_progress

__Description__

Returns string statement of how far the tow truck driver has progressed in the onboarding process.

__Parameters__

None

__Return Type__

String

### ratings_formatted

__Description__

Returns the ratings of a tow truck driver in a formatted string, for example `"4/5 (4 reviews)"`

__Parameters__

None

__Return Type__

String

### remove_if_inactive

__Description__

Evaluates if the tow truck driver has updated its location within the last 30 minutes. If it has not, then it is determined to be inactive and the `set_inactive` method is called.

__Parameters__

None

__Return Type__

None

### required_documents

__Description__

Returns an array of all documents that are required for upload.

__Parameters__

None

__Return Type__

Array

### set_products

__Description__

Returns array of products that have been set for this specific tow truck driver.

__Parameters__

None

__Return Type__

Array

### total_reviews

__Description__

Returns the total quantity of reviews.

__Parameters__

None

__Return Type__

Integer

### total_services

__Description__

Determine the total quantity of services that the tow truck driver has engaged in.

__Parameters__

None

__Return Type__

None

### unset_products

__Description__

Returns array of strings of product names for products that have not yet been set for this specific tow truck driver.

__Parameters__

None

__Return Type__

Array

### unverified_documents

__Description__

Returns an array of all documents that have not yet been verified.

__Parameters__

None

__Return Type__

Array

### uploaded_documents

__Description__

Returns an array of all documents that have been uploaded.

__Parameters__

None

__Return Type__

Array

### verified_documents

__Description__

Returns an array of all documents that have been verified.

__Parameters__

None

__Return Type__

Array
