# Loft Integration

The Loft integration enables you to install a Komodor agent automatically on every vcluster created by Loft.
The vcluster appears in Komodor's UI like a regular cluster and allows users to access, detect, invetigate and remediate their own vclusters independently.
You can see the full potential of the Loft <> Komodor integration in this [Live Demo](https://www.linkedin.com/video/event/urn:li:ugcPost:7004685584732471296/).
ג
In the Demo, there is a detailed exaplanation on how to configure it using the Loft UI.
The steps below include the configuration manifests to create the same environment configuration using Loft Custom Resources.

<br>

## Integration Process

1. Create a Komodor App in Loft
2. Create a vcluster template with the Komodor App
3. Deploy your first vcluster with the Komodor App

<br>

### Step1: Create a Komodor App in Loft

Before applying this YAML, please create a Kubernetes Cluster integration in Komodor and replace the `{{API-KEY}}` with the API key Komodor generated for you.
Create a Komodor App in loft by applying this application configuration.

``` bash
apiVersion: storage.loft.sh/v1
kind: App
metadata:
  name: komodor
spec:
  access:
  - subresources:
    - '*'
    users:
    - admin
    verbs:
    - '*'
  - subresources:
    - '*'
    users:
    - '*'
    verbs:
    - get
  config:
    chart:
      name: k8s-watcher
      repoURL: https://helm-charts.komodor.io
      version: 1.0.18
    values: |+
      watcher:
        clusterName: {{ .Values.clusterName }}
        actions:
          basic: true
          advanced: true

      apiKey: {{API-KEY}}

  displayName: Komodor
  icon: https://komodor.com/wp-content/uploads/2022/11/komodor-logo-blue.jpg
  owner:
    user: admin
  parameters:
  - description: Cluster Name
    label: Cluster Name
    required: true
    variable: clusterName
```  

<br>

### Step 2: Create a vcluster template with the Komodor App

Add the Komodor App to the vcluster templates you are using or create a new one using this vcluster template.
``` bash
apiVersion: storage.loft.sh/v1
kind: VirtualClusterTemplate
metadata:
  name: cluster-with-komodor
spec:
  access:
  - subresources:
    - '*'
    users:
    - admin
    verbs:
    - '*'
  - subresources:
    - '*'
    users:
    - '*'
    verbs:
    - get
  displayName: cluster-with-komodor-and-apps
  owner:
    user: admin
  template:
    access: {}
    apps:
    - name: komodor
      namespace: default
    helmRelease:
      chart:
        name: vcluster
      values: "# Additional helm values for the virtual cluster\n# Loft will automatically
        add the correct service CIDR \n# and k3s version to the helm values upon deployment\nstorage:\n
        \ size: 1Gi\n\n# syncer:\n   # If you don't want to sync ingresses from the
        virtual cluster to \n   # the host cluster uncomment the next lines\n   #
        extraArgs: [\"--disable-sync-resources=ingresses\"]"
    metadata:
      creationTimestamp: null
```

<br>

### Step 3: Deploy your first vcluster with Komodor
Create a new vcluster using the Loft UI or sync an existing one that uses a vcluster template with the Komodor app.

<br>

## Want to simluate the exact scenario as explained in the demo? Use these CRs:

In the Demo we showed an example of an application being deployed with the Komodor app.
You can use the same configratuion by applying these files:
``` bash
apiVersion: storage.loft.sh/v1
kind: VirtualClusterTemplate
metadata:
  annotations:
  name: cluster-with-komodor
spec:
  access:
  - subresources:
    - '*'
    users:
    - admin
    verbs:
    - '*'
  - subresources:
    - '*'
    users:
    - '*'
    verbs:
    - get
  displayName: cluster-with-komodor-and-apps
  owner:
    user: admin
  template:
    access: {}
    apps:
    - name: komodor
      namespace: default
    - name: my-service
      namespace: default
    helmRelease:
      chart:
        name: vcluster
      values: "# Additional helm values for the virtual cluster\n# Loft will automatically
        add the correct service CIDR \n# and k3s version to the helm values upon deployment\nstorage:\n
        \ size: 1Gi\n\n# syncer:\n   # If you don't want to sync ingresses from the
        virtual cluster to \n   # the host cluster uncomment the next lines\n   #
        extraArgs: [\"--disable-sync-resources=ingresses\"]"
---
apiVersion: storage.loft.sh/v1
kind: App
metadata:
  name: my-service
spec:
  access:
  - subresources:
    - '*'
    users:
    - admin
    verbs:
    - '*'
  - subresources:
    - '*'
    users:
    - '*'
    verbs:
    - get
  config:
    chart: {}
    manifests: |-
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: accounts-api
        labels:
          app: komodor-oomkilled
      spec:
        replicas: 1
        selector:
          matchLabels:
            app: komodor-oomkilled
        template:
          metadata:
            labels:
              app: komodor-oomkilled
          spec:
            containers:
            - name: komodor-oomkilled
              image: polinux/stress
              command: ["stress"]
              args: ["--vm", "10", "--vm-bytes", "100M", "--vm-hang", "120", "--backoff", "10000", "--verbose"]
              resources:
                requests:
                  memory: "120Mi"
                limits:
                  memory: "120Mi"
      ---
      apiVersion: v1
      kind: ConfigMap
      metadata:
        name: komodor-python-script
      data:
        python-script: |-
          import time
          import os
          def start_service():
              initialize_connections()
          def initialize_connections():
              fetch_configuration()
          def fetch_configuration():
              create_connection()
          def create_connection():
              conn_auth()
          def conn_auth():
              raise Exception("Can't perform the requested task - authentication error")
          start_service()
      ---
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        annotations:
          app: main-api
        labels:
          app: users-api
        name: users-api
      spec:
        replicas: 1
        selector:
          matchLabels:
            app: users-api
        template:
          metadata:
            labels:
              app: users-api
          spec:
            containers:
            - env:
              image: python:3.11-alpine
              name: python
              command: ["python"]
              args: ["/usr/share/app/code.py"]
              volumeMounts:
                - name: komodor-python-script
                  mountPath: /usr/share/app/code.py
                  subPath: python-script
            volumes:
            - name: komodor-python-script
              configMap:
                name: komodor-python-script
  displayName: application-deployment
  owner:
    user: admin
```
