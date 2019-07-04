---
title: Introduction
last_updated: July 2019
sidebar: primary_sidebar
permalink: devops_introduction.html
folder: devops
---

This document will go over what we need to discuss in terms of dev ops... important things are:

- Local development environment folder
- Docker contianers
- Startup scripts
- Kubernetes set up on KOPS/AWS
- SafeTow.rb control program
- What needs to be edited (eg. the turning off and on)

## Overview

SafeTow is built using Ruby on Rails. It is a monolithic application, meaning that everything pertaining to making SafeTow "run" is stored within one project repository.

This repository is named `safetow-rails`.


## Git repositories

The SafeTow project