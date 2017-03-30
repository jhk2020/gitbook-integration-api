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

{% sample lang="cs" %}
```cs

const string winePath = "api/rest/v001/store/STORE_ID/wine?inventory_fields=id,barcodes,external_id,wine&wine_fields=id,name,vintage,country&country_fields=id,name";
HttpResponseMessage wineResponce = httpClient.GetAsync(winePath).Result;

try
{
    wineResponce.EnsureSuccessStatusCode();
    string wineData = wineResponce.Content.ReadAsStringAsync().Result;
    Console.WriteLine(wineData);
}
catch (Exception)
{
    Console.WriteLine("Requst failed");
}

```
{% endmethod %}


See [API reference](/endpoints.md#list-wine-inventory) for more details.

## Add product to store
POST request to [/api/rest/v001/store/STORE_ID/wine
](/endpoints.md#list-wine-inventory
) or [/api/rest/v001/store/STORE_ID/drink](/endpoints.md#list-drink-inventory
) endpoint will create a new inventory item, wine_id or drink_id parameter is required. Usually you get wine_id or drink_id through full text search across Tipsi database. Other required parameters - barcodes (can be an empty list, though) and external id (item ID in your database). Params should be formatted as JSON dictionary.

{% method %}
The sample will create a new inventory item with assigned drink id 6755 and empty barcodes list. Barcodes can be empty, but the parameter is required.
{% sample lang="postman" %}
![](/assets/add-product.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/drink'
params = {'drink_id': 6755, "in_stock": 17, "barcodes": [], "external_id": 10007}
result = session.post(url, params=params).json()
```

{% sample lang="cs" %}
```cs
const string CreateInventoryItemPath = @"api/rest/v001/store/STORE_ID/wine";

// Make sure the wine_id (drink_id) exists.
HttpResponseMessage createInventoryItemResponce = httpClient.PostAsync(CreateInventoryItemPath, new StringContent("{\"wine_id\": 653842, \"in_stock\": 17, \"barcodes\": [], \"external_id\": 10007}", Encoding.UTF8, ApplicationJSONMediaType)).Result;

try
{
    createInventoryItemResponce.EnsureSuccessStatusCode();
    string createdInventoryItemData = createInventoryItemResponce.Content.ReadAsStringAsync().Result;
    Console.WriteLine(createdInventoryItemData);
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
```

{% endmethod %}


See [API reference](/endpoints.md#create-wine-inventory) for more details.

## Upload image

Use POST request to `/api/rest/v001/store/STORE_ID/image_upload` to upload images for further usage in task creation endpoint.

*Endpoint requires tasks creation option enabled for your store, so contact Tipsi if you have errors.*

{% method %}

{% sample lang="python" %}
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/image_upload'
with open('image.png', 'rb') as file_obj:
    params = {'image': file_obj}
    result = session.post(url, files=params).json()
{% endmethod %}


## Create task for unmatched inventory item

You can create task by sending POST to `/api/rest/v001/store/STORE_ID/wine/INVENTORY_ID/create_task` or `/api/rest/v001/store/STORE_ID/drink/INVENTORY_ID/create_task`.

*Endpoint requires tasks creation option enabled for your store, so contact Tipsi if you have errors.*

{% method %}

{% sample lang="python" %}
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/wine/INVENTORY_ID/create_task'
data = {'front_image': front_image_url,
        'back_image': back_image_url,
        'vintage': '2015'}
result = session.post(url, data=data).json()

{% endmethod %}
