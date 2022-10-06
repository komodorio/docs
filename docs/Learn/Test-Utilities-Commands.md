# Test Utilities Commands


## Komodor Agent Test Utilities

You can use the `komodorio/k8s-watcher` docker image to run the `test` command.
```
Komodor Agent Test Utilities
Usage:
  -clusterconnectivity
    	Run utility to test connectivity to Kubernetes API.
  -connectivity
    	Run utility to test connectivity to Komodor's API. Requires env var: [KOMOKW_API_KEY]
  -inputlog string
    	Used in conjunction with -logredactor to provide an input log to redact (default "Example log with supersecret password:abc123 and username=root")
  -logredactor
    	Run utility to test data redaction for pod logs. Requires env var: [KOMOKW_REDACT_LOG]
```


### Testing connectivity to Komodor API

```bash
❯ docker run --rm -e KOMOKW_API_KEY="YOUR_API_KEY" komodorio/k8s-watcher test -connectivity
no configuration file found, starting with env vars / defaults
time="2022-09-15T13:27:29Z" level=info msg="Using cluster name <production> from context"
time="2022-09-15T13:27:29Z" level=info msg="Identifying agent with Komodor servers" agentId=xxx serverHost="https://app.komodor.com"
time="2022-09-15T13:27:30Z" level=info msg="Successfully connected to Komodor API !!!"
```

### Testing connectivity to Kubernetes API

```bash
❯ docker run --rm -v $HOME/.kube/config:/root/.kube/config komodorio/k8s-watcher test -clusterconnectivity
no configuration file found, starting with env vars / defaults
Running outside kubernetes - using kubeconfig file: /Users/mickael/.kube/config
Successfully connected to Kubernetes API !!!  kubernetesServerInfo=v1.22.12-gke.2300
Available API Groups:
core
	v1
apiregistration.k8s.io
	apiregistration.k8s.io/v1
apps
 	apps/v1
...
...
```


### Testing logs redaction patterns

You can easily test the patterns you want to configure before deploying by using our docker image and our utilities command.

```bash
❯ docker run --rm -e KOMOKW_REDACT_LOGS="redaction" komodorio/k8s-watcher test -logredactor -inputlog="The log line you want to test redaction here"

Patterns to redact: [redaction]

Input log (before redaction):
The log line you want to test redaction here

Output log (after redaction):
The log line you want to test <REDACTED> here
```