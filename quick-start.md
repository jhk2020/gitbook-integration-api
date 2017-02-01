    # Quick Start

Our API is RESTful, so any programming language will support interaction, but the document will provide examples for curl, Python and C# (coming soon).
Before calling private APIs, you should create an authenticated session. It’s cookie-based, so library needs to save cookies and pass them back with continuous calls, in most programming languages it will be done automatically, so nothing complicated.

{% method %}
{% sample lang="bash" %}
The call below will perform POST to login endpoint and create a cookie.txt file:
```bash
echo '{"username": "USERNAME", "password": "PASSWORD"}' > params.json
curl -c cookie.txt -vX POST htts://integration-test.gettipsi.com/api/rest/v001/login -d @params.json
echo 'logged in successfully'
```

{% sample lang="python" %}
```python
import requests

def login():
    login_url = 'htts://integration-test.gettipsi.com/api/rest/v001/login'
    response = requests.post(login_url, {'username': 'USERNAME', 'password': 'PASSWORD'})
    
    assert response.status_code == 200, 'Authentication failed'
    
login()
print('logged in successfully')
```
{% endmethod %}

If response status code is 200, you logged in successfully. Once it happened, any further call will contain session ID in cookies header, please see example below:

{% method %}
{% sample lang="bash" %}
Will use previously created cookie.txt file and request a list of wines
```bash
curl -b cookie.txt https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/wine?inventory_fields=id,barcodes,wine&wine_fields=id,name,vintage
```

{% sample lang="python" %}
```python
def fetch_wines():
    url = 'https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/wine'
    response = requests.get(url,
        {'inventory_fields': 'id,barcodes,wine',
        'wine_fields': 'id,name,vintage'})
    return response.json()

login()
fetch_wines()
```
{% endmethod %}

Once you get your code working on test server, change it to production and go live!