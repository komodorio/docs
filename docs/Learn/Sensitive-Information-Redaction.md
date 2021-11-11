# Sensitive data redaction in Komodor’s k8s-watcher

## What is it

It’s likely that there are values you don’t want to send to Komodor as plain text. Kubernetes Secrets, for instance, ConfigMap sensitive values or container environment variables.
When configured - we will redact the specific value. That way Komodor won't see any sensitive data while you will still see configuration diff.

## How to integrate

Inside `komodor-k8s-watcher.yaml` you should add a list of string or regular expressions under redact key as such:

komodor-k8s-watcher
``` yaml
watchNamespace: all
namespacesBlacklist:
  - kube-system
redact:
   - "PG_.*"
   - ".*PASSWORD.*"
nameBlacklist: ["leader", "election"]
collectHistory: false
```

### Secret Resource
By default, Komodor’s k8s-watcher is hashing all secrets values.

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
Komodor’s k8s-watcher will hash `template.spec.template.[containeres|initContainers].env` list of variables inside Deployment objects for pre-configured list of keys or list of regular expressions.

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