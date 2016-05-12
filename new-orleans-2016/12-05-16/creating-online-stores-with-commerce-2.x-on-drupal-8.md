# Creating Online Stores with Commerce 2.x on Drupal 8

## Lessons from Commerce 1.x

* Expected site builders to be experts on building a commerce workflow
* Scalability problems
* Prioritise UX

## Drupal Commerce 2.x

* Built from scratch on D8
* Alpha 4 on April 28, 2016
* Payment system currently finalizing development
* Beta coming soon with beta-to-beta upgrade paths
* Installation via composer (new site or existing site)

## Module Dependencies

* Inline Entity Form (Alpha 6 currently, beta pending on revision & translation support)
* Address (Beta 2 currently)
  * Address formats now editable in UI (edit fields, mandatory setting etc)
  * Zones - Allows rules based on given address settings
* Profile (Alpha 4 currently)
* State Machine (Beta 2 currently)
  * Order statuses as in 1.x
  * Workflow transitions between order statuses

## Commerce 2.x Features

### Currency management

Uses CLDR currency lists

### Price formatting

Locale aware (Language + Country) e.g German (Austria) vs German (Germany)

### Taxes

* Smart data model accommodating fluctuating tax rates
* Predefined tax rates for EU countries and Switzerland
* Tax resolvers with logic for major uses cases
* Integration with Avalara for sales tax automation

### Stores

* Support for multiple stores out of the box
* Per-store settings include contact email, default currency, supported countries etc
* Orders belong to one store, products one or more stores

### Products

* Product entities are now the actual product display page (not node based product displays)
* Product variations represent individual SKUs

### Product Attributes

* E.g. Product size. Rather than being a taxonomy vocabulary, new entity type
* Own UI
* Stronger data integrity (can't delete an attribute after use)
* Automated field creation

### Order and line item types

Seperate types of order (e.g. digital, phyiscal). Potential for different checkout flow per order type.

### Order editing

Step-by-step order creation wizard (choose products, choose customer, add payments, add discounts etc)

### Add to cart forms

* Preserves support for one or more attributes (defined at the product variation level) and exposed line item fields
* Managed via field display settings

### Shopping carts

* Multiple shopping carts per customer
* Customer support can build a cart, assign to customer, then customer can view that cart and checkout

### Improved checkout UX

* Default configurations and components will be more opinionated in Commerce 2.x to help developers create better experiences

### Payments

* Development ongoing in public branch on GitHub. Sprinting at DrupalCon
* Expanded API to improve DX
* Building tokenization by default into the core API
* Currently integrating Braintree and Authorize.Net as reference implementations
