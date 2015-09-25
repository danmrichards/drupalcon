# Decoupling Drupal Modules into PHP Libraries

## Background

* Abstract functionality out of modules into PHP libraries
* Framework agnostic
* Build Drupal modules on top of these libraries

## Why?

* Re-examine your problem
* Get additional exposure
* Validate your implementation
* Get development/maintenance help
* Allow for backports

## The (not so) hidden cost: time

* Takes a lot longer to write an agnostic library that something tied to a specific platform
* Evaluating edge cases
* Needs to feel familiar to developers used to certain frameworks

## Anatomy of a library

* Data model
  * Interfaces
  * Default class
  * Traits
  * Collections
  * Repository
* Services
* Tests

## Tips & tricks

* Translatable strings
  * Abstract variations out into enumerated classes
  * Allow possiblity to get default value or all values
* Pluggable implementations

## Know when to stop

* Don't attempt to abstract some functionality into the library that can be wildly different across frameworks
* e.g. Form building in Drupal/Symfony/Laravel is completely different
* A library should be something that saves others a decent amount of time. If it can be reinvented in an hour, then don't bother

## Spreading the drop

* Drupal has lots of cool functionality that would be great to spread to the php community
* e.g. migrate, views, D8 render cache
