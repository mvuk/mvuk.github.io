---
title: Docker
last_updated: July 2019
sidebar: primary_sidebar
permalink: devops_docker.html
folder: devops
---

Docker is a program that creates and manages "containers".

A container corresponds to a virtualized environment that mimics a GNU/Linux operating system image with pre-configured and pre-installed software which we customize and set to our liking.

We create a _"docker container"_ for each component of our project. Since we are building as a "monolith" architecture rather than a "microservices" architecture at this time, that means we need to have two docker containers. A docker container for our __application__ and another one for our __database__.

## Getting started with Docker

You must begin by installing Docker, which you can get for macOS at [this link](https://docs.docker.com/docker-for-mac/install/).

## docker-config-data

I have set up a folder in the SafeTow project root titled docker-config data. In there, I store configuration data that is involved with the startup sequence of docker containers.

![docker-config-data](/images/documentation_images/docker-config-data.png)

The reason this has to exist, is that dockerfiles must be named "Dockerfile", they cannot be named anything else. As a result, if we wanted to include both the Neo4J and the Rails dockerfile to be accessed from a single directory, they cannot be in the same folder. I would have set up both Docker files in their own folder, with one exception. 

Dockerfiles cannot load in data that is _"above them"_ in the folder hierarchy, only below. This means that the Ruby on Rails dockerfile must be in the root of the project, and the Neo4J database nested in a deeper folder with any files to include with it at the same depth of folder hierarchy.

### schema.yml

We make sure to include a schema.yml file in this folder to be used with the project. Whenever you are running an application with a database, there needs to be a series of migrations that are run against the database that define what the schema will be.

Thankfully, Neo4J and Neo4j.rb make that convenient for us. While in local development, one can use the "rake tasks" to generate schema migrations. Full details about this process can be read about in the [neo4j.rb documentation here](https://neo4jrb.readthedocs.io/en/latest/Migrations.html#the-schema-file).

The schema needs to be updated when new models are defined, or their unique keys and unique identifiers are altered. They save manually to the `db/neo4j/schema/schema.yml` path in the 'safetow-rails' project directory. Then, what needs to be done is that path is manually copied and pasted when it is time to deploy into `docker-config-data/schema/schema.yml`. A message included in the file from the maintainers of neo4j.rb even says directly: __"It's strongly recommended that you check this file into your version control system."__

The reason we cannot depend on an automated task for this is that the `db` folder must be created fresh at every new deployment. That means the `db` folder is included in our `.gitignore` and `.dockerignore` files and is therefore not included in our docker containers or git repository to prevent conflicts. 

\#TODO A command line task can be set up to automate copying it over. 

The following excerpt contains a sample of what is included in one of these files.

```yml
# This file is auto-generated from the current state of the database. Instead
# of editing this file, please use the migrations feature of ActiveNode to
# incrementally modify your database, and then regenerate this schema definition.
#
# Note that this schema.yml definition is the authoritative source for your
# database schema. If you need to create the application database on another
# system, you should be using neo4j:schema:load, not running all the migrations
# from scratch. The latter is a flawed and unsustainable approach (the more migrations
# you'll amass, the slower it'll run and the greater likelihood for issues).
#
# It's strongly recommended that you check this file into your version control system.

---
:constraints:
- CONSTRAINT ON ( `neo4j::migrations::schemamigration`:`Neo4j::Migrations::SchemaMigration`
  ) ASSERT `neo4j::migrations::schemamigration`.migration_id IS UNIQUE
- CONSTRAINT ON ( actor:Actor ) ASSERT actor.id_key IS UNIQUE
- CONSTRAINT ON ( address:Address ) ASSERT address.id_key IS UNIQUE
- CONSTRAINT ON ( comment:Comment ) ASSERT comment.id_key IS UNIQUE
- CONSTRAINT ON ( contactinfo:ContactInfo ) ASSERT contactinfo.id_key IS UNIQUE
- CONSTRAINT ON ( demodata:DemoData ) ASSERT demodata.uuid IS UNIQUE
- CONSTRAINT ON ( document:Document ) ASSERT document.uuid IS UNIQUE
- CONSTRAINT ON ( email:Email ) ASSERT email.id_key IS UNIQUE
- CONSTRAINT ON ( location:Location ) ASSERT location.id_key IS UNIQUE
- CONSTRAINT ON ( locationservices:LocationServices ) ASSERT locationservices.uuid
  IS UNIQUE
- CONSTRAINT ON ( note:Note ) ASSERT note.id_key IS UNIQUE
- CONSTRAINT ON ( organization:Organization ) ASSERT organization.uuid IS UNIQUE
- CONSTRAINT ON ( person:Person ) ASSERT person.id_key IS UNIQUE
- CONSTRAINT ON ( phone:Phone ) ASSERT phone.id_key IS UNIQUE
- CONSTRAINT ON ( preference:Preference ) ASSERT preference.id_key IS UNIQUE
- CONSTRAINT ON ( product:Product ) ASSERT product.id_key IS UNIQUE
- CONSTRAINT ON ( role:Role ) ASSERT role.uuid IS UNIQUE
- CONSTRAINT ON ( service:Service ) ASSERT service.id_key IS UNIQUE
- CONSTRAINT ON ( session:Session ) ASSERT session.id_key IS UNIQUE
- CONSTRAINT ON ( task:Task ) ASSERT task.uuid IS UNIQUE
- CONSTRAINT ON ( transaction:Transaction ) ASSERT transaction.id_key IS UNIQUE
- CONSTRAINT ON ( trustedcontact:TrustedContact ) ASSERT trustedcontact.id_key IS
  UNIQUE
- CONSTRAINT ON ( url:Url ) ASSERT url.id_key IS UNIQUE
- CONSTRAINT ON ( user:User ) ASSERT user.id_key IS UNIQUE
- CONSTRAINT ON ( vehicle:Vehicle ) ASSERT vehicle.id_key IS UNIQUE
- CONSTRAINT ON ( website:Website ) ASSERT website.id_key IS UNIQUE
:indexes: []
:versions:
- '20190611172001'
- '20190611172006'
- '20190611172009'
- '20190611172011'
- '20190611172014'
- '20190611172016'
- '20190611172018'
- '20190611172021'
- '20190611172023'
- '20190611172026'
- '20190611172028'
- '20190611172031'
- '20190611172033'
- '20190611172035'
- '20190611172038'
- '20190611172040'
- '20190611172042'
- '20190611172045'
- '20190611172047'
- '20190611172049'
- '20190611172051'
- '20190611172402'
- '20190611172405'
- '20190611172409'
- '20190611172412'
- '20190611172414'
- '20190611172417'
- '20190611172419'
- '20190611172421'
- '20190611172424'
- '20190611172426'
- '20190611172429'
- '20190611172431'
- '20190611172434'
- '20190611172436'
- '20190611172438'
- '20190611172440'
- '20190611172443'
- '20190611172445'
- '20190611172447'
- '20190611172449'
- '20190611172452'
- '20190611173041'
- '20190611173044'
- '20190611173046'
- '20190611173049'
- '20190611173051'
- '20190611173054'
- '20190611173056'
- '20190611173059'
- '20190611173101'
- '20190611173103'
- '20190611173106'
- '20190611173108'
- '20190611173111'
- '20190611173113'
- '20190611173116'
- '20190611173118'
- '20190611173120'
- '20190611173123'
- '20190611173125'
- '20190611173128'
- '20190611173132'
- '20190611184355'
- '20190611184359'
- '20190611184405'
- '20190611184409'
```

## Dockerfiles

### SafeTow Rails Dockerfile

```dockerfile
# Base image
FROM ruby:2.5

# Setup environment variables that will be available to the instance
ENV APP_HOME /safetow

# Installation of dependencies
RUN apt-get update -qq \
  && apt-get install -y \
      # Needed for certain gems
    build-essential \
         # Needed for postgres gem
    libpq-dev \
         # Needed for asset compilation
    nodejs \
        # Needed for working live in the container
    vim \
    # The following are used to trim down the size of the image by removing unneeded data
  && apt-get clean autoclean \
  && apt-get autoremove -y \
  && rm -rf \
    /var/lib/apt \
    /var/lib/dpkg \
    /var/lib/cache \
    /var/lib/log

# Create a directory for our application
# and set it as the working directory
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

# Add our Gemfile
# and install gems

ADD Gemfile* $APP_HOME/
RUN bundle install

# Copy over our application code
ADD . $APP_HOME

# Pull in schema information from pre-set
ADD docker-config-data/schema/schema.yml $APP_HOME/db/neo4j/schema.yml

# Pull in schema information from dev env
#ADD db/neo4j/schema.yml $APP_HOME/db/neo4j/schema.yml

# Run migrations from the schema file, then run the rails server

RUN chmod +x $APP_HOME/docker-config-data/scripts/migrate_and_run.sh
CMD $APP_HOME/docker-config-data/scripts/migrate_and_run.sh
```

We start off with a base image of Ruby 2.5. This is a Debian GNU/Linux machine wherre Ruby 2.5.0 is pre-installed, to match our setting for using this in the project. That means we are working within a full GNU/Linux file system that has all of the features of any terminal environment where we can execute commands and use the apt repository.

We create a directory '/safetow' at the root.

We install programs that are required through the apt-get repository.

We install all of the gems required for the project, and copy over the database schema. We make our migrations and run server script executable with chmod +x, then we execute it.

Every docker container can conclude with a single command to be run with the _'CMD'_ value. In our situation, we must run a command that runs a script that has all of the tasks we want to accomplish, and then conclude by running the rails server with the settings we request.

#### migrate_and_run.sh

```sh
#!/bin/sh

echo "migrate_and_run.sh"
echo "Waiting for neo4j server startup, then attempting to migrate"

# sleep gives time for startup
sleep 10

# Make sure that no rails process is already running
echo "Attempt to remove any running server.pid..."
if rm tmp/pids/server.pid ; then
    echo "tmp/pids/server.pid removed"
else
    echo "no existing server.pid was present"
fi

# sleep gives time for startup
sleep 10

ruby manage_migrations.rb

# Start up the rails server
echo "Running rails server (env=$ENVIRONMENT_VARIABLE)"
bundle exec rails s -p 3000 -b '0.0.0.0' -e $ENVIRONMENT_VARIABLE
```

This script begins by giving the Neo4J database 10 seconds to start up and get moving. We set in the rails application configuration to wait on server to start up before executing tasks, however this is still useful to prevent needless polling that we would know to be declined. Starting up the Neo4J server generally still takes less than 10 seconds.

We include a "fail-safe" method to prevent multiple server processes from running simultaneously during startup.

We then execute the `manage_migrations.rb` ruby script to run the tasks associated with migrating the database using the 'schema.yml' file that was copied above in the dockerfile.

An important note is that the `$ENVIRONMENT_VARIABLE` is passed in. This is defined in the docker-compose file for [local development](/devops_local_development.html) and within the configmap for [kubernetes](/devops_kubernetes.html) (where it is passed in as a parameter from [SafeTow CLI](/devops_safetow_cli.html)).

#### manage_migrations.rb

This is a ruby script that runs the migrations for the startup process, it is called within 'migrate_and_run.sh' to run the tasks associated with starting up.

```ruby
require "open3"
include Open3

puts "manage_migrations.rb"

# Now run migrations

out, err, status = Open3.capture3("touch .manage_migrations_ran")
puts out, err, status

# Try just loading schema

puts "Copy over the schema to the proper directory"
p "mkdir db && mkdir db/neo4j"
out, err, status = Open3.capture3("mkdir db && mkdir db/neo4j")
puts out, err, status

p "cp docker-config-data/schema/schema.yml db/neo4j/schema.yml"
out, err, status = Open3.capture3("cp docker-config-data/schema/schema.yml db/neo4j/schema.yml")
puts out, err, status

puts "Load the schema"
p "bin/rails neo4j:schema:load[true]"
out, err, status = Open3.capture3("bin/rails neo4j:schema:load[true]")
puts out, err, status

puts "", "Running migrations...", ""

p "rake neo4j:migrate"
out, err, status = Open3.capture3("rake neo4j:migrate")
puts out, err, status

```

The __Open3__ library is used for running command line programs.

\#TODO I may decide to merge this file with migrate_and_run.sh into a single ruby script, so to solidify that ruby is used universally as our scripting language.

### Neo4J Dockerfile

```dockerfile
# Base image
FROM neo4j:3.5.6

ENV NEO4J_AUTH=neo4j/password

ADD neo4j.conf conf/neo4j.conf
```

The Neo4J Dockerfile is very simple. We start off with the Neo4J 3.5.6 community image which is already made [available to us through docker hub](https://hub.docker.com/_/neo4j?tab=description).

Then, we set the username and passphrase for authentication. We are using the username "neo4j" with passphrase "password". Notice that in the SafeTow Rails dockerfile, we hard code in that same username and passphrase confirmation.

\#TODO programmatically set up as environment variables for those two.

Then, we add in a custom neo4j.conf file that we pre-write that has the configuration settings we want.