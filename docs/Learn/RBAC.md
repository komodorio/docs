# Role-Based Access Control

## Intro
Komodor allows assigning users with Roles to control their access and permissions (such as what data they can read or what they can modify).

## Komodor Roles
Roles are built from one or more policies.

### Built-in Roles
- Admin - has full permissions on the account
- Viewer - has access to view all resources on the account
- Developer - has access to view all resources and perform basic actions (TODO: link to actions page)  

**Please note** - The built-in roles and policies cannot be modified.

## Komodor Policies
Policies define a set of actions & resources they can performed at.

A policy is built from a list of Statements, formatted as follows:
```
[   
    {
        "actions": [],
        "resources": []
    },
    {
        "actions": [],
        "resources": []        
    }
]
```
### Actions
A list of allowed actions, formatted as follows:  
`action:supported-resource-type`  

List of the supported combinations:

|  Action 	|                                                    Supported Resource Types                                                    	|
|:-------:	|:------------------------------------------------------------------------------------------------------------------------------:	|
|   view  	| * (all)                                                                                                                        	|
|   edit  	| * (all), deployment, statefulset, daemonset, replicaset, jobs, cronjobs, configmap, secrets, services, ingresses               	|
|  delete 	| * (all), deployment, statefulset, daemonset, replicaset, jobs, cronjobs, pvc, pv, storageclasses, secrets, services, ingresses 	|
|  scale  	| deployment, statefulset                                                                                                        	|
| restart 	| deployment, statefulset, daemonset                                                                                             	|
|  manage 	| users, monitors, integrations                                                                                                  	|


**Please note** - The `view:all` permission is required in any policy to allow viewing anything in Komodor, you can limit the allowed access using the Resources clause.

### Resources
A list of resources, formatted as follows:
```
{
    "cluster": "*",
    "namespaces": []
}
```

The <strong>cluster clause</strong> supports specifying a specific cluster or "*" (any).  
The <strong>namespaces clause</strong> is optional and allows specifying a list of one or more namespaces. 

### Policy Examples
1. The following policy allows performing the following actions on resources running in the **kube-system** namespaces on **all** clusters and on namespaces **brain** and **k8s-watcher** on the cluster named **main**  
    - Deletion of Pods  
    - Scaling all supported resource types   
    - Restarting all supported resource types   
```
    [
        {
            "actions": [
                "view:all"
                "delete:pod",
                "scale:*",
                "restart:*",
            ],
            "resources": [
            {
                "cluster": "main",
                "namespaces": [
                "brain",
                "k8s-watcher"
                ]
            },
            {
                "cluster": "*",
                "namespaces": [
                "kube-system"
                ]
            }
            ]
        }
    ]
```

