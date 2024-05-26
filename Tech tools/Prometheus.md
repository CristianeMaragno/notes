**

Prometheus

  

What is?

  

Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. Since its inception in 2012, many companies and organizations have adopted Prometheus, and the project has a very active developer and user community. It is now a standalone open source project and maintained independently of any company. To emphasize this, and to clarify the project's governance structure, Prometheus joined the Cloud Native Computing Foundation in 2016 as the second hosted project, after Kubernetes.

  

Features

  

Prometheus's main features are:

  

- a multi-dimensional data model with time series data identified by metric name and key/value pairs
    
- PromQL, a flexible query language to leverage this dimensionality
    
- no reliance on distributed storage; single server nodes are autonomous
    
- time series collection happens via a pull model over HTTP
    
- pushing time series is supported via an intermediary gateway
    
- targets are discovered via service discovery or static configuration
    
- multiple modes of graphing and dashboarding support
    

  

Components

  

The Prometheus ecosystem consists of multiple components, many of which are optional:

  

- the main Prometheus server which scrapes and stores time series data
    
- client libraries for instrumenting application code
    
- a push gateway for supporting short-lived jobs
    
- special-purpose exporters for services like HAProxy, StatsD, Graphite, etc.
    
- an alertmanager to handle alerts
    
- various support tools
    

  

Architecture

  

![](https://lh5.googleusercontent.com/NZYoSXLDx4n_oM224fdByaH5CyVPTxVnjPKdMY5c2BrDa_4apaw_59GkNnSCIkQ8unr16tgFJHfzeUGBWL2EUCsl4SBIQtj9G6TEWf-EE7bJ8Epb3hjvaWbTq71aX6M4tf9zpPffhZJCmwL3eNBO)

Prometheus scrapes metrics from instrumented jobs, either directly or via an intermediary push gateway for short-lived jobs. It stores all scraped samples locally and runs rules over this data to either aggregate and record new time series from existing data or generate alerts. Grafana or other API consumers can be used to visualize the collected data.

  

Basic working

  

![](https://lh3.googleusercontent.com/62hCeEXFTHQYlNueFRo9j7DXNdOWj2GwoJJXwjAPvsQ5OYkTlaGPdsfg91SoqrE5mHzMDE2gEowg3Z6F14RszL5QhKxjQEnI-oJzWXHhTODftK1gjnMXmTfj3_qZ5qU345Y-a0mFaBzX-UDDR2lB)

  

Prometheus is a server component and typically you run one instance of prometheus in each environment(prod, dev etc). Is cross-platform. It runs a lot o functions inside a server:

- Scheduler components that fetch metrics from the systems you want to monitor. An important concept of prometheus is that it uses a pool model, you need to expose metrics from your systems and prometheus will feches those metrics each 5 minutes(or other time you configure). Those systems can be linux or windows servers that provide metrics about ram usage, cpu etc, or they could be websites providing metrics abouts http request response, or they could even be custom metrics built in your application that says as exemple how many users are using the application etc.
    
- Prometheus stores all those metrics in a time serial database that is also running in a server. Time series data just means that all the metrics are stored with a timestamp. Your systems just expose the metric and prometheus stores efficiently with the timestamp, which makes it easy to query and filter the metrics using time ranges.
    
- Prometheus has its own query language because time series data doesn’t fit well with regular sql. There is http api running in the prometheus server that lets you run those queries. There is also a web UI where you can make those queries, basic admin tasks and view configurations. The web UI is not a fully featured dashboard, for this you use a separate system that connects with the prometheus API.
    
- Prometheus has an advanced alerting system, you create rules of alerting and when those are triggered there is a separate prometheus component that takes action to alert you, sending email, pages, creating tickets etc.
    

What makes Prometheus different from other monitoring systems? Is the way that feches metrics. Any system you want to monitor needs to run an exporter that provides all the metrics in a http endpoint. The prometheus server grabs those metrics from the endpoint on a schedule and stores them. Prometheus doesn’t care about the type of system that is being monitored or what the metrics actually mean. Prometheus provides a layer o consistency to monitoring so the process of exporting and collecting metrics is the same even on very different systems and metrics content

![](https://lh6.googleusercontent.com/LYyHkuCU772p8TrfbCzzuto2_ty9Cc81Kj6QTBwnfNhrRjT3khpV6mejLAdYYt7hfo20Ek_6ZMGWGgFqfyWvwW0ejjj_TAi_WrOSsFETEeUPr7F_bBGvv3D3ZMqDoUEEp2MoIQuT3ViMRCZ2l0T9)

![](https://lh4.googleusercontent.com/6a2I1aF4gZNhVBX9R5gjGaG5fJKI5htYQ7K3TevyO_r8rLLhFnk698HMIAX3KVqNd2gZ20N8Pfa3J1eq0HCPdzPYZ_G4hN5x2sJJI2mUTGR-gK47rpdcHhE4E6kciEVLtEeMO2A_e5lCLbVqkQpv)

Example: You run the node exporter(that is part of prometheus ecosystem) on a linux server that provides a http endpoint which returns the metrics values that are data collected by the linux system, the exporter just makes available in the prometheus format as the exemple above.

There are a bunch of exporter maintained by the community to various types of systems and a lot of client libraries to many languages so you can add to your projects and get the metrics. 

  

Types of metrics: 

- Gauges: Um número variável, como quantos usuários estão online no momento
    
- Counters: Soma um valor, como o número de vezes que algo aconteceu. Sempre incrementa
    

  

Test

  

[https://prometheus.io/docs/prometheus/latest/getting_started/](https://prometheus.io/docs/prometheus/latest/getting_started/)

  
  
  
**