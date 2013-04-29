# Maintainable Templates

Brendan Loudermilk @bloudermilk

Developer, Philosophie

# Why?

Templates are frequently neglected. A lot of attention to models, controllers, service models, etc. Views are neglected by many backend coders.

# Unmaintable templates

Caused by:

* Markup repetition
* Logic in templates

## Markup repetition

Good designers repeat themselves. 

Good programmers don't.

Abstract interface components into partials.

## Logic in templates

Highly repetitive.

Painful to test.

Use helpers for repeated routines. Keep helpers *small*. E.g. if you want to mask credit card, just define it in a helper in 1 line.

Problem with helpers:

* Big projects end up with **many** helpers
* Difficult to organize
* Complex logic isn't well suited for them
* Don't feel right

## Decorator Pattern

Decorators attach additional responsibilities to an object dynamically. 

* Wraps a single object
* Transparent interface
* Forwards methods to original object

E.g. add presentation logic to models without affecting the model itself.

**Draper** gem. Helpful features:

* Access to view context
* Easily decorate collections
* Pretends to be decorated object (form_for and such)
* Easily decorate associations

# Complex views

Unique and/or complex UI behavior will quickly outgrow helpers.

## Presentation Model

Fully self contained class that contains all the data and behavior of the UI window, but without the controls used to render that UI. A view projects the state of the presentation model.

Learned from Javascript libraries like Backbone. Use of dumb templates.

Create a class for the object that has a method to_s that renders a partial.

Use Helpers to instantiate the view objects. 

Rails already uses this for forms. Use the form builder to create custom form builders so that we don't have to repeat all the divs and classes in HTML.

# Other tips

* Use i18n when you can
* Find gems to do this work for you. E.g. simple_form and table_cloth