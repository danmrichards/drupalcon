# Entity Storage, the Drupal 8 Way

## Drupal 7 vs Drupal 8

### Drupal 7

* Field swappable storage
* Field data can live in NoSQL storage, remote storage
* Each field configured independently
* Problematic for entity querying
* Supports only fields, properties are always in the SQL database

### Drupal 8

* Switch from field-based to entity-based storage
* Storage still swappable
* Supports also base fields (e.g. the node type)
* Entity querying works nicely
* Fields can no longer be shared between entity types
  * But you can have fields with the *same name* in different entity types
  * Still shareable between bundles

## Swappable storage

*"SQL is not dead, it just smells funny"*

* Swappble backend implys storage-agnostic code
* Contrib modules should not assume SQL storage
  * Leverage Entiy CRUD API
  * Or provide their own API (e.g. views)
* Custom modules can assume specific storage
  * Should **not** bypass the entity API
  * Use SQL-specific APIs if needed

## Entity Query API

* To query entity field data use the *Entity Query API*
  * Successor of D7 *EntityFieldQuery*
  * Improved syntax
  * Leverages swappable backend
* Supports expressing relationship between entity types
  * SQL backend transltes those in `JOIN`s
* Supports expressing aggregation queries
* Very powerful but not as expressive as SQL

## Legal SQL uses

* Always retrive identifiers via custom SQL queries
  * Do not retrive partial data
* Always load an entity before accessing field data
* Always save an entity to write field data to the storage
* Bypassing the Entity API means you are on your own
  * Unexpected behaviour, cache issues...
* At least encapsulate SQL specific code in a service

## Entity type definition

* An entity type definition (a plugin definition) describes the entity type to the system
* Content entities rely on field data
* Configuration entities use plain properties and are stored in configuration
* A definition has several properties

## Key definition properties

* The `handlers` section defines:
  * The `storage` handler that performs the CRUD operations
  * The `storage_schema` that managed the entity storage storage_schema
* The `revisionalable` and `translatable` properties

## Entity Field API

* D8 Entity Field API generalizes the D7 Field API
* Every piece of data attached to an entity is a field
* Base fields are shared among all available bundles (e.g. `nid`)
* Bundle fields may be attached only to certain bundles (e.g. `field_image`)
* Both are handled the same (e.g. Views or REST support)

## Field definitions

* Base field definitions live in code
  * Defind via `hook_entity_base_field_info()`
* Bundle field definitions typically live in configuration
  * Defined via `hook_entity_bundle_field_info()`
  * The field module allows creation of bundle field definitions based on its configuration
  * Can be defined in code too

## Field storage definitions

* Field storage definitions collect the information required to store a field
* Base field definitions are usually instances of the `BaseFieldDefinition` class
  * Both a field and a field storage definition

## Schema generation

* The storage handler is responsible for managing its own schema, if used
  * Schema is automatically generated based on entity type and field definition
* Schema is created on module installation and dropped on uninstallation

## Core SQL storage

* Generates table for base and bundle fields
  * Single base fields are stored in shared tables
  * Bundle fields and multiple cardinality base fields are stored in dedicated tables
* Supports 4 different table layouts depending on
  * Revisionablity
  * Translateability

## Table mapping API

* How to query shared tables?
  * Via Entity Query API (storage-agnostic)
  * Via the Table mapping API (SQL-specific)
* Table mapping API allows to write SQL queries in a layout-agnostic fashion
  * Used by views to implement its SQL backend
  * Currently core entity types only support the `DefaultTableMapping`

## Entity updates

* Leverage a dedicated API
* Entity definition update manager is able to detect any mismatch between the definitions and the actual schema
  * Allows to apply individual updates
  * Trigger events when an update is applied
  * Refused to proceeed if the change requires a data migration
* Typically applied via update functions
* A drush command is available `drush entup` to apply any pending entity update
  * Should be used only in development
  * Should **not** be used to get rid of the status report error in production

## The right way

### Define...

* Define any field needed to implement the business logic
* Field data will be loaded/stored automatically
* Automatic module integration via the Entity Field API
  * Revisionablity, translateability
  * Views, REST, rules
* Field definitions can opt out by marking themselves as having custom storage (not recommended)
  * Mainly used for computed fields

### ...and code!

* Core entity types provide interfaces making business logic explicity e.g. `NodeInterface::isSticky()`
  * Encapsulate with implementation
  * Better integrated with IDEs
  * Mark required data model
* Good practice to provide a wrapper for module provided fields

## A simple tracker

* Simple module (http://bit.ly/d8-esa-ex) to list:
  * Users that have created a node
  * Total amount of nodes
  * Title of most recent node
* Direct querying has poor performance -> denormalize
  * Add two fields to the user entity type
  * Update their values on CRUD events
