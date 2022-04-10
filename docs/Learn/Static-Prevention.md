# Static Prevention 

## Introduction

Komodor not only provides you with remediation instructions when troubleshooting Kubernetes incidents,
but also helps to prevent them from happening in the first place.

### How it works?

Each time a workload is rolled out, and a change has been made to the workload YAML, Komodor runs a set of statical 
checks in order to improve your YAML’s reliability and efficiency. 
The results of our scan are presented under the "Best Practices” section within every service.

If you wish to ignore any check, just click on the `ignore` button under the `Best practices` pop-up.

### Checks we run

#### - Deployment Missing Replicas

    What is checked?
        Check if there is only one replica for a deployment.
    Why should this be checked?
        More than one replica recommended to be scheduled.

#### - Tag Not Specified

    What is checked?
        Check if an image tag is either not specified or the latest tag has not been used.
    Why should this be checked?
        Docker's latest tag is applied by default to images where a tag hasn't been specified. 
        Not specifying a specific version of an image can lead to a wide variety of problems.

#### - Pull Policy Not Always

    What is checked?
        Check if an image pull policy is not always.
    Why should this be checked?
        By default, an image will be pulled if it isn't already cached on the node attempting
        to run it. This can result in variations in images that are running per node, or 
        potentially provide a way to gain access to an image without having direct access 
        to the ImagePullSecret.

#### - Liveness Probe Missing

    What is checked?
        Check if a liveness probe is not configured for a pod.
    Why should this be checked?
        Liveness probes are designed to ensure that an application stays in a healthy state.
        When a liveness probe fails, the pod will be restarted.


#### - Readiness Probe Missing

    What is checked?
        Check if a readiness probe is not configured for a pod.
    Why should this be checked?
        A readiness probe can ensure that the traffic is not sent to a pod until it is actually 
        ready to receive the traffic.

#### - CPU Requests Missing

    What is checked?
        Check if resources.requests.cpu attribute is not configured.
    Why should this be checked?
        Setting appropriate resource requests will ensure that all your applications have
        sufficient compute CPU resources.

#### - CPU Limits Missing

    What is checked?
        Check if resources.limits.cpu attribute is not configured.
    Why should this be checked?
        Setting appropriate resource limits will ensure that your applications do not 
        consume too many CPU resources.

#### - Memory Requests Missing

    What is checked?
        Check if resources.requests.memory attribute is not configured.
    Why should this be checked?
        Setting appropriate resource requests will ensure that all your applications have
        sufficient memory compute resources.

#### - Memory Limits Missing

    What is checked?
        Check if resources.limits.memory attribute is not configured.
    Why should this be checked?
        Setting appropriate resource limits will ensure that your applications do not consume
        too many memory resources.