# Endpoints

## Login Endpoint

It's possible to pass params both as JSON or POST params

| URL | [https://DOMAIN/api/rest/v001/login](https://DOMAIN/api/rest/v001/login) |
| --- | --- |
| Method | POST |
| Format | JSON |
| Params | username, password |

## Sync Inventory

| URL | [https://DOMAIN/api/rest/v001/store/STORE](https://DOMAIN/api/rest/v001/store/STORE) ID/ext/sync |
| --- | --- |
| Method | PATCH |
| Format | JSON |
| Request Content | JSON encoded array list of [inventory structs](/structs.md#base-inventory-struct). Each struct has to contain "external\_id" param, which will be used to lookup related item in inventory. Unnecessary params can be omitted, in that case they will not be updated. By the way, as "external\_id" is used to lookup inventory, inventory Tipsi "id" param is prohibited here as the request will look ambiguously, thus trying to use it will cause error with HTTP respone 400. |

## Sync Inventory With Clearing

| URL | [https://DOMAIN/api/rest/v001/store/STORE](https://DOMAIN/api/rest/v001/store/STORE) ID/ext/sync\_clear |
| --- | --- |
| Method | PATCH |
| Format | JSON |

Same, as [Sync Inventory Endpoint](#sync-inventory), except will clear inventory not listed in the batch. It's a safe method as it will just mark in\_stock parameter to 0. For real inventory deletion DELETE method should be used upon each inventory item.

## List Wine Inventory

| URL | [https://DOMAIN/api/rest/v001/store/STORE](https://DOMAIN/api/rest/v001/store/STORE) ID/wine |
| --- | --- |
| Method | GET |
| GET Params | List of fields for each struct [inventory structs](/structs.md#base-inventory-struct). If not specified which fields to fetch for a given struct, it will contain only "id" parameter. Param name, related to a given struct, listed below struct tables |

```
https://DOMAIN.gettipsi.com/api/rest/v001/store/STORE ID/wine?wine_fields=id,winery,region&inventory_fields=id,wine&winery_fields=id,name&region_fields=id,name,description,image_url
```

## List Drink Inventory

| URL | [https://DOMAIN/api/rest/v001/store/STORE](https://DOMAIN/api/rest/v001/store/STORE) ID/drink |
| --- | --- |
| Method | GET |
| GET Params | List of fields for each struct [inventory structs](/structs.md#base-inventory-struct), similar to wine list. |

## Create Wine Inventory

| URL | [https://DOMAIN/api/rest/v001/store/STORE](https://DOMAIN/api/rest/v001/store/STORE) ID/wine |
| --- | --- |
| Method | POST |
| Format | JSON |
| POST Params | JSON without nested fields [inventory structs](/structs.md#base-inventory-struct). |

Minimal parameters for wine: `barcodes` and `external_id`. If `wine_id` is not passed, it will create item in unmatched state. Such item doesn't have linked wine, but it's useful when wine should be manually matched by Tipsi team \(see [Label Processing Tasks Guide](/create-tasks.md)\).

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

| URL | [https://DOMAIN/api/rest/v001/store/STORE](https://DOMAIN/api/rest/v001/store/STORE) ID/drink |
| --- | --- |
| Method | POST |
| Format | JSON |
| POST Params | JSON without nested fields [inventory structs](/structs.md#base-inventory-struct), similar to wine list. |

Minimal parameters for wine: `barcodes` and `external_id`. If `drink_id` is not passed, it will create item in unmatched state. Please see [Label Processing Tasks Guide](/create-tasks.md).

## List Food

| URL | [https://DOMAIN/api/rest/v001/food](https://DOMAIN/api/rest/v001/food) |
| --- | --- |
| Method | GET |
| GET Params | "food\_fields" - list of fields for food struct [food structs](/structs.md#food-struct). |

## List Wine Styles

| URL | [https://DOMAIN/api/rest/v001/wine\_style](https://DOMAIN/api/rest/v001/wine_style) |
| --- | --- |
| Method | GET |
| GET Params | "style\_fields" - list of fields for wine style struct [wine style structs](/structs.md#wine-style-struct). |

## Get Product By Barcode

| URL | [https://DOMAIN/api/rest/v001/store/STORE](https://DOMAIN/api/rest/v001/store/STORE) ID/barcode/BARCODE |
| --- | --- |
| Method | GET |
| GET Params | List of fields for each struct [inventory structs](/structs.md#base-inventory-struct). If not specified which fields to fetch for a given struct, it will contain only "id" parameter. Param name, related to a given struct, listed below struct tables. |

### Example:

```
https://DOMAIN.gettipsi.com/api/rest/v001/store/STORE ID/barcode/BARCODE?wine_fields=id,winery,region&inventory_fields=id,wine&winery_fields=id,name&region_fields=id,name,description,image_url
```

## Full Text Search

| URL | [https://DOMAIN/api/rest/v001/fts/](https://DOMAIN/api/rest/v001/fts/) |
| --- | --- |
| Method | GET |
| GET Params | query - search query, [fts struct fields](/structs.md#fts-struct) |

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

## Upload image

| URL | /api/rest/v001/store/STORE\_ID/image\_upload |
| --- | --- |
| Method | POST |
| Format | "multipart/form-data" |
| POST Params | Image file encoded as standard "multipart/form-data" to `image` field |

## Create task

| WINE URL | /api/rest/v001/store/STORE\_ID/{wine,drink}/TIPSI\_INVENTORY\_ID/create\_task |
| --- | --- |
| Method | POST |
| Format | JSON |
| POST Params | front\_image, back\_image \(optional\), vintage \(optional\) |

Returns [inventory structs](/structs.md#base-inventory-struct) with drink\_id and wine\_id.

