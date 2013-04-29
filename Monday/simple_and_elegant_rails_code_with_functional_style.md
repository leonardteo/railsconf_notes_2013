# Simple and Elegant Rails Code with Functional Style

Attila Domokos, @adomokos, Hireology

> The work you do is a reflection of who you are.

Michael E Gerber

## Flog gem

For pain analysis. Will check how clean or how big a mess the code is.

> The higher the score, the more pain the code is in.

## Shift code

1. From controllers to models
2. From models to services

Name the service whatever it is supposed to do: e.g. `parses_feed`.

In services class, abstract further into classes for doing certain things. Name classes after verbs e.g. `SplitsFeedToParts`, `ParsesRecrodedAt`

Chain of responsibility design pattern. 

## Light Service

Light Service gem let's you do this.

## Summary

* Get out of the framework
* Code should tell the story. Should read.
* Don't use state if you don't need to
* Separate behavior from data
* Grow your code horizontally
* Make it simple