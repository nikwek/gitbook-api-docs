# Introduction

Welcome to the official reference for the AppOptics Application Programming Interface (API). Detailed documentation for authentication and each individual API call can be accessed through the menu.

This guide includes examples using cURL and the [Ruby client](https://github.com/appoptics/appoptics-api-ruby).


## Quick Start

This example covers submitting and retrieving measurements from a specific metric. View the [Metrics section](#metrics) for more information on metric measurements and metadata.

{% method %}
### Submitting measurements

This example shows how to submit a measurement for the metric `my.custom.metric`.

{% sample lang="bash" %}
```bash
curl \
  -u $APPOPTICS_TOKEN: \
  -H "Content-Type: application/json" \
  -d '{
    "tags": {
      "region": "us-east-1",
      "az": "a"
    },
    "measurements": [
      {
        "name": "my.custom.metric",
        "value": 65
      }
    ]
  }' \
  -X POST \
  https://api.appoptics.com/v1/measurements
```

{% sample lang="ruby" %}
```ruby
require "appoptics/metrics"
AppOptics::Metrics.authenticate 'api_key'

queue = AppOptics::Metrics::Queue.new
queue.add "my.custom.metric" {
  value: 65,
  tags: {
    region: 'us-east-1',
    az: 'a'
  }
}
queue.submit
```

{% sample lang="python" %}
```python
import librato
api = librato.connect('email', 'token')

api.submit("my.custom.metric", 65, tags={'region': 'us-east-1', 'az': 'a'})
```
{% endmethod %}

{% method %}
## Retrieving measurements

URL parameters can be used to refine the query. For example to retrieve the last 5 minutes worth of measurements from the metric `my.custom.metric` at a resolution of 60 seconds. This will return measurement data along with metric metadata.

{% sample lang="bash" %}
```bash
curl \
  -i \
  -u $APPOPTICS_TOKEN: \
  -X GET \
  'https://api.appoptics.com/v1/measurements/my.custom.metric?duration=300&resolution=60'
```
{% sample lang="ruby" %}
```ruby
require "appoptics/metrics"
AppOptics::Metrics.authenticate 'api_key'
query = {
  duration: 300,
  resolution: 60
}
metric = AppOptics::Metrics.get_series "my.custom.metric", query
puts metric[0]["measurements"]
```
{% sample lang="python" %}
```python
import librato

api = librato.connect('user', 'token')

metric = api.get_tagged(
  "my.custom.metrics",
  resolution=60,
  duration=300
)
print(metric['series'])
```
{% endmethod %}


