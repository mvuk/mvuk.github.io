---
title: User
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_user.html
folder: classes
---

## Inheritance

[Person](/classes_person.html) > User

## Introduction

While the Person class addresses the physical characteristics of a person, the User class addresses the login information and access to the application. Login names and passphrases are worked with in this class.

## Modules

* Neo4j::ActiveNode
* Neo4j::Timestamps
* Bcrypt
* [GraphQueries](/modules_graph_queries.html)

## Relationships

|Relationship|Direction|Name|RelClass|Target Class|
|+-+|
|has_one|:out|:preference||[Preference](/classes_preference)|

## Properties

|Property|Type|
|+-+|
|:login_name|String|
|:unique_login_name|String|
|:passphrase_hash|String|
|:alias|String|
|:group|String|
|:status|String|
|:data_access_level|String|
|:question|String|
|:answer|String|
|:hint|String|
|:verification_code|String|
|:verified|String|
|:passphrase_recovery_code|String|

## Methods

### update_passphrase(new_passphrase)

__Parameters__

new_passphrase - String

__Return value__

None

__Description__

This method accepts a string as a new passphrase and then runs the `@user.create_encrypted_passphrase` method to create a Bcrypt based passphrase. Then, it updates its own passphrase property with this value.

### create_encrypted_passphrase(passphrase)

__Parameters__

passphrase - String

__Return value__

String

__Description__

This method accepts a passphrase as a string, and encrypts it with the `Bcrypt::Password.create` method.

### encrypt_passphrase(passphrase)

__Parameters__

passphrase - String

__Return value__

String

__Description__

This method accepts a passphrase as a string, and encrypts it with the `Bcrypt::Password.new` method.

### passphrase_authorized?(params)

__Parameters__

params - Hash of values used at the time of object creation for a User class

__Return value__

Boolean

__Description__

This method evaluates if the parameters passed through params (which will include a login_name and passphrase) matches the correct passphrase for the user object. If they match, the method will evaluate to true.

### generate_passphrase_recovery_code

__Parameters__

None

__Return value__

Recovery code string

__Description__

This method generates a new passphrase recovery code and returns the value. Additionally, it saves that value to the `passphrase_recovery_code` property to be evaluated.

### evaluate_passphrase_recovery_code(passphrase_recovery_code)

__Parameters__

passphrase_recovery_code

__Return value__

Boolean

__Description__

Evaluates the value passed through the parameter to see if it matches the existing set `passphrase_recovery_code` value.

### set_unique_login_name(login_name = nil)

__Parameters__

login_name - String (optional)

__Return value__

String

__Description__

Returns an adjusted login name based on regular expressions. If no login_name parameter is passed, then the object's `login_name` property is used.


### login_name_unique?(login_name = nil)

__Parameters__

login_name - String (optional)

__Return value__

Boolean

__Description__

Evaluates if the user's login name is unique. If there is a value for the parameters, it will evaluate the value in the parameters. If no parameters are set, it will determine the value returned by the `@user.set_unique_login_name` method.

### valid_passphrase_confirmation?(passphrase,passphrase_confirm)

__Parameters__

passphrase - String
passphrase_confirm - String

__Return value__

Boolean

__Description__

This method is used in situations where a user must enter their passphrase twice. If both values of the standard 'passphrase' field and the 'passphrase_confirm' field match, the method will return true.

### create_associate_preference

__Parameters__

None

__Return value__

Preference object

__Description__

Creates a new Preference object with default values and associates it to the user.

### generate_verification_code

__Parameters__

None

__Return value__

String - the verification_code

__Description__

This method generates a new verification code and saves it to the `verification_code` property.

### evaluate_verification_code(verification_code)

__Parameters__

verification_code

__Return value__

Boolean

__Description__

Accepts a verification code as an input parameter, if that value matches the property stored in `verification_code` then this method evaluates to true.

### verify

__Parameters__

None

__Return value__

None

__Description__

This method updates the verified value to `true`.

### verified?

__Parameters__

None

__Return value__

Boolean

__Description__

This method evaluates to determine if the `verified` property is `true`.

## Class Methods
