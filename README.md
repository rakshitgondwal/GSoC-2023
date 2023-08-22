<div align="center">
<img src="assets/gsoc.png" height="auto" width="600" />
<br />
<img src="assets/keptn.png" height= "auto" width="400" />
<br />
<h1>Keptn</h1>
<h3>
Timeframe for Metrics
</h3>
</div>

## Table of Contents

- [Introduction](#introduction)
- [Project team](#project-team)
- [Contacts](#contacts)
- [Work Summary](#work-summary)
  - [Support for Interval](#support-for-interval)
  - [Support for Step and Aggregation](#support-for-range-and-aggregation)
- [Challenges](#challenges)
- [Acknowledgments](#acknowledgments)
- [Project Resources](#project-resources)
- [References](#references)

## Introduction

Currently, the Metrics Controller in the Keptn Lifecycle Toolkit only allows querying a
single value per metric. This project will enable users to define timeframes for metrics
and get standardized aggregated results for the given timeframe. The addition of time
frames for metrics would provide developers with a lot of flexibility when analyzing
their application’s performance as they would be able to easily switch between different
timeframes to get a better understanding of how their application is performing. This can
be achieved by modifying the structure of the Metric CRD by adding certain fields and then
modifying the APIs of our Metric providers to support these newly added fields. The metrics
controller would be able to query metrics over a timeframe and then return raw values from
the providers which can then be passed to the aggregation functions to calculate the desired
aggregated value. These values would be updated in the Metric CRD.

## Project team


- Contributor: Rakshit Gondwal - [GitHub](https://github.com/rakshitgondwal/) | [LinkedIn](https://www.linkedin.com/in/rakshit-gondwal-911223230/) | [Twitter](https://twitter.com/RakshitGondwal)
- Mentors:
  - Florian Bacher - [GitHub](https://github.com/bacherfl/) | [LinkedIn](https://www.linkedin.com/in/florian-bacher-6a58ab79/) | [Twitter](https://twitter.com/bacherfl)
  - Thomas Schuetz - [GitHub](https://github.com/thschue/) | [LinkedIn](https://www.linkedin.com/in/thschue/) | [Twitter](https://twitter.com/ThSchue)

## Contacts

- Slack: `#help`, `#help-contributing` on [Keptn Slack](https://keptn.sh/community/#slack)

## Project Details

The addition of the feature to define the timeframe in metrics would help developers in
many ways such as developers would be able to retrieve aggregated values for a
specific time frame. This would help to analyze the performance of their application or
service more easily. This can help in improving the monitoring capabilities too. By
retrieving aggregated values, developers would be able to save a lot of time while
analyzing the metrics. The addition of time frames for metrics would provide developers
with a lot of flexibility when analyzing their application’s performance. They would be
able to easily switch between different timeframes to get a better understanding of how
their application is performing at different times of the day or week. 

Features this project includes: 
* Define an Interval for which you want your metric to be queried.
* Define a Step which would act as a threshold in the time interval.
* Define an aggregation function which you want to be applied on the data recieved from the SLI provider.
* Define how many values you want that should be stored in the KeptnMetric.

## Work Summary

The two major milestones of this project were:
1. Support for Interval
2. Support for Step and Aggregation

### Support for Interval

- To query metrics over a timeframe, we introduced a new `range.interval` field in the KeptnMetric which is defined as the duration of the time interval for the data query. This field would accept a string value, which has to be a duration such as "1m", "1h" etc.
- To verify if the value inputed by the user is correct or not, we used https://pkg.go.dev/time#ParseDuration to parse the the field's value with the help of a validating webhook.
- This feature required updating the APIs of the SLI providers such as Prometheus, Dynatrace and Datadog.

**PRs for this particular milestone:**
1. feat: add support for timeframe in KeptnMetric [#1471](https://github.com/keptn/lifecycle-toolkit/pull/1471)
2. feat: update Prometheus API to query metrics over a range [#1587](https://github.com/keptn/lifecycle-toolkit/pull/1587)
3. feat: update Datadog API to query metrics for range [#1615](https://github.com/keptn/lifecycle-toolkit/pull/1615)
4. feat: update Dynatrace provider to query metrics over a range [#1658](https://github.com/keptn/lifecycle-toolkit/pull/1658)
5. feat: add interval field for kubectl get KeptnMetric [#1689](https://github.com/keptn/lifecycle-toolkit/pull/1689)
6. docs: document timeframe feature for KeptnMetric [#1703](https://github.com/keptn/lifecycle-toolkit/pull/1703)