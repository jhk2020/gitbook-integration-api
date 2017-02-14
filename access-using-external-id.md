# Access products using external ids

Using external id is convenient, when you have existing list of products and want to sync them to Tipsi, and later retrieve processed data back to your system. Fetching, updating and deleting product will use same product URL, only methods will differ.

```
https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/ext/EXTERNAL_ID
```

## Fetch product

Perform GET request to product URL https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/ext/EXTERNAL_ID

{% method %}
{% sample lang="postman" %}
![](/assets/get-product-by-ext-id.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/19771/ext/10007'
params = {'inventory_fields': 'id,external_id,barcodes,wine,drink',
    'wine_fields': 'id,name,vintage',
    'drink_fields': 'id,name'}
result = session.get(url, params=params).json()
```
{% endmethod %}


## Update product meta

Perform PATCH request to product URL https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/ext/EXTERNAL_ID
Only passed parameters will be modified, as conventionally PATCH performs partial updates, omitted parameters will remain unchanged. Please take into account that it will change only inventory level fields (in_stock, price and etc), all nested wine or drink attributes will remain unchanged even if you try to change them. Params should be formatted as JSON.

Please see inventory level struct [here](/structs.md#base-inventory-struct).

{% method %}
{% sample lang="postman" %}
![](/assets/update-product-by-ext-id.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/19771/ext/10007'
params = {'in_stock': 33}
result = session.patch(url, params=params).json()
```
{% endmethod %}

## Delete product

Perform DELETE request to product URL https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/ext/EXTERNAL_ID

{% method %}
{% sample lang="postman" %}
![](/assets/delete-product-by-ext-id.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/19771/ext/10007'
result = session.delete(url).json()
```
{% endmethod %}

For successful deletion 204 "No Content" HTTP status expected. 