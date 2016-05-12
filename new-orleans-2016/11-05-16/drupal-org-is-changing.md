# Drupal.org is Changing: Content Restructure, Issue Credits, Composer and more

## Content Restructure

* Refresh of documentation
* UI refresh
* Blogs

## Issue Credits and Marketplace

### Issue Credits

* A method for giving credit to organisations that contribute code to open source
* Determine format for commit credit for individuals/organisations/customers
* Attribute organisation as employer or customer when participating in queues
* Credits are given by maintainer and counted when the issue closes
* Last 90 days of issue credits are displayed on profiles
  * Shows consistent contribution
  * Allows smaller organisations that contribute alot to get recognised

### Giving Feedback

* Improve contribution statistics on user and organisation profiles
* Updated organisation content type to better reflect types or organisation in Drupal ecosystem

## Composer Facade

* Allows for site construction using modules/themes from Drupal.org
* Provides metadata for composer to pull in modules/themes

### Why Build it Ourselves?

* Data model - differences between packages on packagist.org and a Drupal project
* Comprehensive support for all D7 and D8 modules
* Semantic versioning - Drupal version numbering (e.g. 7.x-1.0) doesn't map well to packagist.org semantic versioning
  * Facade translates Drupal version numbers: 7.x-3.4-beta2 becomes 3.4.0-beta2
  * Unstable releases abandoned. Same as alpha.
* Usage data
* Project discovery - one place to discover modules
* Distributed infrastructure - pulling from packagist.org in some territories is very slow
* Documentation - https://www.drupal.org/node/2718229

### How to Use

Update `composer.json` with new repository:

```
{
    "repositories": [
        {
            "type": "composer",
            "url":  "https://packages.drupal.org/<drupal version>"
        }
    ]
}
```

To add a module to a project:

`$ composer require drupal/<modulename> <version>`

Search packages on drupal.org

`composer search <modulename>`

### What's missing

* Substree split of drupal core
* Subtree split of drupal components
* Distribution support
* Patch support
* DrupalCI usage
* Deprecated versions in composer.json
* Dev versions complications
