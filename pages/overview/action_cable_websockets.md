---
title: ActionCable and WebSockets
last_updated: Aug 20 2019
permalink: action_cable_websockets.html
folder: overview
---

## What are WebSockets? How do we use them?

WebSockets are an open connection between the client and the server. They allow for the client to send and receive packets of data from the server without making HTTP requests, polling, or requiring page reloads. These open connections are referred to as __channels__.

When packets of data are sent, they are always sent to a specific channel. Then all clients set up to that channel will receive the data. Clients can be a part of multiple channels at one time.

There are multiple ways to implement these channels. You can for example:
- __Put all clients onto one big channel__ (Everyone on the app gets notified of a system-wide notification)
- __Group together several clients into multiple channels__ (Chat rooms. Each chat room has a channel and a new message in a chat room is sent to all of its participants.)
- __Each client gets its own channel__ (Individual messaging to specific clients in real time)

We are using the third option in our situation, this enables us to target individual devices and prompt actions to occur on those devices. For the scope and use-case of SafeTow, the only data we are passing through these packets are prompts to reload a page. 

At any time when you are logged into SafeTow, there is an open connection between your device and the serve which is your channel. 

Your login name is used as a key identifier for your channel, for example this means that when __johnsmith__ is logged in, we can remotely control his device by calling a method with __broadcast_channel_user_johnsmith__ as a parameter. This can be used to remotely trigger his page to reload and bring in new data.

## What is ActionCable?

