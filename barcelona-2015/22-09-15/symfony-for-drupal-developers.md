# Symfony for Drupal Developers

## Symfony 2

* Tier 1 PHP framework
* Loosely coupled
* Helped inspire PHP 5.3 era revolution
* Incubator for Composer

## You

* Know Drupal 7
* Kind of know Drupal 8
* Want to move down-stack
  * Less UI, more framework driven, pure apps
* "*Do I need to learn Symfony to use Drupal 8?*"
  * No!
  * D8 uses mostly decoupled Symfony2 components ~30%
  * D8, Laravel, Silex, Symfony are *siblings*

## Learn Symfony

* RTFM (http://docs.symfony.org)

## Who is it for?

* Drupal
  * Content strategists
  * Site administrators
  * Content editors
  * "Build stuff without writing code"
* Symfony
  * Professional developers
  * Bespoke applications
  * "Make writing code easier"

## Configuration

* No UI
* Multiple config files (usually YAML)
* Compiled config/container

## Bundles

* Enable extensions by hacking code
* "Bundles" have configuration...files
* "Admin" bundles e.g Sonata Admin Bundle
* FOSUserBundle (Drupal-ish user management)

## Developing

* Most dev tools are CLI
* Code scaffolding
* Dev/Prod toggle, by code
* Prod needs force rebuild

## Architecture

Functions?

Nope!

### Services

* All meaningful logic in Services
* Services are stateless objects
* D8 does this
* Event listeners are just glue code

### Unopinionated configuration

* PHP, XML, YAML, Annotations all supported
* Please pick one!
* YAML is reccomended, D8 will be using it
* "The Drupal way" is stricter than "The Symfony way"

Drupal is metaprogramming via the UI
Symfony is metaprogramming via YAML

## Theming (really templating)

* There is only one template per request
* No, really!
* Twig inheritance
* Templates can be extended `{% extends 'base.html.twig' %}`
* Define blocks in the template, content gets injected. `{% block body %}{% endblock %}`

## Extending

* Do hack the core!
  * "*Say whaaaat!*"
* Need to edit core files to enable bundles (`app/AppKernel.php`)

## Project structure

* `app` (Config files, kernel files, autoload files)
  * `cache`
  * `config`
  * `logs`
  * `Resources` (css, js, images)
  * `AppKernel.php`
  * ...
* `bin` (CLI binary etc)
* `src` (Custom code bundles)
  * `AppBundle`
    * `Controller`
      * `DefaultController.php`
    * `Tests`
      * `Controller`
        * `DefaultControllerTest.php`
    * `AppBundle.php`
* `vendor` (Don't edit stuff in here!)
* `web`
  * `bundles` (Contrib stuff in here)
  * `app.php` (Edit this. Prod main file.)
  * `app_dev.php` (Edit this. Dev main file.)
  * ...
* `composer.json`

## Development Workflow

* Drupal
  * Push buttons
  * Write code
  * Click "Clear cache"
  * `git commit`
  * Profit!
* Symfony
 * Write code
 * Run in dev mode
 * Clear prod cache (several cmds)
 * Build deploy snapshot (Run `composer update`, compile config etc. Don't deploy new code to production then build)
 * Profit!

## Same kernel, different patterns

* Drupal always uses the View event
* Symfony discourages it

## Paths and routing

* Drupal 8
  * `$module.routing.yml`, or event
  * No path nesting
  * Fixed paths with aliasing
* Symfony
  * `routing.[yml|xml|php]`, or annotation
  * Path nesting
  * Slugs

## Storing Data

* Drupal
  * Entities
  * State API
  * Configuration API
* Symfony
  * Doctrine

## Doctrine

* Stand-alone PHP project
* Simple objects only
* 1:1 field->property
* MongoDB requires ODM add-on

## Drupal Entities vs Doctrine

* Drupal
  * Configuration driven
  * Fields
  * Multi-value
  * Rich data types
* Doctrine
  * All custom classes
  * Simple properties
  * No multi-value
  * Simple data types

## Doctrine gotchas

* Primitive data only
* SQL and Mongo are different APIs
  * CLI tools are different
  * Event names are different
* Different event listeners from Symfony
* Very primitive file handling

## But still many similarities

* Services (Symfony, D8, Laravel etc)
* Still the same kernel (D8 just uses the Symfony kernel as a vendor)
* Hooks ~ Listeners
* But also tagged services
* Twig (template inheritance is a bit different)
