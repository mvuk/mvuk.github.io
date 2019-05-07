---
title: VehicleOperator
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_vehicle_operator.html
folder: classes
---

## Inheritance

[Role](/classes_role) > VehicleOperator

## Introduction

The VehicleOperator class is used as the parent role to both [Customer](/classes_customer.html) and [TowTruckDriver](/classes_tow_truck_driver.html). It contains all of the relationships, properties and methods that these two classes share.

The VehicleOperator class also makes use of the VehicleOperators Controller, which both the Customer controller and the Tow Truck Driver controller inherit from.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* Neo4j::UndeclaredProperties

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_many|out|services||[Service](/classes_service)|
|has_many|out|transactions||[Transaction](/classes_transaction)|
|has_many|out|vehicles|[HasVehicle](/classes_has_vehicle)|[Vehicle](/classes_vehicle)|
|has_many|out|comments||[Comment](/classes_comment)|
|has_one|out|organization||[Organization](/classes_organization)|
|has_one|out|insurance_company|[HasInsuranceCompany](/classes_has_insurance_company)|[InsuranceCompany](/classes_insurance_company)|
|has_one|out|location||[Location](/classes_location)|
|has_one|out|default_dropoff_address||[Address](/classes_address)|

## Properties

|Property|Type|
|+-+|
|organization_confirmed|Boolean|

## Class Methods

## Methods

### active_services

__Description__

Return an array of each service that the vehicle operator is actively engaged in.

__Parameters__

None

__Return Type__

Array of service objects

### active_services?

__Description__

Evaluates if the vehicle operator is engaged in any active services.

__Parameters__

None

__Return Type__

Boolean

### already_requested?(role_id)

__Description__

Evaluates if the vehicle operator already has a pending request with the role that is passed through.

__Parameters__

role_id - String

__Return Type__

Boolean

### belongs_to_organization?

__Description__

Evaluates if the object belongs to an organization.

__Parameters__

None

__Return Type__

Boolean

### confirm_organization

__Description__

Updates the value of `organization_confirmed` to true.

__Parameters__

None

__Return Type__

None

### complete_services

__Description__

Return an array of each service that the vehicle operator has completed.

__Parameters__

None

__Return Type__

Array of service objects

### complete_services?

__Description__

Determine if the vehicle operator has performed any services to completion.

__Parameters__

None

__Return Type__

Boolean

### determine_distance(vehicle_operator)

__Description__

Uses the location objects associated with both of the 'self' and the new 'vehicle_operator' value that is passed through, and returns a value of a float that represents the number of kilometers between each party.

__Parameters__

vehicle_operator - VehicleOperator object

__Return Type__

Float

### has_comments?

__Description__

Evaluates if the vehicle operator has any comments written about them.

__Parameters__

None

__Return Type__

Boolean

### insurance_company_rel

__Description__

Returns the [HasInsuranceCompany](/classes_has_insurance_company) relationship, so that its properties and methods are accessible.

__Parameters__

None

__Return Type__

Relationship

### log_location_active_service(location)

__Description__

When a vehicle is polling for location during a time that they are part of an active service, this method will then log the location object to the service.

__Parameters__

location - Location object

__Return Type__

Location

### primary_vehicle

__Description__

Returns the default active vehicle of the vehicle operator. If they only have one vehicle it is returned, if they have many the primary vehicle is returned.

__Parameters__

None

__Return Type__

Vehicle object


### service_requests

__Description__

Return an array of each service that the vehicle operator is involved in a request for.

__Parameters__

None

__Return Type__

Array of service objects

### service_requests?

__Description__

Evaluates if any services are in the request stage.

__Parameters__

None

__Return Type__

Boolean


### set_active

__Description__

Set the `active_status` of the role to be enabled

__Parameters__

None

__Return Type__

None

### set_default_dropoff_address(address)

__Description__

Associates the passed through address object into being the default dropoff address for the vehicle operator.

__Parameters__

address - Address object

__Return Type__

None

### set_inactive

__Description__

Set the `active_status` of the role to be disabled

__Parameters__

None

__Return Type__

None

### total_complete_services

__Description__

Return the total number of completed services the vehicle operator has taken part of.

__Parameters__

None

__Return Type__

Integer

### total_payment_amount

__Description__

Return the total number amount of payments spent or received by the vehicle operator.

__Parameters__

None

__Return Type__

Float

### total_services

__Description__

Return the total number of services the vehicle operator has taken part of.

__Parameters__

None

__Return Type__

Integer
