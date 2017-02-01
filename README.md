# Introduction

Tipsi integration API implemented as REST and provides ability to interact with your retail data programmatically.
Supported operations described below:

* Create, read, update, delete operations:
  * List all products of the store
  * Adding product to store
  * Deleting product from store
  * Updating product meta information
* Read, update, delete operations using external ids
* Additional features:
  * Full text search across Tipsi database
  * POS synchronization

Our production integration server domain is **integration.gettipsi.com**, we also provide a separate sandbox for experiments - **integration-test.gettipsi.com**, on that domain you can play with API without worries to accidentally break anything.
