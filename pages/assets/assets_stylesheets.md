---
title: Stylesheets
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: assets_stylesheets.html
folder: assets
---

## Introduction

Stylesheets can be found in the folder `app/assets/stylesheets`.

## Stylesheet Libraries

### Sass

The project uses the `sass-rails` gem to make use of the [Sass](https://sass-lang.com/) extension to the CSS language.

In the `application.rb` file, the follwing line of code is included to set the syntax for stylesheets to be set to Sass.

```ruby
config.sass.preferred_syntax = :sass
```

### Bootstrap

[Bootstrap 4](https://getbootstrap.com/docs/4.0/getting-started/introduction/) is the stylesheet framework that is used for the SafeTow Rails web application. All layout mechanics and UI components come from this library and then are extended by custom css in the `theme.sass` file.

In this project, Bootstrap is managed by the [yarn](/overview_package_managers#yarn) package manager.

## Stylesheet files

### theme_variables.sass

This file contains all of the variables that are used throughout the theme. This includes features such as colors, font choices, gradients and shadow sizes. Using sass variables ensures that there is a standard and consistent set of user-interface elements throughout the application.

### theme.sass

This is the master file that contains all of the custom style changes to the application. 

\#TODO discuss the usage of custom colors for buttons, etc.
