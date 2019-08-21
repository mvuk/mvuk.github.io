---
title: Actors Controller
last_updated: July 2019
sidebar: primary_sidebar
permalink: controllers_actors.html
folder: controllers
---

## Introduction

The actors controller is used for working with the "Actor" who corresponds to the user of the application.

## Methods

### index

__GET__

### show

__GET__

### new

__GET__

This page is used for the initial "sign up" registration.

### edit

__GET__

### create

__POST__

The data about the actor's name, login name and passphrase is all processed into a new Actor object, which then signs in the user. Additionally, a phone number and email address are passed through to create a ContactInfo with a Phone, an Email and makes all of the necessary relationships.

### update

__PATCH/PUT__

Used for updating the passphrase, since other personal information cannot be edited such as first and last name or login name (unique identifiers).

### destroy

__DELETE__

### login_name_unique

__POST__

Calls the method __User.unique_login_name?(params[:login_name])__. Used as an API endpoint for validations, meaning that a user on the Actors#new view can find out if his login name is unique before submitting it through the Actors#create method. 