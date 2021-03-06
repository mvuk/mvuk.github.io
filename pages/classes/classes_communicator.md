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
|account_sid|String|
|auth_token|String|
|sent_from_number|String|

## Class Methods

## Instance Methods

### account_sid

__Description__

Returns the Twilio account SID value from where it is stored in the Rails secrets (`Rails.application.secrets.twilio_account_sid`).

__Parameters__

None

__Return Type__

String

### auth_token

__Description__

Returns the Twilio authentication token value from where it is stored in the Rails secrets (`Rails.application.secrets.twilio_auth_token`).

__Parameters__

None

__Return Type__

String

### document_completion_notification(document_owner_id)

__Description__

Sends an SMS message to the owner of documents to notify them that the review process is complete and they are ready to begin using the application.

__Parameters__

document_owner_id - String

__Return Type__

None

### initialize

__Description__

Sets up a new `Twilio::REST::Client` that is required for usage of Twilio API within the Rails project.

__Parameters__

None

__Return Type__

None

### member_begins_service(service_id)

__Description__

Sends an SMS to the organization's manager that a member is using the SafeTow service to order roadside assistance, with a link to follow the trip and view details.

__Parameters__

service_id - String

__Return Type__

None

### member_completes_service(service_id)

__Description__

Sends an SMS to the organization's manager that a member has completed their service, with a link to view details.

__Parameters__

service_id - String

__Return Type__

None

### organization_confirmation(organization_id, member_id)

__Description__

Sends an SMS to the organization manager that the member role has successfully complete their onboarding and is confirmed.

__Parameters__

organization_id - String
member_id - String

__Return Type__

None

### organization_invitation(to_number, organization_id, member_id)

__Description__

Sends an SMS to the 'to_number' that has a link to complete their onboarding process.

__Parameters__

to_number - String
organization_id - String
member_id - String

__Return Type__

None

### send_passphrase_recovery_code_phone(actor_id)

__Description__

Sends an SMS to the actor specified with a link to follow where they can reset their passphrase.

__Parameters__

actor_id - String

__Return Type__

None

### send_verification_code(actor_id)

__Description__

Sends a verification code to the actor specified in the ID along with a link to follow to complete the verification process of the account.

__Parameters__

actor_id - String

__Return Type__

None

### setup_client(account_sid, auth_token)

__Description__

Initializes new `Twilio::REST::Client` from parameter values.

__Parameters__

account_sid - String
auth_token - String

__Return Type__

None

### send_follow_trip_link(to_number, service_id)

__Description__

Sends an SMS message to the 'to_number' with a link to watch the trip and follow along on their own device.

__Parameters__

to_number - String
service_id - String

__Return Type__

None

### sent_from_number

__Description__

Retrieves a value for the phone number that will be sending the outbound SMS messages.

__Parameters__

None

__Return Type__

String
