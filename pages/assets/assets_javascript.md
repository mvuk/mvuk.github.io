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

In the SafeTow Rails project, JavaScript is used throughout the web UI. The __jQuery__ framework is used for the manipulation of the UI elements.

This page will highlight the various JavaScript files and each of their respective purpose within the SafeTow Rails project. Each group of JavaScript functions is grouped into a file where other functions are written in conjuction to achieve a common goal.

## Javascript files

### directions.js

### markercluster.js



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
