---
title: InsuranceCompany
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_insurance_company.html
folder: classes
---

## Inheritance

[Organization](/classes_organization) > InsuranceCompany

## Introduction

The insurance company class is managed by the [InsuranceCompanyManager](/classes_insurance_company_manager) in their respective dashboard.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* [GraphQueries](/modules_graph_queries.html)

## Relationships

## Properties

|Property|Type|
|+-+|
|countries_serviced|Array|

## Class Methods

### setup_insurance_companies

__Description__

Uses a class constant and application setting to create default insurance companies to be created and added into the database. This is important because when vehicle operators go to add in the insurance company they belong to, the object should already exist to them in an interface where they can select an object that already exists in the database.

__Parameters__

None

__Return Type__

None

## Instance Methods
