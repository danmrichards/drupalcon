# Applied Progressive Decoupling With Javascript

## Decoupled Drupal

* Process of employing a different front end from Drupals own
* Speaks to other front ends via RESTful APis
* Not a new concept

### Rendering client side

* SPA depend on a universal JS framework
* Angular, Ember, React etc
* Native apps have their own systems

### Rewards

* Seperation of concerns
* Content syndication (write once, publish everywhere)

### Risks

* Additional point of failure
* No XSS protection or input sanitization
* No in place editing
* No layout/display management
* No previewable content workflow
* No modules affecting the front end
* No system notifcations
* No BigPipe

### When

A site powering 1 or more other sites or apps

## Weather.com before Drupal

* 144 origin servers.
* 50 million page views per day. 50% going to origin servers.
* Forecasts for 2.9 million locations
* Hundreds of dynamic weather maps.

### Performance and caching

* Split page into wrapper and panes
* Same wrapper from origin to everyone
* Edge computations using ESI
* Client side rendering using Angular

### Front-end Developers

* JS developers want to write JS
* Don't want to learn Drupal APis
* Keep up with JS ecosystem

### Editorial Team

* Want to create pages
* Work independently
* Create page layouts

### Presentation Framework

* Mechanism for putting components on pages
* Supports Angular, PHP & static templates
* Modules served by Drupal or ESI

### Why Panels?

* Variant and selection rules
* Reusable and exportable rules
* Context
* Drag-and-drop UI

## Framework-agnostic Progressive Decoupling

### Goals

* Give JS developers flexibility
* Keep guard rails in place

### Drupal 8

* Decoupled Blocks module in development
* Built on top of Blocks
* Already supports Angular 2 and React. More coming

### Developers can creae JS component Modules

* Easy to use for JS and Drupal devs
* Single bootstrap of Framework
* Site builders can configure components in UI
* Developers can require a context and pass to client
* Add config fields into .info.yml file
  * Shown during block placement and passed to components via `drupalSettings`

### JS Frameworks

* Angular 2, React
* Angnostic

### Components can be contextually aware

* Tightly couple component functionality to Drupals existing system of entities

### Static Prototypes and Style Guides

* Organizations can build library of components
* Site builder can assemble components to create a working prototype
* 'Living style guide'
