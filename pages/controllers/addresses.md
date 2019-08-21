---
title: Addresses Controller
last_updated: July 2019
sidebar: primary_sidebar
permalink: controllers_addresses.html
folder: controllers
---

## Introduction

The "Address" being worked with here is generally the default dropoff address, which is connected to a Location object. Addresses can be be also attacheed to ContactInfo, which is done during the onboarding process of creating a new fleet.

## Methods

### index

__GET__

### show

__GET__

### new

__GET__

### edit

__GET__

### new_dropoff_location

__GET__

This is the page that is accessible through a VehicleOperator's preferences menu. User enters in details about where they want to set their address to with 3 fields of text (business name, street address, city) and a Javascript Google Geocode service will find the best fit.

### create_dropoff_location

__POST__

The create method for a default dropoff address. Takes the input of parameters from the __new_dropoff_location__ method and then creates an Address and Location object to attach to the corresponding VehicleOperator role of the Actor signed in.

If a params[:dashboard] == "fleet" is passed through, then the method knows that the dropoff location was set by a fleet manager and should be routed and redirected appropriately.

### set_dropoff_during_service

__POST__

This method is similar working to the __create_dropoff_location__, however it is invoked during a service as a component of a view. The user e

### create

__POST__

(Not used, see the above two methods)

### update

__PATCH/PUT__

### destroy

__DELETE__