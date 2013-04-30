# Real Time Rails

Brian, Cardarella, (Dockyard)[http://www.dockyard.com]

When technology or business becomes complacent, there's opportunity for someone to scoop in and take market share.

Real-time is one area where Node.js has outpaced Rails.

Rails was the innovator and is now playing catch up.

Recommend this book: **TCP Sockets**

http://www.workingwithtcpsockets.com

## Web servers:

* Puma
* Rainbow
* Thin

Brian likes Puma.

## Rails 4

Rails 4 is fully concurrent, there is no full-stack lock on a request. 

## Threads

* You will have to lean how to write threaded code in Ruby.
* Being aware of thread safety issues.

## Queues

* Mutex#synchronize
* External queue (Redis lists)
* Push to queue
* Worker pops and run job
* Ensures execution order

## Rails

* Event Machine / Celluloid
* Faye / PUsher.com

## Long Polling

Who cares if it's realtime? Just poll. :) 

## Rails 4 ActionController::Live

* Proxy object for the socket
* Stream response
* Allow control of headers

## Server Sent Events

* One way streaming communication
* Part of HTML 5 spec

## Websockets

* Perfect for rack.hijack
* Two way communication
* Websocket gem

## A Wild Pattern Appears!

1. Client captures events
2. Event data is sent to the server
3. Event data is normalized
4. Event data is broadcast to all connections

## Tubesock

Websockets + rack.hijack

## Challenges

* No Heroku support
* Nginx fights websockets

## The Future

* Integrate rack.hijack into ActionController::Live
* Rails is moving towards the client
* Frameworks like Ember are growing and need a strong backend solution