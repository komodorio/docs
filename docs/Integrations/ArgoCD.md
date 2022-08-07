<!-- Output copied to clipboard! -->

<!-----

Yay, no errors, warnings, or alerts!

Conversion time: 0.472 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β33
* Sat Aug 06 2022 12:09:45 GMT-0700 (PDT)
* Source doc: ArgoCD - Komodor integration
----->


This tutorial demonstrates how to integrate ArgoCD external link to the Komodor application for using Komodor as a centralized troubleshooting platform that allows users 

gain effectively investigate Kubernetes issues providing a clear understanding of all events and historical context across a timeline. \
 \
 \


**General**

ArgoCD allows adding an external link to the Komodor service based on the Kubernetes workload resources annotation to extend Argo’s functionality

 \
Adding A Komodor dynamic link to ArgoCD will generate a direct link from an ArgoCD application to the relevant workload in Komodor.

Thus providing a quick way to get a clear understanding of the relevant context on the Komodor timeline.


### **Prerequisite**



* Installed ArgoCD
* Installed Komodor

**Installation**



1. Add annotations to the requested Kubernetes workload resources 
2. The URL should follow the structure bellow \

![Screen Shot 2022-08-04 at 11 48 48](https://user-images.githubusercontent.com/109901035/183279853-213a4b1f-5d04-4cc4-8a22-dccc31374774.png)


**Example**

  **Testing**



1. Open the ArgoCD application details page and make sure that the external link icon is visible for the respective resource 

![Screen Shot 2022-08-04 at 12 01 47](https://user-images.githubusercontent.com/109901035/183279888-da169dc7-92ab-4fe0-a884-810810116d4a.png)

2. click on the external link icon to get directly to relevant workload in Komodor.
