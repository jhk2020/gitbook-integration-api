# Structs
## Base Inventory Struct
| Field Name | Description |
| --- | --- |
| id | Inventory id, int |
| price | Item price, float |
| barcodes | List of barcodes (list of strings) - each barcode has to be unique per retail store, otherwise backend will report validation error |
| proof | Alcohol proof, float |
| abv | Alcohol by value, float |
| unit_size | Unit size in free form text ("150ML" or "1.5 L"), str |
| in_stock | Amount of items in stock (regular price), int |
| updated | Last inventory update date and time |
| pos_item_name | Product name in POS system |

Param name: **inventory_fields**


## FTS Struct

| Field Name | Description |
| --- | --- |
| rank | Matched item search rank, int |
| drink | Related drink, [struct](#drink-struct) |
| wine | Related wine, [struct](#wine-struct) |


## Wine Inventory Struct
Same as [Base Inventory Struct](#base-inventory-struct), +additional params:

| Field Name | Description |
| --- | --- |
| wine | Related wine, [struct](#wine-struct) |
| status | Matching status, str - it can be match_pending, in_progress or match_complete |

Param name: **inventory_fields**

## Drink Inventory Struct
Same as [Base Inventory Struct](#base-inventory-struct), +additional params:

| Field Name | Description |
| --- | --- |
| drink | Related drink, [struct](#drink-struct) |
| status | Matching status, str - it can be match_pending, in_progress or match_complete |

Param name: **inventory_fields**


## Wine Struct
| Field Name | Description |
| --- | --- |
| id | Tipsi wine id, int |
| name | Wine name, str |
| vintage | Wine vintage, str. Year (.e.g. "2003", "2005") or "NV" for non vintage |
| winery | [struct](#winery-struct) |
| vineyard | [struct](#vineyard-struct) |
| designation | [struct](#designation-struct) |
| varietals | list of [structs](#varietal-struct) |
| country | [struct](#country-struct) |
| region | [struct](#region-struct) |
| sub_regions | list of [structs](#sub-region-struct) |
| type | regular, fortified, sparkling, dessert or offdry |
| color | Color density, int. Values from 1 to 3 - White, 4 - Rose, from 5 to 7 - Red |
| label_url | Url of wine label image, str |
| wine_url | URL to wine producer or re-seller |
| pro_rating | list of [structs](#pro-rating-struct) |
| style_scoring | empty list (deprecated) |
| food_scoring | empty list (deprecated) |
| winemakers_note | A note from wine producer |


Param name: **wine_fields**

## Winery Struct
| Field Name | Description |
| --- | --- |
| id | Winery id, int |
| name | Winery name, str |

Param name: **winery_fields**

## Vineyard Struct
| Field Name | Description |
| --- | --- |
| id | Vineyard id, int |
| name | name, str |
| description | description, str |

Param name: **vineyard_fields**

## Designation Struct
| Field Name | Description |
| --- | --- |
| id | Designation id, int |
| name | Designation name, str |
| description | Designation description, str |

Param name: **designation_fields**

## Varietal Struct
| Field Name | Description |
| --- | --- |
| id | Varietal id, int |
| name | Varietal name, str |
| description | Varietal description, str |

Param name: **varietal_fields**

## Country Struct
| Field Name | Description |
| --- | --- |
| id | Country id, int |
| name | Country name, str |
| description | Country description, str |
| image_url | Map image url |

Param name: **country_fields**

## Region Struct
| Field Name | Description |
| --- | --- |
| id | Region id, int |
| name | Region name, str |
| description | Region description, str |
| image_url | Map image url |

Param name: **region_fields**

## Sub Region Struct
| Field Name | Description |
| --- | --- |
| id | Sub Region id, int |
| name | Sub Region name, str |
| description | Sub Region description, str |
| image_url | Map image url |

Param name: **sub_region_fields**

## Pro Rating Struct
| Field Name | Description |
| --- | --- |
| name | Rating long name, str |
| shortcut | shortcut, str |
| rating | Rating value, int: 0..100 |
| rating_description | Description of the given rating value |

Param name: **pro_rating_fields**

## Drink Struct

| Field Name | Description |
| --- | --- |
| id | Drink id, int |
| name | Drink name, str |
| description | Drink description, str |
| drink_type | beer, spirits, cocktail or other |
| producer | Drink producer, [struct](#drink-producer-struct) |
| country | Country, [struct](#country-struct) |
| label_url | Drink label url |

Param name: **drink_fields**

## Drink Producer Struct

| Field Name | Description |
| --- | --- |
| id | Drink producer id, int |
| name | Drink name, str |
| description | Producer description, str |

Param name: **producer_fields**
