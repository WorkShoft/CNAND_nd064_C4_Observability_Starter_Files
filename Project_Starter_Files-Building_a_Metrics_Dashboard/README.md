**Note:** For the screenshots, you can store all of your answer images in the `answer-img` directory.

## Verify the monitoring installation

![Installation](answer-img/001.png)

## Setup the Jaeger and Prometheus source
![Graphana Home Page](answer-img/002.png)

## Create a Basic Dashboard
![Dashboard](answer-img/003.png)

## Describe SLO/SLI
Monthly uptime SLI: how often the application was running, and was able to respond to requests (regardless of response time).
Request response time: the average time it takes endpoints to return a response after they are hit with a request.

## Creating SLI metrics.
### CPU Usage
CPU usage is one of the most classic performance metrics that can be a proxy to application responsiveness. High Server CPU usage can mean the server or virtual machine is oversubscribed and overloaded or it can mean a performance bug in your application such as too many spinlocks. Infrastructure engineers use CPU usage (along with its sister metric, memory percentage) for resource planning and measuring overall health. Certain types of applications like high bandwidth proxy services and API gateways naturally have higher CPU usage than other metrics along with workloads that involve heavy floating point math such as video encoding and machine learning workloads.

Sources:
- https://www.moesif.com/blog/technical/api-metrics/API-Metrics-That-Every-Platform-Team-Should-be-Tracking/
- https://community.grafana.com/t/simple-cpu-usage-graph/41316

### Average Memory Usage
Average MB being used per second.

Sources: 
- https://ibm-cloud-architecture.github.io/b2m-nodejs/Prometheus-Grafana/#average-memory-usage
- https://stackoverflow.com/questions/48835035/average-memory-usage-query-prometheus
### Error Rate

The rate of change of the amount of all of the requests that were not 5xx divided by the rate of change of the total amount of requests

Source: https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/

### Median Response Time
The median is the middle number in a sorted, ascending or descending, list of numbers and can be more descriptive of that data set than the average.

Prometheus query: histogram_quantile(0.5, sum(rate(http_request_duration_ms_bucket[1m])) by (le, service, route, method))

Source: https://ibm-cloud-architecture.github.io/b2m-nodejs/Prometheus-Grafana/#median-response-time

### 99th percentile response time
If the 99th Percentile response time is 100ms, then out of 100 requests, 1 request took the max response time of 100 ms.

Prometheus query: histogram_quantile(0.99, sum(rate(http_request_duration_ms_bucket[1m])) by (le, service, route, method))

Sources:
- https://theflyingmantis.medium.com/what-is-99th-percentile-response-time-f23c09c3b54a
- https://ibm-cloud-architecture.github.io/b2m-nodejs/Prometheus-Grafana/#95th-response-time

## Create a Dashboard to measure our SLIs
*TODO:* Create a dashboard to measure the uptime of the frontend and backend services We will also want to measure to measure 40x and 50x errors. Create a dashboard that show these values over a 24 hour period and take a screenshot.

## Tracing our Flask App
*TODO:*  We will create a Jaeger span to measure the processes on the backend. Once you fill in the span, provide a screenshot of it here. Also provide a (screenshot) sample Python file containing a trace and span code used to perform Jaeger traces on the backend service.

## Jaeger in Dashboards
*TODO:* Now that the trace is running, let's add the metric to our current Grafana dashboard. Once this is completed, provide a screenshot of it here.

## Report Error
*TODO:* Using the template below, write a trouble ticket for the developers, to explain the errors that you are seeing (400, 500, latency) and to let them know the file that is causing the issue also include a screenshot of the tracer span to demonstrate how we can user a tracer to locate errors easily.

TROUBLE TICKET

Name: Degraded response time

Date: 2022-03-20

Subject: Latency

Affected Area: API

Severity: Major

Description: Since release 1.2.11, 99th Percentile response time has nearly doubled from 92ms to 172ms. We must:
- Find out and document the root cause.
- Make the changes needed to meet our SLO of a 99th percentile response time below or equal to 100ms.


## Creating SLIs and SLOs
*TODO:* We want to create an SLO guaranteeing that our application has a 99.95% uptime per month. Name four SLIs that you would use to measure the success of this SLO.

## Building KPIs for our plan
*TODO*: Now that we have our SLIs and SLOs, create a list of 2-3 KPIs to accurately measure these metrics as well as a description of why those KPIs were chosen. We will make a dashboard for this, but first write them down here.

## Final Dashboard
*TODO*: Create a Dashboard containing graphs that capture all the metrics of your KPIs and adequately representing your SLIs and SLOs. Include a screenshot of the dashboard here, and write a text description of what graphs are represented in the dashboard.  
