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

## CDN Selection

* Ready for top 100 levels of traffic
* Drupal compatibility
* Apex domain (example.com not www.example.com) HTTPS support
* 24-hour turnaround
* Cache tagging and invalidation support

## Deployment Process

1. Prepare CDN IPs to terminate HTTPS
2. Create rules to properly handle Drupal
  a. Pass-through for active sessions
  b. Keying on HTTP vs HTTPS
3. Create test domain that routes through CDN
4. Validate anonymous, authenticated and custom functionality
5. Reduce production DNS TTL and wait out old TTL
6. Update productiob DNS to go through CDN
