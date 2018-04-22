
## Authentication

{% method %}
The API requires [HTTP basic
authentication](http://en.wikipedia.org/wiki/Basic_access_authentication)
for every request. All requests must be sent over HTTPS.

Authentication is accomplished with a unique *API token*.
THe API token can be found [on your account page](https://my.appoptics.com/organization/tokens).


{% sample lang="bash" %}
```bash
curl -u 75AFDB82: https://api.appoptics.com/v1/metrics
```
{% sample lang="ruby" %}
```ruby
require "appoptics/metrics"
AppOptics::Metrics.authenticate 75AFDB82
```
{% sample lang="python" %}
```python
import librato
api = librato.connect('email', 'token')
```
{% endmethod %}

### URL Encoding

Because basic auth is used, the `token` will be provided as the username and the password field will be left empty. For example:

```
https://token:@api.appoptics.com/v1/metrics
```

You can also include your API token in the URL with most clients.
