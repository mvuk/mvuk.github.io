---
title: Analytic
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_analytic.html
folder: classes
---

## Introduction

The analytic class contains all of the methods for returning data in a readable, workable format for the process of analytics. It works well with the _chart.js_ library to give meaningful visual representations on dashboards.

## Modules

* Singleton

## Relationships

## Properties

## Methods

### group(class_name,property,ignore_false = true)

__Parameters__

class_name - String
property - String
ignore_false - Boolean

__Return value__

Nested array of values in pattern [["value", 0],["value",1]]

__Description__

The group method collects the numerical count of each property value in a specified property of a specified class.

The notation and format of the response is modeled specifically to be the input for a _chart.js_ visualization of data. Even when not using the chart.js extension, the format is a good standard for this type of data.

For example `Analytic.group("Actor","role_class_name")` could return the following value: `[["Customer", 2], ["VehicleFleetManager", 1], ["InsuranceCompanyManager", 1], ["Administrator", 1], ["TowTruckDriver", 2], ["Salesman", 1], ["BodyShopManager", 1], ["TowTruckFleetManager", 1]]`

The 'ignore_false' value determines if values of 'property' that are set to nil or false should be counted or omitted when returning the array.

### group_by_time_period(class_name,property,time_period)

__Parameters__

class_name - String
property - String
time_period - Boolean

__Return value__

Nested array of values in pattern [["value", 0],["value",1]]

__Description__

This method is similar to the `group` method, but with the added dimension of time involved. This format is essential when working with a line chart in a library such as _chart.js_ where the horizontal axis is representative of time.

For example, the following haml code would create a line chart where the count of actors created on any given day is the y axis, and the x axis being divided up day by day.

```ruby
= line_chart @analytics.group_by_time_period("Actor","created_at","day")
```

A sample output of this value could be `[["02 May 2019", 10],["03 May 2019", 4]]`.

### total_services

### active_services

### complete_services

### cancelled_services

### average_service_duration

### service_state_during_cancellation

### service_ordered_products

### average_transaction_amount

### transaction_payment_type

### transactions_with_rating

### transactions_average_rating

## Class Methods
