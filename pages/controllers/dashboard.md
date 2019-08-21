---
title: Dashboard Controller
last_updated: July 2019
sidebar: primary_sidebar
permalink: controllers_dashboard.html
folder: controllers
---

## Introduction

\#TODO merge this into the administrator dashboard controller?

The reason that this controller exists is that we want to have the appearance and functionality of what the Administrator (or similar type of role) will do in the back-end, and then replicate that behavior through inheritance in other controllers.

One example is in documents controller. We want to have the "view" action of the document be seen with the appearance of the Administrator panel, however the "create" method must be used by a Tow truck driver who would otherwise not have the permission to access ANY view that would be part of an Administrator dashboard.

"Fleet Dashboard" does not inherit from this dashboard, so that should be addressed as well.

That leaves this section technically working but a better solution exists.

