# Dependency Injection in Drupal 8

## What is Dependency Injection?

Injecting the dependency into your class

## Types of Dependency Injection

* Constructor
  * Pass dependency as paramater of the `__construct` method of the class
  * Mandatory dependency
* Setter
  * Pass into a setter method in the class
  * Optional dependency
  * Cannot control dependency lifetime in the class
* Property
  * Similar to setter
  * Pass into a public property of the class.

## Benefits

* Cleaner and modular code
* Reusable and flexible
* Abstracted
* Testable

## DI in a Framework

Dependency injection == Dependency injection Container (DIC) == IOC Container == Service Container

### What is a Service Container?

Creates a map of dependencies that classes need and handle loading/unloading

### Symfony DI

* Services keys are strings e.g. 'some_service'
* Service definitions specify which class to instantiate, the arguments to pass and additional methods to call on the object after instantiation
* Configure in PHP, XML or YAML
  * Can be 'compiled' down to PHP

## Drupal 8 DI

2 ways to use core services:

* Service location: Used for procedural code e.g. `Drupal::service('some_service')`
* Service container: Used for OO code e.g. `$container->get('some_service')`

### How and Where?

* Core services defined in `core/core.services.yml`
* Custom services defined in `mymodule/mymodule.services.yml`
* Custom classes live in `mymodule/lib/Drupal/mymodule`
* List of core services can be found at https://api.drupal.org/api/drupal/services
