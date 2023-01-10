# HELM

## Overview
As part of Komodor vision of helping Kubernetes users to navigate and troubleshoot their clusters, Komodor provides an extensive UI to view and manage installed Helm charts, and see their revision history and corresponding k8s resources. It also allows performing simple actions like rollback to a previous revision or upgrading to a newer version.

Some of the key capabilities are:  

- Multiple clusters support  
- See all installed charts and their revision history   
- See manifest diff of the past revisions   
- Browse k8s resources managed by the chart   
- Easy rollback or upgrade version with a clear and easy manifest diff   

## Pre-requisites 
### Agent permissions/values
In order to add those capabilities, the Komodor agent has to have permission to read and manipulate secrets.
To add those permissions, enable the following values on the helm chart:  

- **watcher.resources.secret=true** - allows Komodor agent to send secrets to the Komodor SaaS (all secrets are redacted by default)  
- **watcher.enableHelm=true** - allows Komodor agent to send Helm-related secrets without redaction  
- **helm.enableActions=true**  - adds relevant permissions to the Komodor agent to allow performing various helm-related actions (manipulation of secrets)  


### Upgrade command
// TODO: Check reuse-values
`helm upgrade --install k8s-watcher komodorio/k8s-watcher --create-namespace --set apiKey=YOUR_API_KEY_HERE --set watcher.clusterName=CLUSTER_NAME --set watcher.resources.secret=true --set watcher.enableHelm=true --set helm.enableActions=true`

## Releases
// TODO: 
## Helm Actions
// TODO: Add relevant actions (upgrade)
## Repositories
To enable upgrading HELM charts directly from Komodor you have to add the HELM repositories where you charts reside.

Komodor will automatically detect available upgrades and will suggest those through the UI

Adding a repository: 

- Enter the Repositories tab on the HELM page in Komodor  
- Click Add Repository  
- Specify the Repository Name, URL and clusters to associate those repositories to  
- Save the repository  

Behind the scenes, the Komodor Agent will install those repositories and will use them to initiate the relevant commands. 



