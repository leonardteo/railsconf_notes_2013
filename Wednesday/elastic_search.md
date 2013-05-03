# Using Elastic Search with Rails Applications
Brian Gugliemetti, Spiceworks

## What is it?

* Open source RESTFUL search engine build on Apache Lucene
* Provides clustering, failover, etc.

## How we got here

* Aggregating product catalogs from multiple partners
* Wanted auto-complete for product searches
* Filterable searches on product groups
* Replace database full-text search
* Bring site search in-house

## Terms

### Node

Node is an instance of elasticsearch that belongs to cluster

### Shard

Data partition within a node. There are primary and replica shards. More shards == faster indexing

### Replica

Copy of primary shard used to increase performance and handle failover.


## Index

Index is the top level data partition. There are many indices within a cluster. Splut across multiple shards.

## Document Type

Each document in an index has a type.

## Document ID

## Tire gem

1. Install and start elasticsearch
2. Add tire to Gemfile
3. Bundle install
4. Edit AR models to include Tire::Model::Search and Tire::Model::Callbacks
5. Import data into ES using Rake or Model.import

