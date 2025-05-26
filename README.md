Risk Identified: 
The manual process to fetch and compare product and transaction timestamps took approximately 16–18 hours (2 full working days) for each run. It involved repetitive tasks such as calling APIs, extracting timestamps, and comparing product activity and transaction data. This manual work was time-consuming, prone to human error, and not scalable when dealing with large volumes of data (100,000+ events). As a result, it was difficult to consistently and quickly identify when card transactions were processed on outdated product versions.  

Solution Implemented: 
To address this, I built an automation script using GoLang. The script authenticates and connects to the Event API to retrieve the last posted timestamp for each product. It then fetches related Card Numbers(CMs) and uses those to call the Profile API to get PT (Product Timestamp) effective dates. The script compares and classifies the timestamps into three categories: identical, near-identical, and clearly different. This classification helps in identifying outdated product usage in transaction processing.

Automation Features: 
The script can handle bulk events (100,000 to 1,000,000+), making it scalable and reliable. It is designed to be modular and can be reused with minor changes for other use cases, such as fetching all CMs for a product or extracting payload specific data from bulk broken events.

Before Automation: 
~2 days (16–18 hours) of manual effort per task, supporting only ~10,000 events. Required full-time analyst effort. Accuracy was moderate due to manual validation.

After Automation: 
Now takes ~30 minutes for the same task. Supports 100,000 to over 1,000,000 events. No manual intervention needed. Accuracy is significantly improved due to automated data comparison.

Operational Impact: 
Approximately 96% time saved. 100% of manual work eliminated for this task. Frees up analysts to focus on higher-value work. The script improves speed, accuracy, and scalability. It also supports faster root cause analysis and can be used across multiple usecases.
