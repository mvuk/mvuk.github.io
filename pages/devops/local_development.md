---
title: Local Development
last_updated: July 2019
sidebar: primary_sidebar
permalink: devops_local_development.html
folder: devops
---

When working locally, we need to create an environment that matches the settings of how we are working on the deployable Kubernetes cluster. In order to do so, that means we have to use the __Docker containers__ which we have set up for each the Rails application and Neo4J database.

SafeTow is built in Ruby version 2.5.0. When working locally with the project, it is recommended that you install the [Ruby Version Manager (RVM)](https://rvm.io/)) and set your local Ruby version to 2.5.0.


## Docker Compose

__Docker Compose__ is a tool that allows us to take our constructed docker containers and "orchestrate" them together. The following .yml file that sets the details of how they are configured together.

### docker-compose.yml

```yml
version: '3'
services:
  db:
    build:
      context: docker-config-data/neo4j-container-development
      dockerfile: Dockerfile
    ports:
     - "7474:7474"
     - "7473:7473"
     - "7687:7687"

  web:
    build:
     context: .
     dockerfile: Dockerfile
    command: sh ./docker-config-data/scripts/migrate_and_run.sh
    volumes:
#      The /safetow directory within the app is mapped to the local entire project with "."
      - .:/safetow
    ports:
      - "80:3000"
    links:
      - db
    environment:
      - DB_URL=http://neo4j:password@db:7474
      - ENVIRONMENT_VARIABLE=development
#      - ENVIRONMENT_VARIABLE=demo
```

By default, each of the objects will be built into a single network that can communicate with eachother. 

Notice when the docker files are constructed, they are pointing to directories and not pre-built images.

## Commands to run local development

### Starting up

Navigate locally to the root project directory, and run the following commands.

```sh
docker-compose build
docker-compose up
```

You will now see in the terminal output the startup scripts that are triggered by the docker containers. The terminal will output to the console everything that would also be output by running the 'rails s' command usually in local development.

__Changes made locally to the rails project file will be updated in real-time without a server restart.__

### Shutting down

When you want to shut down the local development server, click on the active terminal window where you started up the server and then hit `ctrl + c` on your keyboard.

Once the "safetow_web" and "safetow_db" have shut down, run the following command:

```sh
docker-compose down
```

![terminal docker compose down](/images/documentation_images/terminal-docker-compose-down.png)

Notice the difference in terminal output from simply "stopping" and "shutting down". If you do not do docker-compose down, the containers and their network are not removed from memory and persist in the background.

