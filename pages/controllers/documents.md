---
title: Documents Controller
last_updated: July 2019
sidebar: primary_sidebar
permalink: controllers_documents.html
folder: controllers
---

## Introduction

Documents are used for validation of actors in the system. For example, during signup a Tow Truck Driver will upload his documents such as a __profile picture__, a __drivers license__ and a __tow truck license__ and then an Administrator will verify that these documents are valid.

This controller inherits from the __DashboardController__ so the __show__ action (which is only utilized by the Administrator actor) behaves as if it is the extension of the Administrator dashboard.

## Methods

### index

__GET__

### show

__GET__

This action is used by Administrator as part of their dashboard to review a document. All of its details are displayed, along with buttons that link to the __verify__ and __decline__ methods.

### new

__GET__

### edit

__GET__

### create

__POST__

This controller action takes an parameters defined in Document class with [paperclip library](/assets_images.html) and uploads to AWS. The document is stored in the database with a pointer to the URL on AWS where the file is stored.

Association is set to the appropriate tow truck driver and then an email is sent off to the Administrator that there is a requirement to validate a document.

### update

__PATCH/PUT__

Used to replace a document with another and then "unverify" it. Feature is built out but not used, instead the process of replacing the entire document object with another is preferrred.

### destroy

__DELETE__

### verify

__POST__

Used by an Administrator to approve of a document.

### decline

Used by an Administrator to decline a document.