---
title: Demo Data
last_updated: Aug 27 2019
permalink: demo_data.html
folder: overview
---

## Overview


## Files

### Actors spreadsheet

We store the data in a spreadsheet at the path __demo_data/actors.csv__. This file contains all of the data.

This spreadsheet does not have to map 1:1 like a RDBMS, instead we can import each row that will correspond to multiple different nodes and models. 

The table must start with an ID row that can be ignored due to the nature of the library for importing data. Since we base our own unique ID based on the login name, it is better to segment these apart into seperate rows.

![demo data](/images/documentation_images/safetow-demo-data-preview.png)

### Images

There are folders of images of saved at __demo_data/images/__, with subfolders for _profile pictures_ and (other) _documents_.

All users will have the same demo documents, of a sample __drivers license__, __tow truck license__ and their __profile picture__.

In the actors spreadsheet, there are pointers to these filenames for the profile pictures. When the import tool runs, these get uploaded to the Safetow S3 bucket via Paperclip.

### Locations

With our demo tow trucks, we use a pre-set latitude and longitude around the Greater Toronto Area in which we are based and test. When we launch the application in demo mode, these pre-set locations stay for the tow truck drivers and they do not move, even if you are logged in as one at a different location it will not update. 

## Import Rake Task

The ruby ecosystem allows us to write scripts known as "rake tasks". These are executed in the command line as commands that start with __rake__. They are executed from the project root and do not require outside configuration.

Tasks are found in the __lib/tasks__ folder, where we start by creating a new file with the title matching task name as __import.rake__.

The following is an abridged version of the task with pseudocode to explain the process, where the notation '_###_' is a replacement for a large codeblock.

```ruby
require 'csv'

namespace :import do

  desc "Import default actors and their roles."
  task actors: :environment do
    filename = File.join Rails.root, "demo_data/actors.csv"
    CSV.foreach(filename, headers: true) do |row|
      p row
      @actor = Actor.create(first_name: row["First Name"],
                            last_name: row["Last Name"],
                            login_name: row["Login Name"])
      @actor.hash_passphrase(row["Passphrase"])
      @actor.save
      @actor.create_preference

      ### Add in contact info

      ### Verify the actor as if he signed in with his phone number

      # Add the appropriate role
      @actor.add_role(row["Role"].constantize)

      if @actor.role(VehicleOperator)
        ### Add in the profile picture
      end

      p 555
      # These roles require additional logic
      if @actor.role(Customer)
        p 556
        @vehicle = Vehicle.create(make: row["Vehicle Make"], model: row["Vehicle Model"], year: row["Vehicle Year"], color: row["Vehicle Color"], license_plate: row["Vehicle License Plate"])

        p 557
        p @actor.role(Customer)
        p @vehicle
        @actor.role(Customer).vehicles << @vehicle
        p 558
      elsif @actor.role(TowTruckDriver)
        @vehicle = Vehicle.create(make: row["Vehicle Make"], model: row["Vehicle Model"], year: row["Vehicle Year"], color: row["Vehicle Color"], license_plate: row["Vehicle License Plate"], vehicle_type: row["Vehicle Type"])
        @actor.role(TowTruckDriver).vehicles << @vehicle
        @organization = TowTruckFleet.create(name: row["Organization Name"])
        @actor.role(TowTruckDriver).organizations << @organization

        @actor.role(TowTruckDriver).update_attributes(price_per_unit_distance: 2,
                                                      unit_distance: "km")

        @actor.preference.update_attributes(radius: 40)

        ### Generate a random number of reviews for the tow truck driver

        ### Set up random prices for his products

        ### Set up the documents 
      end

      if @actor.role(VehicleOperator)
        @location = Location.new(latitude: row["Latitude"],
                                 longitude: row["Longitude"])
        @location.save
        @actor.role(VehicleOperator).location = @location
        @actor.role(VehicleOperator).broadcast_status!(true)
      end

    end
  end

end
```