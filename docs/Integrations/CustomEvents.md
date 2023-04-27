# Custom Events
Using an API call customers can enrich the Komodor timeline with their own custom events and correlate them to the relevant services

## Prerequisites 
- [API key](https://docs.komodor.com//Learn/Create-API-Token.html)

*Please note*: This feature is only available for paying/trial users

## Using the API
### Body 
```
{
    "eventType": "string", 
    "summary": "string", 
    "scope": { 
        "clusters": ["string"],
        "servicesNames": ["string"], 
        "namespaces": ["string"]
    }, 
    "severity": "warning", 
    "details": { 
        "key": "val",
        "key2": "val2"
        ...
    } 
}
```

| Field              	| Type                                  	| Description                                                                    	|
|--------------------	|---------------------------------------	|--------------------------------------------------------------------------------	|
| eventType          	| String                                	| Required, the type of event you'd like to create, limited to 60 chars          	|
| summary            	| String                                	| Required, descipription of the event                                           	|
| scope.clusters     	| List\<String>                          	| Optional                                                                       	|
| scope.serviceNames 	| List\<String>                          	| Optional                                                                       	|
| scope.namespaces   	| List\<String>                          	| Optional                                                                       	|
| severity           	| Enum - Info (default), Warning, Error 	| Optional                                                                       	|
| details            	| Object (key:value pairs)              	| Optional, key:value pairs allowing specifying any additonal categories of data 	|


### Scope 
The scope field allows the user to define the Services to associate the custom event with.

By default, everything is selected (e.g - no scope specified), when specifying a cluster/namespace/service name you are narrowing the scope accordingly (within the field there is an OR condition, between the fields it's AND).  

Examples:  
- By specifying no scope - the evnet will be correlated to all Services on the account level  
- By specifying a list of one or more clusters - the event will be correlated to all Services in those clusters  
- By specifying a list of namespaces - the event will be correlated to all Services in those namespaces (accross all clusters, unless mentioning otherwise)   
- By specifying a list of servicesNames - the evnet will be correlated to those Services  
