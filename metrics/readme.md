# Metrics

Metrics represent the individual time-series sent to the AppOptics service. Each measurement sent to AppOptics is associated with a Metric.

#### Metric Properties

Parameter | Definition
--------- | ----------
type | Type of metric to create (gauge, counter, or composite).
display_name<br>`optional` | Name which will be used for the metric when viewing the Metrics website.
description<br>`optional` | Text that can be used to explain precisely what the gauge is measuring.
period<br>`optional` | Number of seconds that is the standard reporting period of the metric. Setting the period enables Metrics to detect abnormal interruptions in reporting and aids in analytics. For gauge metrics that have service-side aggregation enabled, this option will define the period that aggregation occurs on.
attributes<br>`optional` | The attributes hash configures specific components of a metric's visualization. A list of metric attributes can be found in the [Metric Attributes table](#attributes).
composite<br>`optional` | The composite definition. Only used when type is composite.