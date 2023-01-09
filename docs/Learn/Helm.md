# HELM

## Overview
// TODO: Use https://github.com/komodorio/helm-dashboard to build this section

## Pre-requisites 
### Agent flags/permissions
// TODO: Add explaination for each flag + which permissions  
- watcher.resources.secret=true  
- watcher.enableHelm=true   
- helm.enableActions=true  

### Upgrade command
// TODO: Check reuse-values
`helm upgrade --install k8s-watcher komodorio/k8s-watcher --create-namespace --set apiKey=YOUR_API_KEY_HERE --set watcher.clusterName=CLUSTER_NAME --set watcher.resources.secret=true --set watcher.enableHelm=true --set helm.enableActions=true`

## Releases
// TODO: 
## Helm Actions
// TODO: Add relevant actions (upgrade)
## Repositories
// TODO: Flow to add a repository
// TODO: Explain how the flow works (in terms of updating the agent with the relevant repos)



