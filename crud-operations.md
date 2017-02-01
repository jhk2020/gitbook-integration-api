# CRUD operations

## List all store products

GET request to [/api/rest/v001/store/STORE_ID/wine#list-wine-inventory
](/endpoints.md) or [/api/rest/v001/store/STORE_ID/drink](/endpoints.md#list-wine-inventory
) endpoint will list all the available products. The endpoints are paginated - they will return a thousand results per page. You can modify page size by passing page_size parameter, but values larger than a thousand will be ignored.
By the way, all GET APIs are lazy - by default they will only return object id. Fields should be requested explicitly as GET parameter - a comma separated list of fields for each struct.
The example below requests inventory id, barcodes and wine fields, and nested fields of wine - wine id, name and vintage:

https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/wine?inventory_fields=id,barcodes,wine&wine_fields=id,name,vintage

Check the full structs description [here](/struts.md).

## Add product to store
POST request to /wine or /drink endpoint will create a new inventory item, wine_id or drink_id parameter is required. Usually you get wine_id or drink_id through full text search across Tipsi database. Other required parameters - barcodes (can be an empty list, though) and external id (item ID in your database). Params should be formatted as JSON dictionary.

## Delete product from store
DELETE request to /wine/<INVENTORY ID>  or /drink/<INVENTORY ID> 

## Update product meta information
PATCH request to /wine/<INVENTORY ID> or /drink/<INVENTORY ID> will update object information.  It will allow to change only inventory level information, nested (wine or drink structs) information will be ignored.