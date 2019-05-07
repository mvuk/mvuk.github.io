---
title: DemoData
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_demo_data.html
folder: classes
---

## Introduction

The Demo Data class fills in any data for the purpose of filling in content for non-production versions of the application. For example, in development, testing and staging environments the methods in this class will construct some default [actors](/classes_actor) with [roles](/classes_role) that can be used.

## Modules

* Singleton

## Relationships

## Properties

## Class Methods

## Instance Methods

### default_actor_contact_info

__Description__

Creates a default [phone number](/classes_phone) and [email address](/classes_email) attached to a [ContactInfo](/classes_contact_info) object, which can be attached to an [actor](/classes_actor).

__Parameters__

None

__Return Type__

ContactInfo object

### default_organization_contact_info

__Description__

Creates a default [phone number](/classes_phone) and [email address](/classes_email) attached to a [ContactInfo](/classes_contact_info) object, which can be attached to any other [organizations](/classes_organization).

__Parameters__

None

__Return Type__

ContactInfo object

### manage_default_administrator

__Description__

Creates a new actor and assigns it the role of [administrator](/classes_administrator).

__Parameters__

None

__Return Type__

Administrator object

### manage_default_body_shop_fleet_manager

__Description__

Creates a new actor and assigns it the role of [body shop manager](/classes_body_shop_manager), and creates a [body shop](/classes_body_shop) which it manages.

__Parameters__

None

__Return Type__

BodyShopManager object

### manage_default_customer

__Description__

Creates a new actor and assigns it the role of [customer](/classes_customer), along with their [vehicle](/classes_vehicle).

__Parameters__

None

__Return Type__

Customer object

### manage_default_insurance_company_manager

__Description__

Creates a new actor and assigns it the role of [insurance company manager](/classes_insurance_company_manager), and creates an [insurance company](/classes_insurance_company) which it manages.

__Parameters__

None

__Return Type__

InsuranceCompany object

### manage_default_roles

__Description__

Calls other methods in the class to evaluate for the presence of roles and creates ones that are not set up.

Uses the class constant: `DEFAULT_ROLES = [Administrator, Salesman, TowTruckDriver, Customer, VehicleFleetManager, TowTruckFleetManager, BodyShopManager, InsuranceCompanyManager]`

__Parameters__

None

__Return Type__

None

### manage_default_salesman

__Description__

Creates a new actor and assigns it the role of [salesman](/classes_salesman).

__Parameters__

None

__Return Type__

Salesman object

### manage_default_tow_truck_driver

__Description__

Creates a new actor and assigns it the role of [tow truck driver](/classes_tow_truck_driver), along side their [vehicle](/classes_vehicle) and [tow truck fleet](/classes_tow_truck_fleet).

__Parameters__

None

__Return Type__

TowTruckDriver object

### manage_default_tow_truck_fleet_manager

__Description__

Creates a new actor and assigns it the role of [tow truck fleet manager](/classes_tow_truck_fleet_manager), and creates a [tow truck fleet](/classes_tow_truck_fleet) which it manages.

__Parameters__

None

__Return Type__

TowTruckFleetManager object

### manage_default_vehicle_fleet_manager

__Description__

Creates a new actor and assigns it the role of [vehicle fleet manager](/classes_vehicle_fleet_manager), and creates a [vehicle fleet](/classes_vehicle_fleet) which it manages.

__Parameters__

None

__Return Type__

VehicleFleetManager object
