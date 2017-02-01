# Quick Start

Our API is RESTful, so any programming language will support interaction, but the document will provide examples for curl, Python and C# (coming soon).
Before calling private APIs, you should create an authenticated session. It’s cookie-based, so library needs to save cookies and pass them back with continuous calls, in most programming languages it will be done automatically, so nothing complicated.

{% method %}
{% sample lang="bash" %}
```bash
curl htts://integration-test.gettipsi.com/api/rest/v001/login
```

{% sample lang="python" %}
```python

import requests

response = requests.post('htts://integration-test.gettipsi.com/api/rest/v001/login
', {'username': 'USERNAME', 'password': 'PASSWORD'})

assert response.status_code == 200, 'Authentication failed'
```
{% endmethod %}

If response status code is 200, you logged in successfully. Once it happened, any further call will contain session ID in cookies header, please see example below:

* EXAMPLE *

Once you get your code working on test server, change it to production and go live!