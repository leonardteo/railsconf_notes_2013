# Make Your Applications Snappy!
Using Asynchronous Workers with Rails

David Kapp @ Coshx Labs
@Happymrdave

Async workers are things that you use along with Rails, but may not be specifically in Rails.

## Slow stuff

We know what's slow and what's fast. It's not an exact science. It depends on what you're doing and it's relative.

Change the way you construct your application

## Definitions

* Synchronous - Done linearly.
* Asynchronous - Other things might happen.

Most things are a mix. 

* Concurrent - Parallelism
* Parallel - execution multiple things at a time

What we want

Ability to asynchronously process slow things in parallel.

We don't want to slow down our Rails requests.

## Asynchronous worker

* Separate process from Rails
* Reads data from a place and processes it
* Polls the data source to see if there is more work

## Queue?

The data store for async workers is a queue. 

## Focus

Use Rails for what it's good at. Let Rails handle HTTP requests.

Get out of Rails for slow stuff.

## What to use on

* External API's
* Numerical calculations
* Document generation
* Image or video manipulation
* Sending email
* Payment processing
* Geolocation
* Anything that is not immediately required upon responding

Caveat:
* Be careful with mutable state when you have the same object modified by multiple workers.


## New things to add to your system

Basic pieces.

* Data Store
* Worker Processes
* Process Monitor

## Redis

Advanced key-value store

## Resque

Uses Redis to share data with workers.

Workers are separate processes that are mostly self-managing.

Each independent chunk of work is called a "job". A worker does many jobs.

## Monit or God

Keep worker processes alive and working.

Process that will kill/restart other processes (workers) under certain conditions.

## Other Async workers

* DelayedJob
* Sidekiq

Conceptually similar. Don't assue Resque is the best for your job.

Adding in async job processing is a significant architectural change but you get significant new functionality.

## Worker Class

```
class Foo
  @queue = :foo
  
  def self.perform(user_id)
    user = User.find(user_id)
    …
  end
end
```

* @queue
* self.perform method

## Loading Rails

lib/tasks/resque.rake

## Calling

```
Resqueue.enqueue(Foo, user.id)
```

Whatever args you pass are serialized as JSON. Don't send in objects! Pass in simple values. Pass the id if possible.

## Start up a worker

```
QUEUE=email rake resque:work
```

## How many workers should I run?

It depends on workload.
Start with 2 or 3, then monitor queue size. Adjust as needed.

## Logging

Resque has its own logger. `Resque.logger`

Defaults to STDOUT. Configure as you like.

Don't write it to Rails log.

## Verbosity

Args VERBOSE and VVERBOSE are useful for development. Deprecated in Resque 2.

Production log is often buffered. Make sure that it really is logging.


## Resque web

Sinatra app that is mounted in your rails app.

## Tips

You must restart workers to pick up on code changes. They do not automatically reload like Rails.

Schema changes while workers are runing will confuse them a lot.

Restart workers when you make code changes.

Test by disabling enqueueing so that things run inline.

`Resque.inline = true`

## Plugins

Has hooks that you can use. E.g. resque-scheduler.

