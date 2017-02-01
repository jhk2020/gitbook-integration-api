# POS synchronization

POS sync designed for batch inventory synchronization on daily/hourly basic between Tipsi and customer retail store.
Sync can be enabled for next purposes:
* To update existing products information - prices, availability and etc. It's done as a single batch, without necessity to PATCH each product separately.
* To create unmatched products in TODO list in MIM tool. In fact, batch sync works like SQL UPSERT command - it will create all the missing products (product availability defined by external id) and update existing ones.
* To have all the products using external ids - in that case processed wine/drink information can be easily pulled back to customer programmatically.

There are two kind of sync commands - sync and sync_clear. They are almost the same:
* [sync](/endpoints.md#sync-inventory) performs UPSERT upon passed products
* [sync_clear](/endpoints.md#sync-inventory-with-clearing) performs UPSERT and marking all the unpassed products as out of stock (without deleting them).

