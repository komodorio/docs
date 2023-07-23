# Right-sizing
Sizing a micro-service requires running performance testing and constant optimization. Komodor analyzes the actual consumption against the allocated resources and provides an extensive overview of suggested modifications and savings.

Our right-sizing dashboard includes: 
- High-level picture of your current cost recommended cost and the potential saving  
- Visualization of our recommendations against your requests during the last 30 days, for both Memory & CPU  
- Detailed right sizing recommendations per service  
    - The table will only include services in which there is a saving potential  

## When to use Right Sizing
| If                                                                                                                                          | Then                                                                                                                              |
|---------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| You’re looking to cut down significantly increased Kubernetes cloud costs without compromising performance                                  | Choose the perfect optimization strategy for your needs to confidently right size                                                 |
| You (or your teams) are unsure how to configure CPU & memory requests for your containers,  or duplicate requests from existing containers  | Komodor cannot recommend initial requests but can offer adjusted right-sizing recommendations based on actual usage within a week |

## Understanding the right-sizing page
- Our right sizing recommendations are based on the last 30 days   
    - Therefore, expect to see different results vs. your cost allocation page, in which you can set different timelines   
- Your overview data can be scoped to one or more clusters (default: all)  
    - However, you can apply additional filters for the detailed report at the bottom of the page by clicking on ‘Filters’ right above it  
- The right sizing report looks quite similar to the cost allocation report, but there are a few key differences:   
    - This report offers a more granular default view, showing recommendations per service   
    - The CPU (core) and memory (MiB) columns will include both your current status (similar to the Cost Allocation report) and the recommended new requests  

## Komodor’s Optimization Strategies
When making right-sizing recommendations, it’s important to understand your preferences and needs. Choose a specific optimization strategy to ensure our recommendations are based on the right balance between your costs and your resource availability. 

| Strategy Name                             | Description                                      |
|-------------------------------------------|--------------------------------------------------|
| Conservative                              | Prirotizies availability over cost optimization  |
| Moderate - Recommended, default strategy  | A mixed, balanced strategy                       |
| Aggressive                                | Prioritizes cost optimization over availability  |