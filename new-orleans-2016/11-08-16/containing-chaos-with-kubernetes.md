# Containing Chaos with Kubernetes

## Why Kubernetes

* Scenario: Many Dockerfiles and containers needed to power application (Frontend/services container and DB container)
* Splitting the containers down, as is best practice, to make them more ephemeral
* Many containers on same machine = single point of failure

## What is Kubernetes

* Container orchestration system
* Open source
* Started by Google
* Contributed to by others (Redhat, Docker etc)

## Cattle not Pets

* Pet
  * Has a name
  * Unique
  * Personal attention
  * If it gets ill you make it better
* Cattle
  * Has a number
  * If it gets ill you make a burger (or a jacket)

## Components

### Pods

* Atomic component of Kubernetes
* Made from one or more containers
* Share
  * IP address
  * Namespace
* Ok to have just one container
* Examples
  * Webserver & file sync
  * All web available services
  * Converting an all-in-one box

### Containers

* Subatomic particles of Kubernetes
* Dockerfiles just like you are used to

### Controllers

* Handle turning current state into desired state
* Example
  * Replication Controllers

### Replica Set

* Everything that Replication Controllers do
  * Can do set-based selector
* Recent change so a lot of the docs will refer to Replication Controllers but you can use Replica Sets

### Deployments

* An improvement over previous rolling updates
* Allow for easy updates to application pieces

### Services

* Define a set of pods that work together for a common purpose
* Gets a virtual IP address
* Used for exposing an application to non Kubernetes clients

### Labels & Selectors

* Metadata for Objects
* Select sections of your infrastructure

### Networking

* Pod IPs are routable
  * Docker default is private IP
* Pods can reach each other without NAT
