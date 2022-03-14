# Workflows

## Introduction

Once configured, Komodor Workflows are designed to automatically detect different failure scenarios in nodes, PersistentVolumeClaims (PVC) and services such as Loadbalancers, Ingress controllers and Endpoints, and investigate certain aspects around them in order to provide additional information to simplify the troubleshooting process and reduce mean time to resolution.

Komodor currently offers two Workflows, they are the Node Detector and PVC Detector.

## Node Detector

The Node Detector is triggered when a node condition changes to a faulty [condition](https://kubernetes.io/docs/concepts/architecture/nodes/#condition) and persists longer then the configured duration (default is 60 seconds).

- Once triggered, we perform the following checks as part of our investigation 
    - Is the node ready?
    - Is the node overcommitted?
    - Is the node under pressure?
    - Is the network available?
    - Is the node schedulable?
    - Are pods being evicted?
    - Are user pods healthy?
    - Are system pods healthy?
    - Node overall resource consumption including top 5 pod consumers (requires metric-server installed)
- Note
    - The Node Detector currently does not detect nodes in an "unknown" state, this means spot instance interruptions or scale-down events will not be handled by the Workflow, this could possibly affect other scenarios as well.
    - The Node detector will only run on nodes that have a creation time greater than 3 minutes.

##  PVC Detector
Detects PVCs in a pending state. 

The PVC Detector is triggered when a PVC is in a pending state for the defined duration (default is 60 seconds).
- We perform the following checks as part of our investigation   
    - PVC creation, utilization, and readiness issues
    - Volume provisioner related issues
    - PVC spec changes
    - Identify the impact on related services

##  Services Detector (Coming Soon)
Detects services such as Ingress controller, endpoints and Loadblancers in an unhealthy state. 

The Detector is triggered when a PVC is in a pending state for the defined duration.

- We perform the following checks as part of our investigation   
    - PVC creation, utilization, and readiness issues
    - Volume provisioner related issues
    - PVC spec changes
    - Identify the impact on related services

## Settings

- Sensor: Resources can be monitored at either the cluster scope or namespace(s) scope.
- Duration: The minimum time the issue has to presist prior to running the Workflow checks, if the problem has been resolved during this duration the Workflow will not run. Default is 60 seconds.
- Sink/Notification: Where Komodor will send a notifications when a Workflow is triggered, supports either Slack or Microsoft Teams.

## Supported Actions
- Pause: Pause a workflow and its notifications.
- Edit: Change Sensors, Duration, Notifications and Name.
- Remove: Delete a workflow.

## How to Configure

1. Click on the _workflows_ tab

2. Mouse over the workflow you would like to add and click _Add Workflow_

3. Click _Activate_ on the top right hand corner

4. Configure the Sensor

5. Pick a cluster

6. Pick a namespace(s) or leave this option blank for all namepsaces on the selected cluster

7. Click on _Continue_

8. Set the minimum duration in seconds, default is 60 seconds.

9. Choose a notification platform and channel, or choose _Continue without notifications_

10. Name the workflow and click _Activate Workflow_

## How to Remove a Workflow

1: Select the workflow you want to delete

## How to Remove a Workflow

1: Select the workflow you want to delete


## How to delete a Workflow

1: Select the workflow you want to delete







## Prerequisites for Workflows

**Agent version** - 0.1.72 and above we recommended running the latest version. See how to update the agent [here](https://docs.komodor.com/Learn/Komodor-Agent.html#updating-the-agent).

**Please note**: Recently the ClusterRole was updated with metric-server related permissions and might require an update for customers already running agent version 0.1.72.
