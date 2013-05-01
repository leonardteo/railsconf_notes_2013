# Forget Scaling - Focus on Performance

Terence Lee

Bundler and Heroku

Ruby Task Force Meetings (RTFM) haha

## Well architected apps can be scaled easily

Client side vs Server Side

Look at Page Load cycle - what's happening.

## Server Side

Don't let your web server slow you down.

2 types of Ruby servers:

1. Single request server. Web server can only serve 1 request at a time.
2. Concurrent web servers. Can process multiple requests at a time.

## Puma

Multi-threaded web server.

## Unicorn

Heroku recommended. Good concurrency out of the box. Single process but spawns off individual sub processes.

7 parallel connections on single Dyno.

Bundler API uses 16 unicorn workers on 2x dyno = 16 parallel requests per dyno.

Doesn't require thread-safe code, easy to optimize, stable code.

## How many Unicorn Workers do I need in each dyno?

More Unicorn Workers = More RAM.

Enable log-runtime-metrics. 

Check out **Librato** for performance monitoring.

This talk was a big ad for Heroku. :)