ActionCable is the library included in Ruby on Rails for working with WebSockets. WebSockets are the technology we are working with, and ActionCable is only one of several options bringing to the table its own syntax made up of Ruby and JavaScript. Another library that could be used is __AnyCable__, which was created by the EvilMartians agency who are prominent in the Ruby on Rails development community and promote their library in many conferences and talks. ActionCable is not actually built to be the most performant solution for Websockets _(see: https://github.com/rails/rails/issues/26999)_, however it is the most useful for most use cases. Once the load goes up beyond 10,000 connections, performance may start to suffer and we can investigate replatforming to another form of using WebSockets. 

## Configuration

### cable.yml

Websockets need to connect to the __Redis__ service to be used. In order to set up that configuration, we go to the configuration file found at `config/cable.yml` and set up how we will connect them at each different environment. If we use __async__ in a situation where there are clients, the behavior is unpredictable (delays, not always working).

```yml
development:
  adapter: redis
  url: redis://localhost:6379/1

test:
  adapter: async

production:
  adapter: redis
  url: <%= ENV["REDISCLOUD_URL"] %>
```

Each of the different environments is set up with a different configuration. 

In our Gemfile, we must ensure that the Redis gem is installed. It is done so by default in Rails, the gemfile contains the following lines:

```
# Use Redis adapter to run Action Cable in production
gem 'redis', '~> 4.0'
```

Locally, in __development__, we use a local version of Redis on our computer. In order to have the Redis service running at localhost:6379, we set up the following commands in our terminal.

`brew install redis` (Install Redis to mac OS with brew package manager.)

`redis-server` (Runs the Redis service locally at port 6379.)

Once this is set up, every single time that you run rails locally in development mode, we must also run this `redis-server` command before we run `rails server`, or else the Ruby on Rails server running with Puma won't even start!

For the __test__ environment, there are no WebSocket channels used because there are no clients. This means that we use the connection type __async__.

For the __production__ environment, we use an environmnet variable that is passed in. Note that 


## Channels

### Application Cable

In the directory `app/channels/application_cable`, you will find two files that are relevant: `channel.rb` and `connection.rb`, the latter of which we are more concerned about.

#### connection.rb

This file establishes the connection between the client and the server, The methods will used below in the __Ruby Channels__ section of this guide.

The important part to look at here is the method __find_current_user__ gets called when a connection starts. The code __request.session.fetch('user_id', nil)__ will return the value that would usually be returned by __session[:user_id]__, which corresponds to activity that happens in the __Access Controller__ and __User.rb__.

If there is a user logged in, then the connection's _current_user_ attribute will resolve to their username, otherwise the connection attempt will be rejected. There is point within the scope of our application to open a connection to someone who has not yet logged in. Someone in SafeTow who has not yet logged in will just be prompted through the screens to log in or create an account.

```ruby
module ApplicationCable
  class Connection < ActionCable::Connection::Base

    identified_by :current_user

    def connect
      self.current_user = find_current_user
    end

    private

    def find_current_user
      user_id = request.session.fetch('user_id', nil)
      if user_id
        p "ActionCable connected to #{user_id}"
        return user_id
      else
        reject_unauthorized_connection
      end
    end

  end
end
```

### Creating a new channel

We set up a channel in the terminal with the following code at the Rails project default line: `$ rails generate channel Broadcast`. 

We call it the broadcast channel because it deals with the 'broadcasting' of messages of data to each users. It does not have anything to do with "Service Broadcasts", but rather it deals with the fact that the method for sending a message is written as __ActionCable.server.broadcast__, meaning it is a universal messaging channel. \#TODO we can reconsider that name.

That would create two new files that we would work with as dealt with below, see `app/channels/broadcast_channel.rb` and `app/assets/javascript/channels/broadcast.coffee`

### broadcast_channel.rb 

`app/channels/broadcast_channel.rb`

This contains the ruby code that deals with the subscription of the client to the channel. The following code snippet is a simplified version of the code.

```ruby
class BroadcastChannel < ApplicationCable::Channel

  def subscribed
    stream_from "broadcast_channel_user_#{current_user}"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
  
end
```

This means that each member who is "subscribed" to the channel, will have their own subscription with their username. For example, "johnsmith" will be accessible with __broadcast_channel_user_johnsmith__.

### broadcast.coffee

`app/assets/javascript/channels/broadcast.coffee`

This is written in __CoffeeScript__, which compiles into JavaScript as part of the asset pipeline. The syntax of CoffeeScript is meant to more closely resemble Ruby. The channel can also be written in _vanilla_ JavaScript, but CoffeeScript is the standard followed throughout examples and documentation. There are services on the web that you can use to translate JavaScript code into CoffeeScript. The following code is our simple broadcast channel logic.

```coffeescript
App.service = App.cable.subscriptions.create "BroadcastChannel",
  connected: ->
    # Called when the subscription is ready for use on the server

  disconnected: ->
    # Called when the subscription has been terminated by the server

  received: (data) ->
    # Called when there's incoming data on the websocket for this channel
    if data.reload
#      console.log("time to reload!")
#      alert("time to reload!")
      reload()

reload = ->
#  console.log 'Time to reload the page'
  window.location.reload()
  return
```

We have a custom __reload__ method that is written, that will simple reload the window when it is called. For the __received__ situation, that is anytime we call the following method. Keep in mind that the following code is __Ruby__ and it is placed in the __controller action__ where you want the specific channel to be acted on. In our SafeTow system, each channel pertains to a specific different user.

```ruby
ActionCable.server.broadcast channel,
                             options
```

In the following example I show a given situation on how we could practically write that. We use the following Ruby code to deliver data, where we interpolate in the "user_id" for whichever actor we want to message.

```ruby
ActionCable.server.broadcast "broadcast_channel_user_#{user_id}",
                                       reload: true
```

Notice that in the __CoffeeScript__ example for the _received_ method I evaluate "__if data.reload__". Because in the Ruby broadcast __reload: true__ is passed through, it will resolve to true in the CoffeeScript and then the client of the appropriate page is refreshed.

_Any type of data_ can be passed through, for example instead of a boolean value you can pass in an array, then work with that data in the JavaScript on the client side, then determine which appropriate JavaScript should be executed on the client's device. That could be to manipulate the DOM, reload the page, go back a page, call an AJAX request, for a few examples.
 
A good example of this would be during the creation of a service. First, a service is created and saved to the database. Once the service is created, we need to notify all of the tow truck drivers of the new service they are eligible for, then refresh their screens to display it.

This is a snipped from the _create_broadcast_ method in the _services_controller.rb_. It is not the actual full code, but just a shortened example to show the relevant lines of code.

```ruby
@service = Service.new(service_params)
@service.save
@service.broadcast_requests
@service.requests.each do |requested_tow_truck_driver|
  ActionCable.server.broadcast "broadcast_channel_user_#{requested_tow_truck_driver.actor.id}",
                               reload: true
end
```

