<!-----

Conversion notes:

* Docs to Markdown version 1.0β33
* Sat Aug 13 2022 23:09:46 GMT-0700 (PDT)
* Source doc: ArgoCD - Komodor integration

----->

# **ArgoCD integration** 

This tutorial demonstrates how to utilize ArgoCD’s external links to seamlessly hop from a specific K8s resource on Argo to its parallel on Komodor.
This is meant to reduce friction and context-swtiching when troubleshooting incidents.

Komodor is a continuous reliability platform for Kubernetes that collects all changes and events across your system, provides a coherent timeline view, and offers actionable insights for remediation.  

### **General**

ArgoCD can generate clickable links to external pages for a resource based on per resource annotation.

 
Adding a Komodor dynamic link to ArgoCD will generate a direct link from an ArgoCD application to the relevant workload in Komodor, based on the Kubernetes workload resources annotation.

Thus providing a way to quickly get the full context of an incident and resolve it end-to-end with minimal effort.

### **Why use Komodor on top of ArgoCD?**



* To resolve incidents in complex and distributed environments you need full context which can only be understood by looking at changes and events over time 
* Komodor provides visibility to all resources and not only ArgoCD managed apps
* Komodor can compliment Argo with more capabilities dedicated specifically for rapid incident response. 


### **Prerequisites**



* Installed ArgoCD
* Installed Komodor 

### **Installation**


1. Add annotations to the requested Kubernetes workload resources 
2. The URL should follow the structure bellow 


        https://app.komodor.com/main/deep-dive/{{account-name}}.{{cluster}}-{{namespace}}.{{service}}


### **Example** 
&nbsp;

![Screen Shot 2022-08-04 at 11 48 48](https://user-images.githubusercontent.com/109901035/185045272-1269b941-1b89-4dce-8049-27472a2d7028.png)

###  **Testing**

1. Open the ArgoCD application details page and make sure that the external link icon is visible for the respective resource 
2. Click on the external link icon to directly hop onto the relevant workload in Komodor.

![Screen Shot 2022-08-04 at 12 01 47](https://user-images.githubusercontent.com/109901035/185045403-b16e62c6-335e-4f57-9aea-f958679ab725.png)


### **Demo**  

https://user-images.githubusercontent.com/109901035/185045498-18569afc-0871-4903-8c7c-dff80fbda1cd.mov



	
