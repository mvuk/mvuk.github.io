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

### Ruby Channels 

In our application, there is the directory `app/channels/`. In here you will find all of the Ruby logic associated with

### JavaScript Channels
