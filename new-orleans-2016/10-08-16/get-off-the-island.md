# Get off the Island - But build bridges back!

* Complex modules with many custom classes, entities etc can become tightly coupled to Drupal itself
* Even with seperation of concerns it is easy for tighy-coupling to creep in e.g. using `variable_get` in a PHP class
* Hard to isolate and test classes

## Abstracted Libraries and components

* Backend logic can be placed into a framework-agnostic PHP library
* Bring back into Drupal with a wrapper module; can load the PHP library
* Don't just build a new library. Check if something exists already!

## Reasons to do it

* Frustration dealing with Drupalisms rather than solving the problem at hand
* D7 and D8 modules end up having similar code repackaged
* Cultural as much as engineering issue

## Building a PHP Library

* PHP-Fig (http://www.php-fig.org)
* Coding standards
* Style guide
* Autoloading standard
* League of Extraordinary Packages - Skeleton package

## Developer Experience

* Functionality evolved around Drupal
* If you keep using functionality in a certain way - consider abstracting into a library

## Benefits

* Seperate domain logic completely
* Makes functionality available to a wider audience
* Force yourself to consider the domain problem
* Enjoy writing tests!

## Drupal 7

* Composer Manager (https://drupal.org/project/composer_manager)
* Use a `composer.json` file and Composer manager runs composer to bring in libraries

## Drupal 8

Composer in core yo!

## How to use Libaries

* Just like any PHP library
* May be special cases such as a Drupl-aware db storage controller

## When should I write a library?

* The solution is interesting to a wider community
* More than a single class to include
* You want your module to be easier to upgrade
* Functionality is not Drupal specific
