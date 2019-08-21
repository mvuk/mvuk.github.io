---
title: Application Controller
last_updated: July 2019
sidebar: primary_sidebar
permalink: controllers_application.html
folder: controllers
---

## Introduction

The Application Controller is what all other controllers inherit from. Any methods and actions taken here apply to the entire application.

## before_actions

The following methods are called before any page (or POST controller action) loads anywhere on SafeTow.

### set_session_actor

### set_session_role

### set_menu_link

## Methods

### confirm_logged_in

This method evaluates if a user is logged in. If he is not logged in, then he is redirected to a login page. It is included throughout many more controllers.

### set_session_actor

This method takes in parameters from the session cookie of the __session[:user_id]__ of whichever Actor is logged in. Then, it does a lookup in the database to find who has that ID and retrieves the appropriate object that is used throughout the application.

### set_session_role

This method uses the __@actor__ which was found in the previous method, and then sets

### role_access_authentication(*roles)

A variable number of __Role__ classes can be passed in (as the class name, such as "TowTruckDriver", "Manager") and the __@actor__ who is defined from the __set_session_actor__ method is evaluated true or false if they are authorized to view that page.

Then they are redirected with the __role_access_redirect_gateway__ method, which means that if they are not logged in at all they will be redirected to the login page. If they are logged in as an role who is unauthorized, they will be redirected to the appropriate role's homepage, such as the Vehicle Operator home or the administrator dashboard.

### role_access_redirect_gateway

This method is called in moments when an __@actor__ must be redirected to a different view. 

If they have not yet set up any roles, they will be redirected to the onboarding page where they select a role.

If they already have a role set up, a switch statement is used to filter them to the appropriate home page.

If the session trying to access the URL is not signed in, they are taken care of by the separate __confirm_logged_in__ method before this method is called.

### set_menu_link

The SafeTow application for mobile users utilizes a hamburger menu icon in the top left. However, not every "view" of the application it is right to display a hamburger menu icon in that spot, sometimes you need a back button, sometimes you need another type of button with a link to a specific page.

The __@menu_link__ instance variable takes care of this. This method by defaut sets the value to __"menu"__.

In the individual views and controller methods, the value of this instance variable can be overwritten, for example as __"@menu_link = "/"__. That means that on this page, the hamburger icon will be replaced with a back button icon that resolves to the URL which was assigned there.

### set_dismissed_declined_services

This method is utilized by the Tow truck driver when dismissing away declined services #TODO move it into vehicle operator controller?