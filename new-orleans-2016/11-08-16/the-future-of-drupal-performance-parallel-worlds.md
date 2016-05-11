# The Future of Drupal Performance - Parallel Worlds

We load:

* Service container
* All the classes

We run:

* Session intialization
* Authorization
* Routing

We always start from zero (even though we cache a lot)

Not necessarily bad, just how the CGI model works. It means we do potentially unecessary work.

## This is how we fix it

* Avoid doing unecessary work
* Bring back performance of D7 page cache to D8
  * Its possible - https://drupal.org/node/2501989
* Bring dynamic page cache to 'index.php' level as well
* Cache the cache contexts per session
* Retrieve page with placeholders
* If all the placeholders are cached, composer the page and be done

## Both Profit

* Small sites: Faster performance
* Enterprise sites: Easier varnish ESI

> Using the exact same mechanism

All sites get faster response times for cached fragments

We can do this *almost* today! The only thing we need is pre-container middleware support

## Vision for D9

* Remove bootstrapping
* Remove service container
* BigPipe the main content as soon as its ready

### We want

* Transparent change to developer/themer
* Site just gets faster

## Render Tree

* Create a 'promise' and push to a queue
* Build dependency chain
* Promises will wait for other unresolved promises
* A queue worker processes the queue => Async I/O
  * While we wait for I/O we can start rendering an unrelated fragment
  * PHP7 in the process of implementing async I/O as well. Maybe PHP 7.4
  * Could do it in ReactPHP or another async framework

## Rendering

* Why not push the rendering to an independent render farm?
* We need to know the cache context. We do!
* Pre generate content
  * Heuristic pre-rendering of content. e.g. Most popular blocks/pages etc
* Re generate content and serving of stale content
* Workers in a rendering farm

## Workers Everywhere

* Requires long running processes
* Paradigm shift
* Already in place for some queue runners
* Services need to be stateless
* In `index.php` you can then clear the static cache and create a new kernel
  * Classes are already loaded. HHVM does this.
* Potential race condition with static caches and long running processes
