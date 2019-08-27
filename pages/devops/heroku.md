---
title: Heroku
last_updated: August 22 2019
sidebar: primary_sidebar
permalink: devops_heroku.html
folder: devops
---

## What is Heroku? Why do we use it?

Heroku is a __Platform as a Service__ solution. That means it is one step of abstraction above Amazon Web Services, which they use behind the scenes. They are a platform where we deploy our application.

We take our Ruby on Rails project files for SafeTow, deploy them through Heroku, and then all of the services of running and managing servers is abstracted away from us, and we just pay per usage.

Heroku is meant for situations where we have a single project folder with one main process, such as our Rails application. It is not meant for situations where you have many different programs running together in connection with one another like a mail-server. Those situations we are better suited for a dedicated Amazon AWS EC2 instance.

## Billing

Heroku charges us based on usage of __"dynos"__. The dynos will correspond to commands that we would run on a server. For example, running the `rails server` command corresponds to one dyno. 

## How is Heroku set up?

### Project structure

Heroku projects are set up with this following hierarchy.

- Team ("SafeTow")
    - App/Pipeline ("safetow-pipeline")
        - App <Staging>
        - App <Production>

We have our __team__ of which all users are members. There those team members have access to our __pipeline__ which contains an __app__ for each of our different environments.

We develop locally, and then push our code up the the _staging_ app. That will give us access to a staging version hosted on the web with Heroku at a private URL we access. From there we evaluate that the app is working, and then _move the app_ from our _staging_ to _production_ environment in the pipeline. The production version of the application is what the public will see.

#### Setting up a new project for Neo4j Graph database + Rails app

There are several different ways to set up new _apps_ in Heroku, but none in the official documentation cover the situation of using a graph database with it. As a result, there is a preferred method we use that is agnostic to any database, because the Heroku docs are opinionated towards using a PostgreSQL database. Screenshots of the pages mentioned in these steps are included in the sections below of this documentation page.

1. Create an empty application project in Heroku web console
2. Go to the _Resources_ tab for the purpose of adding in _Add-Ons_
3. Add GrapheneDB and Redis Cloud add-ons to the project
4. Go to the _Settings_ tab and then the _Config Vars_
5. Copy the variables into the appropriate files as variables into the rails project for staging and production environments: REDISCLOUD_URL -> "config/cable.yml", GRAPHENEDB_URL -> "config/neo4j.yml", SECRET_KEY_BASE -> "config/secrets.yml"
6. Set up the Heroku CLI on your local machine (https://devcenter.heroku.com/articles/heroku-cli)
7. Push up your local repository into the Heroku app

#### Front end vs Back end vs DB access in API mode

\#TODO as React Native is implimented as our front end and we move our application in Rails to being just API mode, the following link covers the topic: https://blog.heroku.com/a-rock-solid-modern-web-stack

### Pipeline

Heroku has more than one "endpoint" where the application is hosted. See the following image as an example.

![heroku dashboard overview](/images/documentation_images/heroku/heroku-pipeline.png)

First we push our application up to staging, evaluate it, then move it over to production. Each environment has its own separate Neo4j database and Redis server and they can run concurrently, and since we use the config variables there is no need to manually make any different adjustments in code throughout the application.

### Connection with local repository and pushing up to Heroku

First, get everything set up:

1. Follow this guide from the Heroku website to install the CLI and log in: https://devcenter.heroku.com/articles/heroku-cli
2. Navigate in your command line to the project, then set the "Heroku remote" to the empty app set up on Heroku's site with this guide: https://devcenter.heroku.com/articles/git

Now, you can make changes to your local project and updates. Use the 

1. Push up your changes to get as you always would: `git add .`, `git commit -m "<message>"`, `git push`
2. Push the changes to Heroku: `git push heroku master`

Now your code repository will be sent to Heroku, and your history of pushes and status will all be shown on the main Heroku dashboard.

#### Procfile

In the root of our project directory, we create a file titled __Procfile__. When we push up to Heroku, whatever is written in our Procfile will be executed on their service. We use the following Procfile:

```text
web: bundle exec puma -t 5:5 -p ${PORT:-3000} -e ${RACK_ENV:-development}
```

This means we are executing rails to run the __puma webserver__ with __five threads running concurrently__. If no __PORT__ is specified in our environment variables it will default to 3000, and if no __RACK_ENV__ (environment variable) is set then it will default to development mode. See the section below on environment variables to see how we manage this.

### Continuous Integration (CI)

\#TODO Set this up

Heroku has built in features for CI. What this means is that we write tests in the Rails _test_ folder, and then when we push it up to Heroku the tests will all automatically run. 

If the tests fail, then we will see the logs and errors and we can fix it in local development then try again to redeploy. If the test pass then the program will continue to run and upload to the __staging environment__. There we can double check it again and then push to __production environment__.

The tests are run with a new "dyno", so we are billed per-second that the command takes to run.

https://www.youtube.com/watch?v=4lJVzdA11OQ

### Execute Command Line Tasks (such as Rake)

Often times we may want to run specific rake tasks along side the application running in the cloud. Generally we will use `heroku run <command>` and that will run the command from the root of the Rails project up in the cloud.

This page has the full documentation from Heroku on the topic: https://devcenter.heroku.com/articles/heroku-cli-commands

Let's say we want to run our data import task. Locally we would execute this as `rake import:actors`. To execute this on the cloud, we navigate to our local project on our computer and execute the command `heroku run rake import:actors` and then the Heroku CLI tool will run the program up in the cloud. There is also a button in the Heroku web console to execute directly from there.

## Heroku Application Dashboard

### Overview

This page shows you the project at a glance. The right hand column activity is a list of all your recent pushes from the local repository.

![heroku dashboard overview](/images/documentation_images/heroku/heroku-dashboard-overview.png)

### Resources

The project resources, or _add-ons_ refer to other programs such as databases that run alongside our primary Rails app. Each one is charged at different pricing tiers depending on usage and functionality.

Heroku manages the resources' paths, and they are stored in the __Config Vars__ under Settings that we can use throughout the application.

![heroku resources](/images/documentation_images/heroku/heroku-resources.png)

#### GrapheneDB - Neo4j

The Heroku implementation of Neo4j is called GrapheneDB. Database backups, downloads, logs and web access directly into the Neo4j Browser are all possible here. One can even directly manipulate the data through the web console, deleting nodes, adding new content, etc.

![heroku graphenedb](/images/documentation_images/heroku/heroku-graphenedb.png)

### Deploy

![heroku deploy](/images/documentation_images/heroku/heroku-deploy.png)

### Metrics

![heroku metrics](/images/documentation_images/heroku/heroku-metrics.png)

### Activity

![heroku activity](/images/documentation_images/heroku/heroku-activity.png)

### Settings

![heroku settings 1](/images/documentation_images/heroku/heroku-settings-1.png)

#### Config Vars - Environment Variables

There are many situations in the Rails Application where we need to load in various different environment variables based on the specific deployment.

![heroku settings 2](/images/documentation_images/heroku/heroku-settings-2.png)
