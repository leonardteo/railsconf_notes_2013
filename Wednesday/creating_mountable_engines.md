# Creating Mountable Engine

Patrick Peak, @peakpg

Check out BrowserCMS - content management system.

## DRY

Duplication is the root of all evil.

## Start with a library

Write a library and distribute it as a gem. Appropriate if there is no user interface.

What you you want something that's Rails specific?

Plugins are dead. /vendor/plugins are gone.

## Engines

Mini applications that can be factored into other Rails applications.

Using engines, we can focus a gem on specific areas so that we can re-use it.

## Examples

* Spree. E-Commerce shopping cart.
* Devise. Authentication.
* Rails Admin - Admin dashboard.

## Building an engine

`rails plugin new rubypress --mountable`

You'll get a Gemspec.

You'll also get a dummy rails app in test/dummy.

Engines can't live on their own, they need to live with a Rails app.

When you generate a model, controller, etc. it will be namespaces and in a sub-folder.

## Routing

Engines have their own routes. A Rails app can have multiple engines with their own routes.

```
# Inside Rails app
<%= enginename.root_url %>

# Inside Engine
<%= main_app.root_url %>
```

## Migration

Has namespaced tables.

## Versions

Be rational.

Major.Minor.Build

* Major = Backwards inconpatible
* Minor = New Features
* Build = Details

## Issues when mixing engines

1. Dependency issues. 2 engines require different versions of the same gem
2. Authentication. Rails does not have a common authentication model.
3. 