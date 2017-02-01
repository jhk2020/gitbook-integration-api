# Endpoints
## Login Endpoint
It's possible to pass params both as JSON or POST params


| URL | https://DOMAIN/api/rest/v001/login |
| --- | --- |
| Method | POST |
| Params | username, password |


## Sync Inventory
| URL | https://DOMAIN/api/rest/v001/store/STORE ID/barcode/sync |
| --- | --- |
| Method | PATCH |
| Request Content | JSON encoded array list of [inventory structs](#base-inventory-struct). Each struct has to contain "barcode" param, which will be used to lookup related item in inventory. Unnecessary params can be omitted, in that case they will not be updated. By the way, as barcode is used to lookup inventory, inventory "id" param is prohibited here due to the request will be ambiguous, thus trying to use it will cause error with HTTP respone 400. |


## Sync Inventory With Clearing
| URL | https://DOMAIN/api/rest/v001/store/STORE ID/barcode/sync_clear
| --- | --- |
| Method | PATCH |

Same, as [Sync Inventory Endpoint](#sync-inventory), except will clear inventory not listed in the batch. It's a safe method as it will just mark in_stock parameter to 0. For real inventory deletion DELETE method should be used upon each inventory item.

## List Wine Inventory
| URL | https://DOMAIN/api/rest/v001/store/STORE ID/wine |
| --- | --- |
| Method | GET |
| GET Params | List of fields for each struct [inventory structs](#base-inventory-struct). If not specified which fields to fetch for a given struct, it will contain only "id" parameter. Param name, related to a given struct, listed below struct tables |

```
https://DOMAIN.gettipsi.com/api/rest/v001/store/STORE ID/wine?wine_fields=id,winery,region&inventory_fields=id,wine&winery_fields=id,name&region_fields=id,name,description,image_url
```

## List Drink Inventory
| URL | https://DOMAIN/api/rest/v001/store/STORE ID/drink |
| --- | --- |
| Method | GET |
| GET Params | List of fields for each struct [inventory structs](#base-inventory-struct), similar to wine list. |


## Create Wine Inventory
| URL | https://DOMAIN/api/rest/v001/store/STORE ID/wine |
| --- | --- |
| Method | POST |
| POST Params | JSON without nested fields [inventory structs](#base-inventory-struct).|

Minimal parameters for wine: `barcodes`, `external_id`, `wine_id`

```javascript
// POST /api/rest/v001/store/38/wine
// Data: {"external_id": 3001, "barcodes": ["wine-123"], "wine_id": 311}
// Response code: 201
({
     "abv": null,
     "barcodes": [
         "wine-123"
     ],
     "external_id": 3001,
     "id": 421,
     "in_stock": null,
     "price": null,
     "proof": null,
     "special_price": null,
     "special_price_amount": 0,
     "special_price_on": false,
     "status": "match_complete",
     "unit_size": null
 })
```

## Create Drink Inventory
| URL | https://DOMAIN/api/rest/v001/store/STORE ID/drink |
| --- | --- |
| Method | POST |
| POST Params | JSON without nested fields [inventory structs](#base-inventory-struct), similar to wine list. |

Minimal parameters for wine: `barcodes`, `external_id`, `drink_id`


## List Food
| URL | https://DOMAIN/api/rest/v001/food |
| --- | --- |
| Method | GET |
| GET Params | "food_fields" - list of fields for food struct [food structs](#food-struct). |


## List Wine Styles
| URL | https://DOMAIN/api/rest/v001/wine_style |
| --- | --- |
| Method | GET |
| GET Params | "style_fields" - list of fields for wine style struct [wine style structs](#wine-style-struct). |


## Get Product By Barcode
| URL | https://DOMAIN/api/rest/v001/store/STORE ID/barcode/BARCODE |
| --- | --- |
| Method | GET |
| GET Params | List of fields for each struct [inventory structs](#base-inventory-struct). If not specified which fields to fetch for a given struct, it will contain only "id" parameter. Param name, related to a given struct, listed below struct tables. |

### Example:
```
https://DOMAIN.gettipsi.com/api/rest/v001/store/STORE ID/barcode/BARCODE?wine_fields=id,winery,region&inventory_fields=id,wine&winery_fields=id,name&region_fields=id,name,description,image_url
```

## Full Text Search
| URL | https://DOMAIN/api/rest/v001/fts/ |
| --- | --- |
| Method | GET |
| GET Params | query - search query, [fts struct fields](#fts-struct) |

### Example

```javascript
// Search drinks and wines
// GET /api/rest/v001/fts/?pro_rating_fields=shortcut%2Crating&amp;wine_fields=id%2Cpro_rating%2Cwinery&amp;fts_fields=rank%2Cwine%2Cdrink&amp;query=caymus&amp;winery_fields=id%2Cname
// Data: {"pro_rating_fields": "shortcut,rating", "wine_fields": "id,pro_rating,winery", "fts_fields": "rank,wine,drink", "query": "caymus", "winery_fields": "id,name"}
// Response code: 200
({
     "count": 2,
     "next": null,
     "previous": null,
     "results": [
         {
             "drink": null,
             "rank": "0.638323",
             "wine": {
                 "id": 19,
                 "pro_rating": [],
                 "winery": {
                     "id": 18,
                     "name": "Caymus"
                 }
             }
         },
         {
             "drink": {
                 "id": 20
             },
             "rank": "0.0607927",
             "wine": null
         }
     ]
 }

// Only wines
// /api/rest/v001/fts/?pro_rating_fields=shortcut%2Crating&amp;wine_fields=id%2Cpro_rating%2Cwinery&amp;query=caymus&amp;fts_fields=rank%2Cwine&amp;winery_fields=id%2Cname
// Data: {"pro_rating_fields": "shortcut,rating", "wine_fields": "id,pro_rating,winery", "query": "caymus", "fts_fields": "rank,wine", "winery_fields": "id,name"}
// Response code: 200

 {
     "count": 1,
     "next": null,
     "previous": null,
     "results": [
         {
             "rank": "0.638323",
             "wine": {
                 "id": 19,
                 "pro_rating": [],
                 "winery": {
                     "id": 18,
                     "name": "Caymus"
                 }
             }
         }
     ]
 }

// Only drinks
// /api/rest/v001/fts/?pro_rating_fields=shortcut%2Crating&amp;wine_fields=id%2Cpro_rating%2Cwinery&amp;query=whiskey&amp;fts_fields=rank%2Cdrink&amp;winery_fields=id%2Cname
// Data: {"pro_rating_fields": "shortcut,rating", "wine_fields": "id,pro_rating,winery", "query": "whiskey", "fts_fields": "rank,drink", "winery_fields": "id,name"}
// Response code: 200

({
     "count": 1,
     "next": null,
     "previous": null,
     "results": [
         {
             "drink": {
                 "id": 20
             },
             "rank": "0.0607927"
         }
     ]
 }
```


 