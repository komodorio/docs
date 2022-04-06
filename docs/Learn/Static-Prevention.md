# Static Prevention 

## Introduction

Otherwise then helping you troubleshoot incidents over Kubernetes, Komodor wants to 
help you prevent those incidents from happening in the first place.

### How it works?

Each time your workload got rolled out and something got changed in the workload YAML, we run
some checks statically on your yaml. Those checks are supposed to help you improve your YAML reliability
and efficiency.

Checks results are presented under `Best practices` block within every service.

If you wish to ignore any check, just click on the `ignore` button under the `Best practices` popup.

### Checks we run

#### - Deployment Missing Replicas

    What is checked?
        Check if there is only one replica for a deployment.
    Why we want to check it?
        More than one replica recommended to be scheduled.

#### - Tag Not Specified

    What is checked?
        Check if an image tag is either not specified or latest.
    Why we want to check it?
        Docker's latest tag is applied by default to images where a tag hasn't been specified. 
        Not specifying a specific version of an image can lead to a wide variety of problems.

#### - Pull Policy Not Always

    What is checked?
        Check if an image pull policy is not always.
    Why we want to check it?
        By default, an image will be pulled if it isn't already cached on the node attempting
        to run it. This can result in variations in images that are running per node, or 
        potentially provide a way to gain access to an image without having direct access 
        to the ImagePullSecret.

#### - Liveness Probe Missing

    What is checked?
        Check if a liveness probe is not configured for a pod.
    Why we want to check it?
        Liveness probes are designed to ensure that an application stays in a healthy state.
        When a liveness probe fails, the pod will be restarted.


#### - Readiness Probe Missing

    What is checked?
        Check if a readiness probe is not configured for a pod.
    Why we want to check it?
        A readiness probe can ensure the traffic is not sent to a pod until it is actually 
        ready to receive traffic.

#### - CPU Requests Missing

    What is checked?
        Check if resources.requests.cpu attribute is not configured.
    Why we want to check it?
        Setting appropriate resource requests will ensure that all your applications have
        sufficient compute resources.

#### - CPU Limits Missing

    What is checked?
        Check if resources.limits.cpu attribute is not configured.
    Why we want to check it?
        Setting appropriate resource limits will ensure that your applications do not 
        consume too many resources.

#### - Memory Requests Missing

    What is checked?
        Check if resources.requests.memory attribute is not configured.
    Why we want to check it?
        Setting appropriate resource requests will ensure that all your applications have
        sufficient compute resources.

#### - Memory Requests Missing

    What is checked?
        Check if resources.limits.memory attribute is not configured.
    Why we want to check it?
        Setting appropriate resource limits will ensure that your applications do not consume
        too many resources.