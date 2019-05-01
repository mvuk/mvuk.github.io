---
title: GraphQueries
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: April 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: modules_graph_queries.html
folder: modules
---

## Introduction

The intention of this module is to include methods that are used to generate unique identifiers for classes.

```ruby


```

## Modules

* bcrypt

## Methods

### generate_uuid_created_at

__Parameters__

None

__Return value__

String that is used as unique identifier.

__Description__

This method takes timestamp of when the node was created, attaches it to the string of a new UUID that has been generated, encrypts that string with `bcrypt` and returns a string.

## Class Methods
