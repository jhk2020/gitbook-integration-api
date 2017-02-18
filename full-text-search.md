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
// Use the same httpClient, which has been created while login
const string queryMerlotPath = "api/rest/v001/fts?query=merlot&fts_fields=wine,drink&wine_fields=id,name,vintage&drink_fields=id,name";
HttpResponseMessage queryMerlotResponce = httpClient.GetAsync(queryMerlotPath).Result;

try
{
    queryMerlotResponce.EnsureSuccessStatusCode();
    string searchResult = queryMerlotResponce.Content.ReadAsStringAsync().Result;
    Console.WriteLine(searchResult);
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
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
// Use the same httpClient, which has been created while login
const string queryAbsolutePath = "api/rest/v001/fts?query=absolute&fts_fields=wine,drink&wine_fields=id,name,vintage&drink_fields=id,name";
HttpResponseMessage queryAbsoluteResponce = httpClient.GetAsync(queryAbsolutePath).Result;

try
{
    queryAbsoluteResponce.EnsureSuccessStatusCode();
    string searchResult = queryAbsoluteResponce.Content.ReadAsStringAsync().Result;
    Console.WriteLine(searchResult);
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
```

{% endmethod %}


See [API reference](/endpoints.md#full-text-search) for more details.