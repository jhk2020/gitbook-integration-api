# Quick Start

Before calling private APIs, you should create an authenticated session. It’s cookie-based, so library needs to save cookies and pass them back with continuous calls, in most programming languages it will be done automatically, so nothing complicated.

* EXAMPLE *

If response status code is 200, you logged in successfully. Once it happened, any further call will contain session ID in cookies header, please see example below:

* EXAMPLE *

Once you get your code working on test server, change it to production and go live!