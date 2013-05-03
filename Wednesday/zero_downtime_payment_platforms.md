# Zero downtime payment platforms

Prem Sichanugrist, Level Up and Ryan Twomey, Thoughtbot

learn.thoughtbot.com

Promo code: RAILSCONF

20% off first month

20% off everything else on the store

LevelUp is a mobile payments company. Show QR code on phone to create an order. 

$1,000 per minute.

## Two different kinds of downtime

* Us - our code
* Them - somebody else's code

## Them - External services

* External database
* Email provider
* Caching provider
* Payment gateway

## What happens if our payment gateway goes down?

When a new order comes in and our payment gateway goes down, our order gets rejected.

Customer turns away and is unhappy.

## Failover mode

* Accept low risk orders
* Store them and charge customer later

## Risk assertion

If the order amount < $x, consider as low risk.

Pros:

* Customers can make purchase
* No lost orders

Cons:

* Requires a human all the time. Requires human to be there when the gateway goes down.

## Automated Failover

* Wrap a charge in a timeout
* If it times out, evaluate risk
* If low risk, save it and return success
* Cron task to retry timed-out orders


## When WE are down

* Application error
* Heroku is failing
* AWS went away

Nothing much we can do!

Always use a CDN to serve your static pages and assets.

Chocolate - request replayer

Dynamic failover service - powered by Akamai

Using Akamai Dynamic Router, we can route to different stuff like the Rails app, Chocolate and CDN.

## Chocolate

VCR for web requests.

Is a Sinatra application. 

Perform risk assertion.

Store raw request in the database.

Replay request later.

Store on a different server.

But same risk as before.

* If an order is accepted but can't be charged, we're still on the hook.
* Our support team follows up with customers to keep lost $$ as low as possible.

## How it works

* Single POST endpoint to save an order into the database
* Pulls out interesting things (amount, customer to charge, etc.)

## If order looks real…

* Calculate risk
  * Is low, save everything: params, headers, etc. to DB
* Returns a response that looks identical to a production response

## When we're back up

* Order model on chocolate has a replay method
* Manual process run by support team to track results and follow up if necessary.

## Deduping

* Akamai injects a unique request ID for every order
* Store this on each order in production and on replays in chocolate
* Chocolate sends this as part of a replay

## When to failover

* Akamai has a rule that if a POST to our order #create endpoint takes > 15 seconds, retry the same request on chocolate
* Sometimes production will actually succeed, but not a problem: chocolate de-dupes

## Pros of using something like Akamai

* Allows you to autoreplay to separate endpoints
* If your site goes down it appears like it's never down

## Cons

* Adds fair layer of complexity
* Expensive to run

## Stuff

1. Your site will go down
2. Use a replayer for critical web requests
3. Accept some risk to keep customers happy
4. Keep your endpoints lean and fast
5. Use a CDN





