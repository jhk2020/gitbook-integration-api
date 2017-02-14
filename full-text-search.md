# Full text search

Full text search provides ability to search products by names across Tipsi database. Once you found the product, it can be added to inventory with endpoints described [here](/crud-operations.md).

{% method %}
Searching product by "Merlot" keyword
{% sample lang="postman" %}
![](/assets/fts-merlot.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/fts'
params = {'query': 'merlot',
    'fts_fields': 'wine,drink',
    'wine_fields': 'id,name,vintage',
    'drink_fields': 'id,name'}
result = session.get(url, params=params).json()
```

{% sample lang="cs" %}
```cs
// coming soon
```

{% endmethod %}


{% method %}
Searching product by "Absolut" keyword
{% sample lang="postman" %}
![](/assets/fts-absolut.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/fts'
params = {'query': 'absolut',
    'fts_fields': 'wine,drink',
    'wine_fields': 'id,name,vintage',
    'drink_fields': 'id,name'}
result = session.get(url, params=params).json()
```

{% sample lang="cs" %}
```cs
// coming soon
```

{% endmethod %}


See [API reference](/endpoints.md#full-text-search) for more details.