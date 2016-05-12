# How Puppet Labs Runs on AWS

* Amazon EC2 offers a T2 server which allows burst capacity based on CPU 'credits'

## Shared Storage Options

* S3 + Drupal module - Best option
* FUSE mounted S3
* NFS mounted S3 - Traditional choice
* AWS hosted S3 - Still in beta

## Don't Run a MySQL Server in AWS

* Not worth the operational overhead!
* RDS - AWS hosted MySQL
  * Best cost-benefit ratio. Can be HA.
* Aurora - AWS hosted MySQL-compatible database
  * Scales well

## What about Varnish & Memcache

* Proper MySQL tuning made them uncessary
* Drupal caching good enough for their use case
