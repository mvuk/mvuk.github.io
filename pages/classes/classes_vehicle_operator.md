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
|has_many|:out|:services||[Service](/classes_service)|
|has_many|:out|:transactions||[Transaction](/classes_transaction)|
|has_many|:out|:vehicles|[HasVehicle](/classes_has_vehicle)|[Vehicle](/classes_vehicle)|
|has_many|:out|:comments||[Comment](/classes_comment)|
|has_one|:out|:organization||[Organization](/classes_organization)|
|has_one|:out|:insurance_company|[HasInsuranceCompany](/classes_has_insurance_company)|[InsuranceCompany](/classes_insurance_company)|
|has_one|:out|:location||[Location](/classes_location)|
|has_one|:out|:default_dropoff_address||[Address](/classes_address)|

## Properties

|Property|Type|
|+-+|
|:organization_confirmed|Boolean|

## Methods

### confirm_organization

__Parameters__

None

__Return value__

None

__Description__

Updates the value of `organization_confirmed` to true.

### belongs_to_organization?

__Parameters__

None

__Return value__

Boolean

__Description__

Evaluates if the object belongs to an organization.

### insurance_company_rel

__Parameters__

None

__Return value__

Relationship

__Description__

Returns the [HasInsuranceCompany](/classes_has_insurance_company) relationship, so that its properties and methods are accessible.

### already_requested?(role_id)

__Parameters__

role_id - String

__Return value__

Boolean

__Description__

Evaluates if the vehicle operator already has a pending request with the role that is passed through.

### set_default_dropoff_address(address)

__Parameters__

address - Address object

__Return value__

None

__Description__

Associates the passed through address object into being the default dropoff address for the vehicle operator.

### primary_vehicle

__Parameters__

None

__Return value__

Vehicle object

__Description__

Returns the default active vehicle of the vehicle operator. If they only have one vehicle it is returned, if they have many the primary vehicle is returned.

### total_services

__Parameters__

None

__Return value__

Integer

__Description__

Return the total number of services the vehicle operator has taken part of.

### total_payment_amount

__Parameters__

None

__Return value__

Float

__Description__

Return the total number amount of payments spent or received by the vehicle operator.

### total_complete_services

__Parameters__

None

__Return value__

Integer

__Description__

Return the total number of completed services the vehicle operator has taken part of.

### complete_services

__Parameters__

None

__Return value__

Array of service objects

__Description__

Return an array of each service that the vehicle operator has completed.

### complete_services?

__Parameters__

None

__Return value__

Boolean

__Description__

Determine if the vehicle operator has performed any services to completion.

### active_services

__Parameters__

None

__Return value__

Array of service objects

__Description__

Return an array of each service that the vehicle operator is actively engaged in.

### active_services?

__Parameters__

None

__Return value__

Boolean

__Description__

Evaluates if the vehicle operator is engaged in any active services.

### complete_services

__Parameters__

None

__Return value__

Array of service objects

__Description__

Return an array of each service that the vehicle operator has completed.

### service_requests

__Parameters__

None

__Return value__

Array of service objects

__Description__

Return an array of each service that the vehicle operator is involved in a request for.

### service_requests?

__Parameters__

None

__Return value__

Boolean

__Description__

Evaluates if any services are in the request stage.

### set_active

__Parameters__

None

__Return value__

None

__Description__

Set the `active_status` of the role to be enabled

### set_inactive

__Parameters__

None

__Return value__

None

__Description__

Set the `active_status` of the role to be disabled

### has_comments?

__Parameters__

None

__Return value__

Boolean

__Description__

Evaluates if the vehicle operator has any comments written about them.

### determine_distance(vehicle_operator)

__Parameters__

vehicle_operator - VehicleOperator object

__Return value__

Float

__Description__

Uses the location objects associated with both of the 'self' and the new 'vehicle_operator' value that is passed through, and returns a value of a float that represents the number of kilometers between each party.

### log_location_active_service(location)

__Parameters__

location - Location object

__Return value__

Location

__Description__

When a vehicle is polling for location during a time that they are part of an active service, this method will then log the location object to the service.

## Class Methods
