# Behat, MinkJS, PhantomJS: Test all the Things

Gherkin -> Behat -> FeatureContext -> MinkJS/PhantomJS

## BDD

* Behaviour Driven Development
* Natural language written tests

## Why Behat?

* Clear defined behaviour
* Behaviour script written in *Gherkin*. Actual tests themselves still need to be written in PHP

## Gherkin

* Each behaviour test prefixed with *Scenario*
* *Given*, *When*, *Then* = Steps of behaviour. Also can use *And*
* Can use *Scenario Outline* to reduce repetition. Accept parameters to certain values.

### Steps

* Automatically add steps by accepting context
* Results - *Pending*, *Failed*, *Skipped*, *Redundant*, *Undefined*, *Succesfull*

### Hooks

* Trigger functionality before/after/during scenarios
* Tag function with `@BeforeScenario`. Suffix with scenario names `@BeforeScenario @database @orm`, `@BeforeScenario @database&&@fixtures`

### Context

* Feature = How application behaves
* Context = How to test the application
* `FeatureContext` class
  * Annotation defines the related Gherkin, function name does not matter. `@When I do something with :argument`
  * Has to be a discoverable class
  * Class is initialised before each test is run
* Can have multiple contexts. Defined in `behat.yml`

## Writing Tests

* Write functions in context class. Write annotation to match Gherkin
* Test anything you like

## MinkJS

* A context with a lot of built in functionality:
  * Clicking links
  * Fill fields
* Saves time when writing common tests

## Fixtures & Mocking

* Mock API responses to ensure test consistency
* Problematic to test PHP and JS in the same tests
* Can be solved by using PHP VCR. Records HTTP interactions and replays them in the test suite

### PHP VCR

* Much faster tests
* Do not have to hit any API, runs from test data (HTTP interactions) stored on disk
* Avoids rate limits etc
* No need to create mocks or fixtures.
* Useful for other things like offline programming

## PhantomJS

* Headless browser
* To use with Gherkin it runs as a ghost; as a selenium driver
* Can save screenshots during a test. Displays exact output of the headless browser at that time

### Screenshot comparison

* Compare image code between tests
* If they are different then the test has most likely failed
* Not ideal as will be affected by design changes - colour, padding etc

## Other use cases

* Integration testing
* Run tests on deploy hooks
* Test legacy applications

## Wrapup

* Still not mature for CSS and image comparison
* Behat is Open Source
* Extension available for Drupal containing a lot of Drupal specific scenarios and contexts
