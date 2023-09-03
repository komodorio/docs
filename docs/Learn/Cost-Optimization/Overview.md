# Overview

>Komodor’s advanced cost capabilities are offered as part of Komodor’s paid plans, including 14-day trials.  
>[Learn more about our pricing plans](https://komodor.com/pricing-and-plans/), or [contact us](https://komodor.chilipiper.com/book/me/timi-petrov) to request trial access

Komodor analyzes your cluster resources and consumption and provides 3 main capabilities:   
1. Complete **visibility** into your Kubernetes cost allocation   
2. Actionable optimization via **right sizing recommendations**   

**When clicking on ‘Cost Optimization’, you’ll notice tabs for two different pages:** 
1. <u>Cost Allocation</u> - full visibility into your costs structure from your overall environment to specific clusters, namespaces, or services   
2. <u>Right Sizing</u> - Detailed recommendations based on actual consumption vs. configured requests  

## Prerequisites
- An agent update is required per cluster   
    - Agent version 0.2.42 and above  
    - Metrics enabled   
    - Update command:  
    ```helm repo update; helm upgrade --install k8s-watcher komodorio/k8s-watcher --set metrics.enabled=true --reuse-values```  
    - A relevant notification will appear if the agent isn’t up-to-date  
- To generate valuable, significant analysis & recommendations, we recommend waiting at least 7 days after the agent update to review your data.

**Please Note:** Our calculations are based on default values for CPU & memory monthly prices. If needed, you can modify these values to fit your exact prices. 

## Komodor Attributes
- **Optimization Score:** How optimized your environment is, using a 0%-100% range. Calculated based on current costs, the savings recommended by Komodor, and the savings already applied.   
    - For example, if your current costs are $10k, and Komodor identifies a saving opportunity of 30% ($3k), your optimization score will be 70%.   
- **Share of Allocated Cost:** The % out of the total allocated (requested) costs associated with each row, in the selected scope and timeframe.  



