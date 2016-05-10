# Handling Powerball Night with Patch

* Runs on 'decapitated' Drupal
* A back-end content platform and a front-end web platform
* Communicates via services
* Programatic cache clearing on content deployment

## Outgrowing One Load Balancer

* Traffic gets to a peak
* Throughput on the balancer is used up
* Bottleneck

## Paths to Even More Scale

* Option 1 - Round-robin DNS
  * More balanacers
  * Rotate the IPs
  * No guarantee as ISPs can cache the IP and never hit the rotation again
* Option 2 - Crazy hardware load balancers
  * Weeks to Deploy
  * Very expensive
* Option 3 - Go right to the varnish edge
  * Skip the balanacers
  * Send traffic direct to the edge nodes
  * No HTTPS for customer domains
* Option 4 - Add a CDN
  * User agents routed to geographically local CDN server
