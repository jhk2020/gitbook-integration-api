# Quick Start

Our API is RESTful, so any programming language will support interaction, but the document will provide examples for curl, Python and C# (coming soon).
Before calling private APIs, you should create an authenticated session. It’s cookie-based, so library needs to save cookies and pass them back with continuous calls, in most programming languages it will be done automatically, so nothing complicated.

{% method %}
{% sample lang="postman" %}
![](/assets/login.png)

{% sample lang="python" %}
```python
import requests

login_url = 'https://integration-test.gettipsi.com/api/rest/v001/login'

session = requests.Session()
response = session.post(login_url, {'username': 'USERNAME', 'password': 'PASSWORD'})

if response.status_code == 200:
    print('Logged in successfully')
else:
    print('Login failed')        
```
{% endmethod %}

If response status code is 200, you logged in successfully. Once it happened, any further call will contain session ID in cookies header.
{% method %}
In the given example, store id is 19771
{% sample lang="postman" %}
![](/assets/list-wine-inventory.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/19771/wine'
params = {'inventory_fields': 'id,barcodes,wine',
         'wine_fields': 'id,name,vintage'}
         
products = session.get(url, params).json()
```
{% endmethod %}

Once you get your code working on test server, change it to production and go live!