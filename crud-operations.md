# List or create operations

## List all store products

GET request to [/api/rest/v001/store/STORE_ID/wine
](/endpoints.md#list-wine-inventory
) or [/api/rest/v001/store/STORE_ID/drink](/endpoints.md#list-drink-inventory
) endpoint will list all the available products. The endpoints are paginated - they will return a thousand results per page. You can modify page size by passing page_size parameter, but values larger than a thousand will be ignored.
By the way, all GET APIs are lazy - by default they will only return object id. Fields should be requested explicitly as GET parameter - a comma separated list of fields for each struct, see the full structs description [here](/struts.md).

{% method %}
The example below requests wine inventory and nested fields (ids, barcodes, vintage and etc):
{% sample lang="postman" %}
![](/assets/list-wine-inventory.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/wine'
params = {'inventory_fields': 'id,barcodes,external_id,wine',
    'wine_fields': 'id,name,vintage,country',
    'country_fields': 'id,name'}
result = session.get(url, params=params).json()
```
{% endmethod %}


See [API reference](/endpoints.md#list-wine-inventory) for more details.

## Add product to store
POST request to [/api/rest/v001/store/STORE_ID/wine
](/endpoints.md#list-wine-inventory
) or [/api/rest/v001/store/STORE_ID/drink](/endpoints.md#list-drink-inventory
) endpoint will create a new inventory item, wine_id or drink_id parameter is required. Usually you get wine_id or drink_id through full text search across Tipsi database. Other required parameters - barcodes (can be an empty list, though) and external id (item ID in your database). Params should be formatted as JSON dictionary.

See [API reference](/endpoints.md#create-wine-inventory) for more details.


