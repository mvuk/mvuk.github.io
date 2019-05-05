---
title: JavaScript
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 3 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: assets_javascript.html
folder: assets
---

## Introduction

This page will highlight the various JavaScript files and each of their respective purpose within the SafeTow Rails project. Each group of JavaScript functions is grouped into a file where other functions are written in conjuction to achieve a common goal.

## JavaScript libraries

### jQuery

The [jQuery library](https://jquery.com/) is included for usage of manipulating DOM elements. It'

### Google Maps JavaScript API

The [Google Maps JavaScript API](https://developers.google.com/maps/documentation/javascript/reference/) is used for working with interactive maps, directions, geolocation calculations and searching for businesses.

### Chart.js

[Chart.js](https://www.chartjs.org/) is a library for drawing charts. It is useful in displaying data on dashboards.

## Javascript files

### directions.js

This file contains functions for navigation and directions powered by the Google Maps library.

It utilizes data from the customer and tow truck driver's position stored in the database, and then will output for the two parties:

* A path of recommended driving route to be drawn on a map
* Distance in kilometers of driving route
* Estimated time of driving route

### geocode.js

Geocoding is the process of turning the description of an address into geolocation data.

This JavaScript library manages the creation of Body Shops and other dropoff locations for users - both default preferences and ones set during a service.

In this library, we are taking inputs from users looking up physical locations such as body shops or other

### geolocation.js

This library contains all of the functions for collecting location data from the client browser. Location services are not prompted for until a user is signed up and on their dashboard pushing a button to enable broadcasting location as a Tow Truck Driver or to search for Tow Truck Drivers as a Customer.

When the location data is collected from the client, a '/POST' request is sent to the Ruby on Rails application and a new [Location](/classes_location.html) object is created and attached to the user.

### map_manager.js

This library contains any code that is used exclusively by the "Map Manager", where administrators and salespeople can interact with a map that shows all customers and tow trucks in service in the SafeTow application.

### tow_truck_driver_listings.js

This library contains code for managing how customers can sort through Tow Truck Drivers. They can select between a 'map view' or a 'list view'.

### markercluster.js

This library contains the code that powers marker clustering in Google Maps. It is not a part of the standard Google Maps API library but rather an extension.

[This page](https://developers.google.com/maps/documentation/javascript/marker-clustering) highlights a demo of marker clustering, and the specific code I have included within `markercluster.js` comes from [this code library](https://googlemaps.github.io/js-marker-clusterer/docs/reference.html).

### menu.js

This library contains any of the controls for managing the menu's behavior.

### rating.js

This library manages the interactions between users and the visual ratings buttons.

When a user goes to submit a rating (from the [Comment](/classes_comments.html) class), the value of the rating in the database is stored as a numeric value of 1-5. From a user-interface standpoint, the user interacts with clickable stars where he can decide what rating he wants to give. The clicking of the stars changes the numeric value of an invisible form field using JavaScript and then the review is submitted to the database.

### select_dropoff.js

During a [Service](/classes_service.html) a customer is prompted to select where he would like to be dropped off. To correspond with this prompt, he has a visual display with buttons to select from a preferred drop-off location or a new one that he will enter the details of.

This library manages those interactions of user-interface elements and how they correspond to a hidden form that passes the values into the database.

### share_trip.js

This library contains the code for managing interactions with the [SafetyContact](/classes_safety_contact.html)'s user-interface elements.

### turbolinks_manager.js

The Turbolinks library is used in this project for switching between pages. It is included through the `turbolinks` gem.

It is also used for the purpose of refreshing pages while also maintaining scroll position, so that updates can be displayed.

Since the web browser itself is stateless, content could not be dynamic on the screen without refreshes - turbolinks is providing this functionality.

This custom library contains many methods and settings which extend the way that turbolinks is used in the context of our application.

The following methods can be included on any page to manage the turbolinks state as enabled or disabled:
```JavaScript
turbolinksTrigger(); // to enable turbolinks refreshes
setRefreshRate(20000) // to set the rate in milliseconds of the refresh rate

disableTurbolinks(); // to disable turbolinks refreshes
```
