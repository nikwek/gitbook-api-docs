{% method %}
## Create a Measurement

Create a new measurement `my.custom.metric` with the tag `region: "us-east-1", az: "a"`

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

{% sample lang="Ruby" %}
```ruby
require "appoptics/metrics"
AppOptics::Metrics.authenticate 'token'

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

{% sample lang="Python" %}
```python
import librato
api = librato.connect('email', 'token')

api.submit("my.custom.metric", 65, tags={'region': 'us-east-1', 'az': 'a'})
```
{% endmethod %}