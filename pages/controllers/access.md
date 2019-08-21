---
title: Access Controller
last_updated: July 2019
sidebar: primary_sidebar
permalink: controllers_access.html
folder: controllers
---

## Introduction

The access controller is the regulator for accounts logging in and out of the SafeTow application.

## Methods

### home

__GET__

The default page of the app.

### login

__GET__

This is the login page.

### attempt_login

__POST__

The _login name_ and _passphrase_ are passed through this method, and __User.log(login_name, passphrase)__ method is called. A valid login credential will set the __session[:user_id]__ variable to the logged in user, setting the cookie.

### logout

__POST__

Makes all values of the session[] object set to nil, meaning that cookies are cleared. The user is redirected to the login page as a result.