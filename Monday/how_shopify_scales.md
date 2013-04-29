# How Shopify Scales

John Duff, Shopify

## Stack

Stack is not really that special.

* Ruby 1.9.3
* Rails 3.2
* Percona MySQL
* Unicorn
* Memcached
* Redis

Stats:

* 53 App servers
* 1590 Unicorn workers!
* 5 Job servers
* 370 Job workers

9.9 million orders per year.

2000 sales per minute on Cyber Monday.

Same codebase since 2004! Upgrades and grown till today.

We now have 468 models!

Issue with Unicorn. 1 request == 1 process. Constraint on DB connections.

Requests per minute = num_workers * 60/response_time

## Scaling

1. Increase workers
2. Reduce response time

## Know the system

1. Avoid network requests
2. Speed up unavoidable network calls

## Tools

1. New Relic
2. Splunk for logs
3. StatsD
4. Cacti - Mysql
5. Conan - Load Testing

Put dashboards in rooms so that everyone can see key metrics.

## Caching

* Use **cacheable** gem. Looks awesome
* **identity_cache** gem.

## Get out of my process

1. Use **resque**

## Extract stuff as services

Move stuff into services as needed.

## Hire a DBA

If you're fiddling with DB variables, hire a DBA consultant. Percona for MySQL.



