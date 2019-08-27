---
title: Local Development
last_updated: July 2019
sidebar: primary_sidebar
permalink: devops_local_development.html
folder: devops
---

When working locally, we need to create an environment that matches the settings of how we are working on the deployable Kubernetes cluster. In order to do so, that means we have to use the __Docker containers__ which we have set up for each the Rails application and Neo4J database.

SafeTow is built in Ruby version 2.5.0. When working locally with the project, it is recommended that you install the [Ruby Version Manager (RVM)](https://rvm.io/)) and set your local Ruby version to 2.5.0.

## Running on your local machine

There are __three services__ which must be running locally on your computer to work with Rails locally. 

We must run each of them to start. Rails configration for the development environment is pre-set so that each of them will properly plug in. Ensure that all of the command outlined in this section are run from the safetow-rails project root directory.

- Neo4j Database
- Redis Server
- Rails Server

### Neo4j Database

1. Run `rake neo4j:start`
2. The Neo4j server is running now at port 7474
3. To end the database process from running, run `rake neo4j:stop`

### Redis Server

1. Make sure that redis is installed with `brew install redis`
2. Open new command line window
3. Run `redis-server`
4. Keep this window open for as long as your project is running. Rails server will not run without it.
5. To close, execute `control + c` in the command window

### Rails Server

1. Open a new command line window
2. Run `rails s`
3. Navigate to _"localhost:3000"_
4. To close, execute `control + c` in the command window

__NOTE: Everything below this line with Docker compose is currently not working because Redis is not yet configured and set up into it yet.__ 

---

## Docker Compose

__Docker Compose__ is a tool that allows us to take our constructed docker containers and "orchestrate" them together. The following .yml file that sets the details of how they are configured together.

### docker-compose.yml

```yml
version: '3'
services:
  db:
    build:
      context: docker-config-data/neo4j
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

