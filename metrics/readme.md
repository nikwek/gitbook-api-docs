# Metrics

Metrics represent the individual time-series sent to the AppOptics service. Each measurement sent to AppOptics is associated with a Metric.

## Metric Properties

Parameter | Definition
--------- | ----------
type | Type of metric to create (gauge, counter, or composite).
display_name<br>`optional` | Name which will be used for the metric when viewing the Metrics website.
description<br>`optional` | Text that can be used to explain precisely what the gauge is measuring.
period<br>`optional` | Number of seconds that is the standard reporting period of the metric. Setting the period enables Metrics to detect abnormal interruptions in reporting and aids in analytics. For gauge metrics that have service-side aggregation enabled, this option will define the period that aggregation occurs on.
attributes<br>`optional` | The attributes hash configures specific components of a metric's visualization. A list of metric attributes can be found in the [Metric Attributes table](#attributes).
composite<br>`optional` | The composite definition. Only used when type is composite.

{% method %}
## Create a Metric

Metrics can be created without submitting a measurement value using a PUT to the `/metrics` endpoint.
Metrics are automatically created by POSTing a measurement for the first time. See [Create a Measurement](#create-a-measurement).

{% sample lang="bash" %}
```bash
curl \
-u $APPOPTICS_TOKEN: \
-H "Content-Type: application/json" \
-d '{
  "type": "gauge",
  "name": "cpu.percent.used",
  "period": 60,
  "attributes": {
    "summarize_function": "sum",
    "color": "#FFFFFF"
  },
  "tags": {
    "environment": "prod",
    "service": "api"
  }
}' \
-X PUT \
'https://api.appoptics.com/v1/metrics/cpu.percent.used'
```
{% sample lang="ruby" %}
```ruby
Not yet available
```

{% sample lang="python" %}
```python
Not yet available
```
{% endmethod %}

{% method %}
## Update a Metric

### HTTP Request

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
## Delete a Metric

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