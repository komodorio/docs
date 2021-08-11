# Komodor source control support

### What is it
Enrich services with relevant source control metadata. This allows to show smart-diffs as part of Komodor service changes tracking.
Doing so connects the specific service with repositories that might not be the original codebase, such as infrastructure or CI repos, which are still relevant changes.

### How to integrate
Add the following annotations to your service's Kubernetes spec:

```YAML
    app.komodor.com/[name]: FULL_REPO_URL
    app.komodor.com/[name].ref: SOURCE_CONTROL_REF
    app.komodor.com/[another-name]: ANOTHER_FULL_REPO_URL
    app.komodor.com/[another-name].ref: ANOTHER_ SOURCE_CONTROL_REF    
```

### Full example

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: git-example
  annotations:
    app.komodor.com/app: https://github.com/komodorio/infra
    app.komodor.com/app.ref: 3350e3311f9520fe5e237e2d71f339029ee051d8     
    app.komodor.com/infra: https://github.com/komodorio/helm-charts
    app.komodor.com/infra.ref: 32b355df32713afc511528d909eff296e91dbe74 
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
          ports:
            - containerPort: 8080
              protocol: TCP
```

### Tracked Files
Once the integration with Github is established, Komodor will scan the pull requests files (only the names), to see if there are common, interesting files that have been updated. For example, when there was a change in `Dockerfile`, Komodor will show that in the Deploy summary.


To customize which files will be tracked by Komodor. Using Kubernetes annotation `app.komodor.com/tracked_files` that accepts multiline string (gitignore like) to specify the files. 
For example, track any `yaml` files:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: git-example
  annotations:
    app.komodor.com/tracked_files: |
      *.yaml
    app.komodor.com/app: https://github.com/komodorio/infra
    app.komodor.com/app.ref: 3350e3311f9520fe5e237e2d71f339029ee051d8     
    app.komodor.com/infra: https://github.com/komodorio/helm-charts
    app.komodor.com/infra.ref: 32b355df32713afc511528d909eff296e91dbe74 
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
          ports:
            - containerPort: 8080
              protocol: TCP"
```