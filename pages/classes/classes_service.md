---
title: Service
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_service.html
folder: classes
---

## Introduction

The service class is used for all towing and roadside assistance services between [Tow Truck Drivers](/classes_tow_truck_driver) and [Customers](/classes_customer).

To initiate, the customer creates a service and selects which properties he wishes to request (for example, `accident` or `flat_tire`) and then the Tow Truck Driver will view the request and reply, either accepting or declining.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|in|customer_vehicle||[Vehicle](/classes_vehicle)|
|has_one|in|tow_truck||[Vehicle](/classes_vehicle)|
|has_one|in|customer||[Customer](/classes_customer)|
|has_one|in|tow_truck_driver||[TowTruckDriver](/classes_tow_truck_driver)|
|has_one|out|initial_tow_truck_location||[Location](/classes_location)|
|has_one|out|pickup_location||[Location](/classes_location)|
|has_one|out|dropoff_address||[Address](/classes_address)|
|has_one|out|transaction||[Transaction](/classes_transaction)|
|has_many|in|trip_locations||[Location](/classes_location)|

## Properties

|Property|Type|
|+-+|
|number|Integer|
|start_date|Date|
|end_date|Date|
|status|Integer|
|customer_confirm|Boolean|
|vendor_confirm|Boolean|
|accident|Boolean|
|towing_service|Boolean|
|flat_tire|Boolean|
|locked_out|Boolean|
|battery_dead|Boolean|
|out_of_gas|Boolean|
|message|String|
|dropoff_trip|Boolean|
|cancelled|Boolean|

## Methods

### cancel

__Description__

The service `cancelled` property is set to true.

__Parameters__

None

__Return Type__

None

### cancelled?

__Description__

Evaluate if the service has been cancelled.

__Parameters__

None

__Return Type__

Boolean

### dropoff_trip?

__Description__

Evaluates if the service will include a towing trip that a vehicle will be dropped off to true. If it is just a roadside service without a towing this will evaluate to false.

__Parameters__

None

__Return Type__

Boolean

### service_type

__Description__

Returns a string articulating which service type is set.

__Parameters__

None

__Return Type__

String

### vendor_accept

__Description__

The service status is updated that the vendor has accepted the request.

__Parameters__

None

__Return Type__

None

### confirm_dropoff

__Description__

The service status is updated that the dropoff location has been confirmed.

__Parameters__

None

__Return Type__

None

### service_set_dropoff(address)

__Description__

The dropoff address for the service is assigned to be the address object that is passed through as a parameter.

__Parameters__

address - Address object

__Return Type__

None

### complete_service

__Description__

The service status is updated and the trip's end-time is set.

__Parameters__

None

__Return Type__

None

### set_dropoff_trip(value)

__Description__

Determines the value as to if the service will include a towing to a dropoff location, or if it will not. If it will include a dropoff trip then the service proceeds, otherwise a transaction is initialized and the service is complete.

__Parameters__

None

__Return Type__

None

### initialize_transaction

__Description__

Creates a new [Transaction](/classes_transaction) object for the service and associates it to the service.

__Parameters__

None

__Return Type__

Transaction

### log_location(latitude, longitude)

__Description__

Accepts a latitude and longitude value for a new location. Evaluates if this latitude and longitude are new for this trip, otherwise it does not log duplicate locations.

__Parameters__

location - Location object

__Return Type__

None

### customer_status_message(customer_name, vendor_name)

__Description__

Returns a the status message from the `CUSTOMER_STATUS_MESSAGES` class constant with the names of both the customer and tow truck driver formatted into it. For example: "Randy is on his way to come pick you up".

__Parameters__

None

__Return Type__

String

### tow_truck_driver_status_message(customer_name, vendor_name)

__Description__

Returns a the status message from the `VENDOR_STATUS_MESSAGES` class constant with the names of both the customer and tow truck driver formatted into it. For example: "Drop off Randy's vehicle".

__Parameters__

None

__Return Type__

String

### status_message

__Description__

Returns the appropriate status message from the `STATUS_MESSAGES` class constant.

__Parameters__

None

__Return Type__

String

### service_options

__Description__

Returns an array of all the options of requested products for the service.

__Parameters__

None

__Return Type__

Array

### service_state

__Description__

Returns in a string format the state of the service, options are 'Cancelled', 'Active', 'Requested', 'Complete'

__Parameters__

None

__Return Type__

String

### status_step_forward

__Description__

Increases the value of the `status` property by 1, to set the trip forwards one step.

__Parameters__

None

__Return Type__

None

### status_step_backward

__Description__

Decreases the value of the `status` property by 1, to set the trip backward one step.

__Parameters__

None

__Return Type__

None

### message?

__Description__

Evaluates if the service trip was ordered with a message included with it.

__Parameters__

None

__Return Type__

Boolean

### tow_truck_average_speeds

__Description__

Returns a nested array with the values of how fast a tow truck driver was estimated to be travelling at any given time. It follows a series of timestamps that are calculated by the distance travelled in the time interval of location objects being sent to the server.

For example, the array would be returned in the format of [[time, speed],[time, speed],[time, speed]].

__Parameters__

None

__Return Type__

Array

### start_time

__Parameters__

None

__Return Type__

DateTime

__Description__

Returns the time that the service started.

### end_time

__Description__

Returns the time that the service has completed.

__Parameters__

None

__Return Type__

DateTime

### start_end_times_formatted

__Description__

Returns a formatted string of the start and end times of the service.

__Parameters__

None

__Return Type__

String

### time_duration

__Description__

Returns the time duration of the service.

__Parameters__

None

__Return Type__

DateTime

### time_duration_formatted

__Description__

Return a string with the full formatted duration of the service from start to completion. If the service is not yet complete, then it defaults to the current time as the end time.

__Parameters__

None

__Return Type__

String

### complete?

__Description__

Evaluate if a service is complete.

__Parameters__

None

__Return Type__

Boolean

### active?

__Description__

Evaluate if a service is active.

__Parameters__

None

__Return Type__

Boolean

### request?

__Description__

Evaluate if the service is currently in that state where it is only a request, and not yet been accepted and become active.

__Parameters__

None

__Return Type__

Boolean

## Class Methods

### active_services

__Description__

Return an array of all service objects that are currently active.

__Parameters__

None

__Return Type__

Array

### active_services?

__Description__

Evaluate if any services are currently active.

__Parameters__

None

__Return Type__

Boolean

### complete_services

__Description__

Return an array of all complete services.

__Parameters__

None

__Return Type__

Array

### complete_services?

__Description__

Evaluate if complete services exist.

__Parameters__

None

__Return Type__

Boolean

### setup_new_service(service_params,tow_truck_driver_id,customer_id,customer_vehicle_id)

__Description__

Setup a new service and set its properties from paramters and connect the associations.

__Parameters__

service_params - Parameters
tow_truck_driver_id - String
customer_id - String
customer_vehicle_id - String

__Return Type__

Service object
