---
title: Actor
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_actor.html
folder: classes
---

## Inheritance

[Person](/classes_person.html) > [User](/classes_user.html) > Actor

## Introduction

The actor class inherits from both person and user. While Person addresses the physical characteristics of someone on the SafeTow platform and User addresses the characteristics of having an account, actor addresses the relationship between them and one of the many [roles](/classes_role) which allow them to take action on the service.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* Neo4j::UndeclaredProperties
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_many|:out|:roles|[HasRole](/classes_has_role)|[Role](/classes_role)|

## Properties

## Methods

### has_role?(specified_role = nil)

__Description__

If no parameter is passed (ex. `@actor.has_role?`), then this method evaluates if the actor has any roles.

If a parameter of a given class name is passed (ex. `@actor.has_role?(Customer)`) then the method will evaluate true or false based on if the actor has that given role.

__Parameters__

specified_role - The class name of a role, ex. "Customer" (optional)

__Return Type__

Boolean

### add_role(role_class)

__Description__

The method accepts in a class name as a parameter, creates a new object for that class and associates it to the actor.

__Parameters__

role_class - The class name of a role, ex. "Customer"

__Return Type__

Role object

### remove_role(role_class)

__Description__

The method evaluates if the actor has the role specified in the parameter, and then removes the association if it is present.

\#TODO set this to become an 'inactive' hasRole relationship instead

__Parameters__

role_class - The class name of a role, ex. "Customer"

__Return Type__

None

### attach_role(role_object)

__Description__

This method associates a selected role object to the actor.

__Parameters__

role_object - an instantiated object that descends from the Role class

__Return Type__

None

### role(role_class = nil)

__Description__

This method is called on the actor with the parameter of a given class to return the corresponding role object. For example, `@actor.role(Customer)` would return the _customer_ object that is associated to that particular actor.

If no parameter is passed through, then the role object associated with that actor is returned, either as an array of objects or single object.

This is useful because it is the role object that contains the methods and relationships to actions that involve a service.

__Parameters__

role_class - The class name of a role, ex. "Customer" (optional)

__Return Type__

Role object

### role_class_name

__Description__

The method returns the class name of the actor's role. For example `@actor.role_class_name` could return _'Customer'_ whenever `@actor.role(Customer)` also resolves to true.

__Parameters__

None

__Return Type__

String - the class name of the role corresponding to that actor. Array is returned when the actor has multiple roles.

### add_manager_role(organization_id, access_level = nil)

__Description__

If access_level is left blank, the value defaults to a default value.

__Parameters__

organization_id - String
access_level - String, see access_level property of [Manager](/classes_manager) (optional)

__Return Type__

Manager role object

### create_phone_number(phone_number)

__Description__

Creates a new Phone object and associates it to the ContactInfo object associated to the actor. If no ContactInfo exists yet, that object is created too.

__Parameters__

phone_number - String

__Return Type__

Phone object

### create_email_address(email_address)

__Description__

Creates a new Email object and associates it to the ContactInfo object associated to the actor. If no ContactInfo exists yet, that node is created too.

__Parameters__

email_address - String

__Return Type__

Email object

## Class Methods

### create_from_name(first_name,last_name)

__Description__

This class method is equivalent to running 'create' method except that it uses just the parameters of first name and last name to satisfy all of the requirements such as a login name, passphrase.

When this new account is created, it has these default values set for the login information. Actors who are created in this manner get specific landing pages where they are prompted to set their own usernames and passphrases which overwrite the defaults.

__Parameters__

first_name - String
last_name - String

__Return Type__

Actor object
