# Making Drupal Fly
## The Fastest Drupal Ever is Here!

## Drupal 8

* Utilises BigPipe to send quick content (text, cached items) first. Slow content last.
* Page renders faster. Slow content filled in as/when ready.
* Similar technology, SmallPipe, works without JS.

## Make the web fast

* Great user experience, pages load fast for 1 user
* Great user experience, pages load fast for [n] concurrent users
* Time to first byte + Asset loading + Rendering + JS exec time == minimal

## Optimization

* Remove as much work as possible from the critical path
* ACD = Avoid, Cache, Defer

## Cache invalidation

* Drupal 7 clears whole page cache when an element of the page changes
* Drupal 8 invalidates instantaneously
  * Everything declares what it varies by
  * Allows caching authenticated user content securely

## D8 makes it simple

* Does all the caching logic internally
* If you give Drupal information then it can be smarter about is decisions
* Formalizes things in a "language" to make these things fast
  * Potentially can be backported to D7

## Dependencies

* D7 did not track dependencies
* e.g. `drupal_add_css()`, `drupal_add_js()`
  * Global state: impossible to cache
  * `#attached` asset libraries solves that
* e.g. `url()` output depends on
  * `<front>` config
  * HTTPS config
  * Clean URL config
  * Current site in multisite
  * ...
  * Impossible to ~~cache~~ ***invalidate***
* To make it easier:
  * `Renderer:addCacheableDependency($build, $dependency);`

## Correct invalidation in D8

* Cache tags (data dependencies)
* Cache contexts (context dependencies)
* Cache max-age (time dependencies)
* Cacheability bubbled during rendering!

## Thought process

1. I'm rendering something. That means I need to think about cacheability?
2. Is this smething thats expensive to render, and therefore is worth caching?
  * If yes cache keys
3. Does the representation of the thing I'm rendering vary per combination of permissions, per URL, per interface...
  * If yes, cache context
  * `$build['#cache']['contexts'][] = 'user.permissions';`
  * `$build['#cache']['contexts'][] = 'url';`
4. What causes the representation of the thing i'm rendering to become outdated
  * If yes, cache tags.
5. When does the representation of the thing I'm rendering become outdated?
  * If yes, cache max-age
  * `$build['#cache']['max-age'][] = Cache::PERMANENT;`

## Cacheability metadata

* All relevant objects provide cacheability metadata

## Page cacheability

* Pages are static and dynamic
* Dynamic content slows the page down
  * Gets slower with more content and more users. More unique data which is uncacheable.
* D8 solves this with placeholders (in core).
  * Removes all dynamic content from page, placeholders there instead. Static content remains, as it is cacheable.

## Lazy builder

```
$build['complex_thing'] = [
  '#lazy_builder' => ['callback', [
    'arg1',
    'arg2',
  ]],
];
```

* Effective successor to `hook_pre_render()`
* Builds a render array and returns it
* Output must solely depend on the input (arguments)
  * Able to render in isolation
  * This is what enables BigPipe


## Pitfalls

* Don't forget to add cache tags!
* Uncacheable? Don't forget to set max-age to zero
