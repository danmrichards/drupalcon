# Configuration Management in Drupal 8

## Why?

* Deployment
* A predictable and robust system

## What is configuration?

* It is **not** state (e.g. time of last cron run)
* It is **not** cache
  * Too expensive to use as a cache
  * Needs to be rebuilt
* It is **not** content
* It is everything that is left
  * Any information to synchronise from development to production

## Types of configuration

* Simple configuration
  * There can be only one instance
  * e.g. Site name
* Configuration entities
  * There can be none, one or many
  * e.g. Node types, fields, vocabularies, filter formats, views...

## Using configuration

* Reading
  * Simple - `$site_name = \Drupal::config('system.site')->get('name');`
  * Configuration entities - `$node_type = NodeType::load('article');`
* Creating
  * Typically during installation
    * Simple - `module_name/config/install/module_name.settings.yml`
    * Optional - `module_name/config/optional/views.view.settings.yml`
  * Through the API - `$config->set('key', 'value');`

## Configuration entity dependencies

* Modules
* Themes
* Configuration entities
* Content
* Implicit dependency on the module that declares it

## How are the dependencies defined?

* From the name e.g. **node**.type depends on the node module
* From their own data
* 3rd party settings. Other modules can change the settings.
  * `::setThirdPartySetting($module, $key, $value);`
  * `::getThirdPartySetting($module, $key, $default = NULL);`

## Other types of dependencies

* Content
  * e.g. Content block module depends on content in the block
* Enforced
  * e.g. A module that defines a new node type. The new node type config depends on that module.
