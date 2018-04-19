{% method %}

## Update a Metric

#### HTTP Request

`PUT https://api.appoptics.com/v1/metrics`

Set the `period` and `display_min` for metrics `cpu`, `servers` and `reqs`:

{% sample lang="bash" %}
```bash
curl \
  -u $APPOPTICS_TOKEN: \
  -d 'names%5B%5D=cpu&names%5B%5D=servers&names%5B%5D=reqs&period=60&display_min=0' \
  -X PUT \
  'https://api.appoptics.com/v1/metrics'
```

{% sample lang="ruby" %}
```ruby
require "appoptics/metrics"
AppOptics::Metrics.authenticate <token>
AppOptics::Metrics.update_metrics names: ["cpu", "servers", "reqs"], period: 60, display_min: 0
```

{% sample lang="python" %}
```python
import librato
api = librato.connect(<user>, <token>)
for name in ['cpu', 'servers', 'reqs']:
  gauge = api.get(name)
  attrs['period'] = '60'
  attrs['display_min'] = '0'
  api.update(name, attributes=attrs)
```
{% endmethod %}

{% method %}

## Display units short

Set the `display_units_short` for all metrics that end with `.time`:

{% sample lang="bash" %}
```bash
curl \
  -u $APPOPTICS_TOKEN: \
  -d 'names=*.time&display_units_short=ms' \
  -X PUT \
  'https://api.appoptics.com/v1/metrics'
```

{% sample lang="ruby" %}
```ruby
require "appoptics/metrics"
AppOptics::Metrics.authenticate <token>
AppOptics::Metrics.update_metrics names: ["*.time"] , display_units_short: "ms"
```
{% sample lang="python" %}
```python
Not yet available
```

{% endmethod %}