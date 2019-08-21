---
title: Comments Controller
last_updated: July 2019
sidebar: primary_sidebar
permalink: controllers_comments.html
folder: controllers
---

## Introduction

In SafeTow, the "comments" are reviews left after a service

## Methods

### index

### show

### new

### edit

### reply

__POST__

The reply method is used for a comment's replies. When Alice leaves a comment about Bob, Bob will be able to reply by passing a string through to this action.

### comment_after_service

__POST__

This method creates a comment and then associates it to the transaction, author and party which it is written about.

\#TODO merge it with the __create__ method that would otherwise go unused?

### create

### update

### destroy
