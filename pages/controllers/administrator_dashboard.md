---
title: Administrator Dashboard Controller
last_updated: July 2019
sidebar: primary_sidebar
permalink: controllers_administrator_dashboard.html
folder: controllers
---

## Introduction

The administrator dashboard governs the views where an __Administrator__ is signed in and operates in the application.

It is not accessible to any other type of actor.

## Methods

### home

__GET__

The main dashboard view of the administrator. He can see stats at a glance, and any pending tasks for him to address.

### tow_truck_drivers

__GET__

Lists all of the Tow Truck Drivers

### tow_truck_driver_view

__GET__

The "profile" page of a given tow truck driver. All details about their services and history can be found here.

### customers

__GET__

Lists all of the Customers

### customer_view

__GET__

The "profile" page of a given customer. All details about their services and history can be found here.

### services

__GET__

View all services.

### service_view

__GET__

View details of a particular service.

### tasks

__GET__

View all pending tasks and the specific link to address the item.

### analytics

__GET__

View graphs and statistics.

### settings

__GET__

Nothing here yet.

### insurance_companies

__GET__

View all insurance companies.

### insurance_company

__GET__

View a specific insurance company.

### new_insurance_company

__GET__

Create a new insurance company.

### body_shops

__GET__

View all body shops.

### map_manager

__GET__

This is where the administrator has a tool to point and click on a map and create tow trucks on it.

### broadcast_status_false

__POST__

This method is used to remove a role from the map_manager.

### new_role

__POST__

This method id used to add a role to the map manager.