# Drupal 8, where did the code go? From info hook to plugin

## Background

* Dependency injection container (DIC)
  * Container object that contains instances of stateless services (current user, url generator etc)
* New routing system
  * Names instead of paths
  * Route name is just a machine name connected to a path and callbacks to provide title, content access
* Namespaced classes like `Drupal\search\Plugin\Block\SearchBlock`

## Plugins

* Encapsulates re-usable functionality inside a class that implements 1 or more interfaces
* Plugins combine what in D7 was an info hook and implementation hooks e.g. `hook_search_info` and `hook_search_execute`
* Evolved from ctools and views plugins but quite different discovery mechanisms

## Plugin Manager and IDs

* Every plugin type has a manager - registered as a service and used to find and instantiate the plugin instances
* Each plugin has an ID - may be in it's definition or generated as a derivative
* For a given plugin ID one single class will be used for all plugin instances using that plugin ID
* A plugin instance is specified by a combination of the plugin ID and the config values (potentially coming from a `ConfigEntity`)

## Hooks Still Have Their Place

* Most plugin managers invoke an `_alter` hook so the modules can add to or alter the plugins definitions
* E.g. `hook_block_alter` allows you to alter the block plugin definitions
* Info hooks that return a data array, without code and logic, were not candidates to become plugins but may have become YAML
* Others like `hook_cron` or `hook_entity_access` are still present

## Plugin Discovery

* Basically the same as invoking an info hook
* Discovery gives you an array of plugin definitions (an array of keys and values)
* Process fills in defaults, such as a `provider` which is the name of the module providing the plugin
* Discovery can make derivatives (many from one) like `FieldUiLocalTask` - one tab per bundle

## Plugin Discovery & Config in Core

* YAML based
* Annotation, some config but no config entity
* Annotation and config
* Not a pure plugin but uses annotation discovery e.g. `Entity`

## A Drupal 8 Module

* `mymodule.info` becomes `mymodule.info.yml`
* `mymodule.module` file not required
* Only a few hooks go in `mymodule.module`. Most code lives in classes
* Tabs (LocalTask) added via `mymodule.links.tasks.yml` file
  * Config options and defaults are on the `LocalTasksManager` class
* Routes added via `mymodule.routing.yml`

## Blocks as Plugins

* Each custom block is defined in code as a class
* When the admin places a block in a region, a config object is created to track that setting
* The config object is a `ConfigEntity`. An abstraction on top of CMI. Makes it convenient to list, load etc using entity functions
* Drupal can easily list the active block instances
* Blocks implement the `BlockPluginInterface` class
* PSR-4 - Namespace of Block class has to map directly to a file path.
  * `\Drupal\mymodule\Plugin\Block\MyBlock` maps to `modules/mymodule/src/Plugin/Block/MyBlock.php`
  * Class name and path match up under `src`

## Block Discovery

* Each plugin type must be in the expected class namespace
* Most core plugins have a custom annoation class
* The annotation class provides documentation on the possible keys for annoation and fills in defaults

## Creating Your Own Plugins

* You want to upgrade your module to Drupal 8 and it defined an info hook or had a ctools plugin type
* Use annotation based discovery by default
* It keeps the meta-data together with the class and is suited for typical plugin types where the actual class (code) is different for each plugin
* YAML discovery is good for a case like local tasks, where the majority use a common class, but few will implement a different one.
