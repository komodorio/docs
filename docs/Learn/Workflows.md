# Workflows

Komodor Workflows are built to detect different scenarios, investigate certain aspects around them and provide additional context to simplify the troubleshooting process and reduce MTTR

## Supported configurations per Workflow:

- Resources to monitor (cluster & namespaces)
- Duration - specifies the length of time the issue has to presist prior to running the actual checks, if the problem has been resolved during the duration of the workflow it will not run (currently defaults to 60s for all workflows)
- Sink/Notification - will be triggered whenever a workflow runs

## Prerequisites:

**Required agent version** - 0.1.72 (recommended - latest version)  

**Please note**: recently the ClusterRole was updated with metric-server related permissions and might require an update for customers already running with 0.1.72 .

## Node Detector
Detects Nodes with faulty [Conditions](https://kubernetes.io/docs/concepts/architecture/nodes/#condition). 

The Detector is triggered when a Node Condition/s changes to a faulty Condition and lasts through the configured Duration. 

- We perform the following checks as part of our investigation 
    - Is the node ready?
    - Is the node overcommitted?
    - Is the node under pressure?
    - Are system pods healthy?
    - Is the network available?
    - Are pods being evicted?
    - Are user pods healthy?
    - Is the node schedulable?
    - Node overall resource consumption including top 5 pod consumers (requires metric-server installed)
  
- Notes
    - The Node detector currently does not cover nodes in an "Unknown" state (this means Spot interruptions or scale-down events will not be handled by the WF, this could affect other scenarios as well)
    - The Node detector will only run on Nodes that are created for more than 3 minutes (there is a 3-minute delay from Node create time prior to running the workflow)

## PVC Detector
Detects PVCs in a pending state. 

The Detector is triggered when a PVC is in a pending state for the defined duration. 
- We perform the following checks as part of our investigation   
    - PVC creation, utilization, and readiness issues
    - Volume provisioner related issues
    - PVC spec change
    - Identify the impact on your services

## Service Detector (coming soon)
