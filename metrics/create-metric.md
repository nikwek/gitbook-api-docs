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

{% endmethod %}