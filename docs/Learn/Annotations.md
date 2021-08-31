## Komodor kubernetes annotations

Komodor annotations (AKA Komodor as code), is a method to allow users to configure everything related to Komodor as part of their native k8s yaml.
Komodor annotations should be placed in the deployment resource annotations (annotations set on the pod template are ignored)

## Notifications

Configure the Slack channel notification as part of the deployment object.


### How

| annotation                                        | values | description                                                       | example             | default |
|---------------------------------------------------|--------|-------------------------------------------------------------------|---------------------|---------|
| app.komodor.com/notification.deploy.slack         | string | Slack channel name for all deploy events notifications            | “deploy-brain-team" |         |
| app.komodor.com/notification.deploy_fail.slack    | string | Slack channel name for failed deploy events notifications         | “deploy-failed"     |         |
| app.komodor.com/notification.deploy_success.slack | string | Slack channel name for successful deploy events notifications     | “deploy-success"    |         |
| app.komodor.com/notification.health.slack         | string | Slack channel for health event notifications                      | “alerts-p1”         |         |


## Service Links

Define quick-links for a specific service, making it easier to get context when troubleshooting.


### How

 in the form of `app.komodor.com/service/link/name:url`

Examples:


| annotation                                                 | values | description                                                | example             | default |
|------------------------------------------------------------|--------|------------------------------------------------------------|---------------------|---------|
| app.komodor.com/service.link.grafana-overall-system-health | url    | Url for Grafana health dashboard related to this service.  | “deploy-brain-team" |         |
| app.komodor.com/service.link.datadog-http-500              | url    | Url for datadog dashboard with bad http                    | “alerts-p1”         |         |
| app.komodor.com/service.link.company-playbook              | url    | The playbook for the company playbook                      | “120”               | “30”    |



## CI-Deploy Links

For each deployment version, you can add a quick link with the job url.

 

How

`app.komodor.com/deploy/job/name:url`

Example:

| annotation                         | values | description                                  | Example                                | default |
|------------------------------------|--------|----------------------------------------------|----------------------------------------|---------|
| app.komodor.com/deploy.job.jenkins | url    | Link to Jenkins job that deploys the service | https://ci.jenkins-ci.org/computer/job |         |




## Deploy Links

For each deployment version, you can add a quick link with the relevant filters already in place!

 

How

`app.komodor.com/deploy/link/name:value`

Examples:


| annotation                         | values | description                                  | Example                                                                                                    |
|------------------------------------|--------|----------------------------------------------|------------------------------------------------------------------------------------------------------------|
| app.komodor.com/deploy.link.logs   | url    | Link for the specific version logs           | https://app.logz.io/#/dashboard/kibana/discover?_a=env:123.0.1                                             |
| app.komodor.com/deploy.link.sentry | url    | Link for the specific version  Sentry issues | https://sentry.io/organizations/rookoutz/issues/?project=1320440&query=sdk.version%3A1.0.1&statsPeriod=14d |

### Full example

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: annotation-example
  annotations:
    app.komodor.com/notification.deploy.slack: "#deploy-slack-channel"
    app.komodor.com/notification.alert.slack: "#p1-health-issues"
    app.komodor.com/service.link.grafana-overall-system-health: "https://grafana.com/service/annoation-exmaple"
    app.komodor.com/service.link.datadog: "https://datadog.com/dashboard/annoation-exmaple"
    app.komodor.com/service.link.playbook: "https://docs.google.com/playbook"    
    app.komodor.com/deploy.job.jenkins: "https://ci.jenkins-ci.org/computer/job"
    app.komodor.com/deploy.link.logs: "https://app.logz.io/#/dashboard/kibana/discover?_a=env:1.0.1"
    app.komodor.com/deploy.link.sentry: "https://sentry.io/organizations/rookoutz/issues/?project=1320440&query=sdk.version%3A1.0.1&statsPeriod=14d"        
spec:
  selector:
    matchLabels:
      run: example
  replicas: 1
  template:
    metadata:
      labels:
        run: example
    spec:
      containers:
        - name: hello-world
          image: gcr.io/google-samples/node-hello:1.0.1
          ports:
            - containerPort: 8080
              protocol: TCP
```




## Annotations Best Practices
In Komodor we believe that k8s annotation is the best practice for describing service metadata.
This includes all of the “extra” fields used to tag and label your service, both for other team members and for external tools.
BTW, We collect the data both from annotations and labels.

### Where does Komodor utilize annotation?
Everywhere, Komodor will use these annotation to create a powerful connections between services and enrich service information in all of the following:
* Service explorer
* Related services
* Events screen
* Match alerts to the right services 

### [Official kubernetes recommendation](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/)
```yaml 
app.kubernetes.io/component: database
app.kubernetes.io/part-of: wordpress
app.kubernetes.io/managed-by: helm
```

### Komodor recommendation
```yaml
app.koomdor.com/label/team: backend
app.koomdor.com/label/group: infrastructure
app.koomdor.com/labe/owners: "#infa-team"
app.koomdor.com/labe/alert-team: "#devs"
app.koomdor.com/labe/Impacted-by: redis
```

### Usage example
* Tagging Team annotation on relevant services and adding relevant metadata on the alert metadata in datadog.
* Using the Team name in the alert tools (for example PD) as part of the komodor labels
