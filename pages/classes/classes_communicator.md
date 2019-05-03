---
title: Communicator
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: classes_communicator.html
folder: classes
---

## Introduction

The communicator class manages all of the methods that use outbound communication from the system, such as SMS and Emails. The Communicator is a singleton class, and its methods are called from within other classes and controllers whenever it is time to send a message.

Requires `twilio-ruby` gem.

## Modules

* Singleton

## Relationships

## Properties

|Property|Type|
|+-+|
|:account_sid|String|
|:auth_token|String|
|:sent_from_number|String|

## Methods

### initialize

### account_sid

### auth_token

### sent_from_number

### setup_client(account_sid, auth_token)

### document_completion_notification

### organization_invitation

### organization_confirmation

## Class Methods
