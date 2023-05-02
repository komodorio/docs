# Metrics

Komodor enables you to overview metrics like cpu and memory on your cluster using the prometheus metrics server. 

NOTE: We also support prometheus that is installed by GrafanaLabs managed service

## Prerequisites

- Agent version from 0.1.108
- Installed prometheus on your cluster

Coming soon: prometheus installation integration!

## How does it work?

Komodor agent identifies Prometheus in the cluster and saves the configuration details.
The agent sends an HTTP request to the Prometheus metrics server and gets matric results like CPU and memory. The received data is processed and displayed in the Pods and Nodes screens.

### Pods:

Data is displayed in 2 columns:

- %CPU/R - percentage of cpu usage per request
- %MEM/R - percentage of memory usage per request

<img src="./img/pod_metrics.png" width="550">

More columns can be added: %CPU/L, %MEM/L, CPU, Memory

<img src="./img/metrics_columns.png" width="200">

### Nodes:

Data is displayed in 3 columns:

- %CPU - utilization of CPU allocation in percentage
- %Memory - utilization of memory allocation in percentage
- %Disk - utilization of disk capacity in percentage

<img src="./img/node_metrics.png" width="550">

More usage columns can be added: CPU, Memory, Disk

## Add metrics integration

In case you have prometheus in your cluster and the agent doesn’t identify it you can add metrics integration.

### Steps:

1. Go to integration screen and click on Prometheus metrics server

<figure>
    <img src="./img/prometheus_metrics_icon.png" width="400">
</figure>

2. Enter the fqdn as follows: `<namespace>/<service>:<port>`

- Namespace - prometheus service namespace
- Service - prometheus service name
- Port - The port that prometheus service is listening to
<figure>
    <img src="./img/prometheus_metrics.png" width="400">
</figure>

3. Choose how you installed prometheus: helm or other operator
4. Click install
