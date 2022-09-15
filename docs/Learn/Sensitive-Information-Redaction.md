# Sensitive data redaction in Komodor’s k8s-watcher

## What is it

It’s likely that there are values you don’t want to send to Komodor as plain text. Kubernetes Secrets, for instance, ConfigMap sensitive values, container environment variables or pod logs.
When configured - we will redact the specific value. That way Komodor won't see any sensitive data while you will still see configuration diff.

## How to integrate

Inside `komodor-k8s-watcher.yaml` you should add a list of string or regular expressions under `redact` and `redactLogs` key as such:

komodor-k8s-watcher
``` yaml
watchNamespace: all
namespacesBlacklist:
  - kube-system
redact:
   - "PG_.*"
   - ".*PASSWORD.*"
redactLogs:
   - "password=(.+?)\b"
   - "(?U)\"sessionId\": (\".+\"{1})"
nameBlacklist: ["leader", "election"]
collectHistory: false
```

### How to integrate using helm upgrade command

``` bash
helm upgrade --install k8s-watcher komodorio/k8s-watcher --set watcher.redact="{.*PASSWORD.*,.*password.*,.*KEY.*,.*key.*,.*SECRET.*,.*secret.*}" --set watcher.redactLogs="{password=(.+?)\b,(?U)\"sessionId\": (\".+\"{1})}" --set apiKey=<API-KEY> --set watcher.clusterName=<cluster-name> --set watcher.enableAgentTaskExecution=true --set watcher.allowReadingPodLogs=true 
```

### How to integrate using environment variables

Separate multiple values with a whitespace in the environment variable value.  
To include a whitespace in the patterns to redact, make sure to use `\s` as it the patterns are regexp.

```bash
export KOMOKW_REDACT=".*password.* PG_.*"
export KOMOKW_REDACT_LOGS="password=(.+?)\b (?U)\"sessionId\": (\".+\"{1})"
```

### Secret Resource
By default, Komodor’s agent is hashing all secrets values.

### ConfigMap resource
You can preconfigure a list of keys for Kubernetes watcher to also redact specific values from ConfigMap.


komodor-k8s-watcher.yaml:
``` yaml
redact:
    - "SENTRY_API_KEY"
    - "PG_.*"
```

configmap.yaml:
``` yaml
apiVersion: v1
kind: ConfigMap
metadata:
  Name: sensitive-config-map
data:
  SENTRY_API_KEY: super_secret
  PG_SECRET: super_secret
  PG_USERNAME: super_secret
```

All the above “super_secret” will be sent has hashed value.

### Deployment resource
Komodor’s agent will hash `template.spec.template.[containeres|initContainers].env` list of variables inside Deployment objects for pre-configured list of keys or list of regular expressions.

komodor-k8s-watcher.yaml:
``` yaml
redact:
    - "SENTRY_API_KEY"
    - "PG_.*"
```

deployment.yaml:
``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sensitive-deployment
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
          image: gcr.io/google-samples/node-hello:1.0
          env:
            - name: PG_USERNAME
              value: super_secret
            - name: SECRET
              value: this_will_show_up
```

In the above deployment example we will not send the secret values for PG_USERNAME.

SECRET will show up as is due to the fact it won’t match any string or regex in our configuration.


### Pod Logs

**Note: Pod Logs redaction is available starting from Komodor Agent version**

Komodor's agent will redact any logs matching one of the patterns set in the `redactLogs` configuration.

komodor-k8s-watcher.yaml:
``` yaml
redactLogs:
   - "password=(.+?)\b"
   - "(?U)\"sessionId\": (\".+\"{1})"
```

Environment variables:
```bash
export KOMOKW_REDACT_LOGS="password=(.+?)\b (?U)\"sessionId\": (\".+\"{1})"
```

Example logs:
```json
INPUT: example my password=supersecret and something else
OUTPUT: example my <REDACTED> and something else

INPUT: { "level": "INFO", "message": "User has added Item 12453 to Basket", "sessionId": "SESS456", "timestamp": 1634477804 }
OUTPUT: { "level": "INFO", "message": "User has added Item 12453 to Basket", <REDACTED>, "timestamp": 1634477804 }
```