
![Header](Assets/Observability-For-SRE.png)

> ✏ If you can't measure it, you can't manage it.

# Table of Contents
* [Why do we need observability?](#Why-do-we-need-observability?)
* [How does Observability work?](#How-does-Observability-work?)
* [Logs](#Logs)
* [Metrics](#Metric)
* [Traces](#Traces)
* [References](#References)
## Why do we need observability?
* Once you have your system up and running, we need to measure its state to be able to identify if any issue occurs.
* It also helps to know the source of the problem in order to know where to look instead of relying on the engineer ability solely.
## How does Observability work?
- Observability works on 3 pillars
	1. Logs
	2. Metrics
	3. Traces
### Logs
* Logs are a record with all the events and messages a software system produces.
* Each service in the system produces logs. We store these logs in order to have detailed information about the system.
* Their usefulness diminishes as they get older. So, we store logs long enough to fulfill their lifespan and evict or archive accordingly to reduce overhead storage.
* Log retention policies: are guidelines to automatically expire log data after a specified duration.
#### Tools used for logging
* [Grafana Loki](Logging/Grafana%20Loki) 
	* Adding Loki as a data-source in Grafana enables to visualize the logs in it.
* [Elastic Beats](Logging/Log%20Monitoring%20Using%20Elastic%20Stack) 
	* The role of beats in ELK stack is that they are **shippers** for different data types to elastic.
	* Types
		* Filebeat: For logs << Similar to Loki
		* Metric Beat: For Metrics << Used in monitoring
		* Heartbeat: For uptime monitoring (check if the service is reachable or not)
		* Auditbeat: For audit data (user's activity)
		* Packetbeat: For network data << To check traffic
		* Winlogbeat: For windows event log
### Metrics
* Unlike logs, metrics are measurements that provide a snapshot of a system's performance at a specific point in time.
* These measurements can be CPU or memory consumption.
* Alerts can be configured so that if a metric pass a certain threshold a notification can be sent to the developer to fix the issue. This notification can be: Slack message, call, etc...
#### Tools
* [Prometheus](Metrics/Prometheus)
* Zabbix
* Grafana Mimir << like Prometheus but for a larger scale

> [!Note]
> To apply high availability in Prometheus we use a tool called Thanos.
### Traces
* A trace is the complete journey of a request or workflow as it moves from one part of the system to another. 
* We have 2 metadata information
	* Span ID: an application generates every time it reports an event.
	* Trace ID: each application will pass along if the data it receives contains it. If not available, a new one will be generated and reported.
#### Tools
* Grafana Tempo
* Zipkin
* Jaeger

> [!Note]
> For distributed tracing, we use service mesh. 
> Famous examples: Linkerd, Consul Connect.
> When to use distributed tracing? When you have an application with multiple microservices like an online shopping web app. 

## References
* [Tracing and Observability - Medium](https://medium.com/swlh/tracing-and-observability-9ab98438d773)
* [The Three Pillars of Observability - Cindy Sridharan](https://www.oreilly.com/library/view/distributed-systems-observability/9781492033431/ch04.html)