# Symfony2: The Journey from the Request to Response

## Philosophy

* Symfony is a HTTP framework not an MVC framework
* HTTP request -> Front Controller -> HttpKernel -> Routing Component -> Controller -> Model/View -> HttpFoundation response

### Components Involved

* HttpFoundation
  * Abstraciton of the request and the response
* HttpKernel
  * Turns the request into a response

### Routing Component

* Maps a URL to a set of parameters
* In D8 `module_name.routing.yml`

### Controller

* A callable responsible for communication with the model and view layers
* In Symfony it must return a `Response` object
* In D8 it can return an array

### Event Dispatcher Component

* Dispatch an Event
* Listen/Subscribe to an event

## Event

Is an object which carries all the needed data into retrieve into each listener

### Listeners

* Any valid PHP callable like a function name, an instance method, a static method or a closure
* Event Listener != Event Subscriber
* Event Subscriber
  * Have a defined list of events and functions to call on those events (defined by `getSubcribedEvents()`)
  * Need to create a dispatcher and add the subscriber (`addSubscriber()`)
* Event Listener
  * Class that implements a function e.g. `onKernelRequest(GetResponseEvent $event)` (on is a standard prefix for event listener functions)
* Events need to be dispatched

### In Drupal

* Create services to dispatch events

### HttpKernel Events

* `kernel.request`
* `kernel.controller`
* `kernel.view`
* `kernel.response`
* `kernel.terminate`
* `kernel.finish_request`
* `kernel.exception`

## Service Container

* Manages instantiation of service
* Makes sure there is only one of each service

## Services

* PHP object
* Perform global task
* Does not have any state
* In D8 `module_name.services.yml`
* Can be tagged to have different behaviour (e.g. `event_subscriber`)

## Parameters

* Global configuration
