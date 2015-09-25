# Drupal 8: Plugins
## *A visual and technical deep dive*

## What is a Plugin?

Heliors' definition: *A discreet class that executes an operation withing the context of a given scope, as a means to extend Drupal's functionality*

Kris' definition: *A discoverable class that implements a particular interface which adds or extends a pluggable subsystem*

* Discoverable
* Object Oriented
* Interface Driven
* Swappable
* Drupal not required

## Why Plugins

Drupal actually is kinda unique

* Unprecedented configurability
* Abscence of similar code
* Other CMS don't expose as much
* Frameworks expect it to be hardcoded

## Benefits of Plugins

* Definition & implementation are co-located
  * Instead of looking at an implemention of a hook (e.g. `module_menu`) and looking at `hook_menu` in another file
  * Implementation in class code, definition in annotation
* Plugins are object oriented
  * No need to know names of all related hooks (e.g. `hook_block_view`, `hook_block_info`)
  * Implements a standard interface
* Plugins are extensible
  * Inherit from base class
  * Inherit from other plugins
* Plugins are lazy loaded by default
* Common pattern (*learn once, use everywhere*)

## Foundational Concepts

* Autoloading
  * PSR-0 - `\Drupal\Core => "core/lib/Drupal/Core"` `\Drupal\Component => "core/lib/Drupal/Component"`
  * PSR-4 - `\Drupal\Block => "core/modules/block/src"`
* Dependency Injection
* Service Containers
* Annotations
  * Config in code comments

## Annotations

* Annotations are **not code**!
* yaml, json, {insert_serializer} are **not code**!
* Annotations have more in common with serialization
* Data not behaviour
