
In Sunbird, the **State Admin Report (User Consent Report)** and the **Geo Report** are essential administrative tools that provide insights into user consent preferences and geographic distribution, respectively. Here's a more detailed overview of each:

### **1. State Admin Report (User Consent Report):**

This report offers a comprehensive view of user information organized by their consent preferences, aiding in understanding user demographics and ensuring compliance with consent regulations. Key features include:

- **Organizational Breakdown:** The report is structured to provide user details and consent information organized by organization name, facilitating easy analysis of consent data across different organizational units.

- **Data Generation:** The `StateAdminReportJob` generates this report, producing a folder named `declared_user_detail` that contains CSV files with user-declared consent and personal details.

- **Data Provider:** The report utilizes data from the `user_declaration` table, ensuring that the consent information is up-to-date and accurate.

### **2. Geo Report:**

The Geo Report provides insights into the geographic distribution of users, assisting administrators in understanding regional engagement and planning targeted interventions. Key aspects include:

- **Geo-Summary Data:** The report includes a `geo-summary` that shows the number of schools, districts, and blocks within a particular organization, helping to identify regional patterns and needs.

- **Geo-Summary by District:** It also provides a `geo-summary-district` that offers data with respect to each district, detailing the number of blocks and schools, which is crucial for district-level planning and analysis.

- **Data Generation:** The `StateAdminGeoReportJob` generates this report, creating three folders in Azure Blob Storage: `geo-detail`, `geo-summary`, and `geo-summary-district`. These folders contain CSV and JSON files with channel-wise data, facilitating detailed geographic analysis.

By leveraging these reports, Sunbird administrators can gain valuable insights into user consent behaviors and geographic distribution, enabling informed decision-making and effective platform management.

### **3. User Cache Indexer Job:**

While not a traditional report, the **User Cache Indexer Job** plays a vital role in maintaining the efficiency of user data retrieval. It ensures that user data is indexed correctly, facilitating quick access and updates. This job is essential for:

- **Data Indexing:** Ensuring that user data is indexed for efficient retrieval, supporting the performance of various reports and enhancing the platform's responsiveness.

- **Scheduled Execution:** Configured as a cron job, it runs at specified intervals to keep the user data index up to date.

This job is part of the administrative tools available in Sunbird Ed, contributing to the platform's overall performance and data management.

### **Accessing and Managing Admin Reports:**

To access these reports, administrators can navigate to the 'Manage' section within the Sunbird Ed platform, where reports are fetched from Azure Blob storage and displayed. Administrators can view details and download reports in CSV format for further analysis. Additionally, these reports can be scheduled and automated using cron jobs, ensuring timely and regular data updates.


# References

 
[Workflow](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/2961211401/Org-Admin+Reports)

[Microsite with example report structure](https://lern.sunbird.org/use/developer-guide/user-and-org-service/reports/standard-exhaust/state-admin-geo-report)

[Source code](https://github.com/Sunbird-Lern/data-products/tree/master/lern-data-products/src/main/scala/org/sunbird/userorg/job/report)

[Automation](https://github.com/project-sunbird/sunbird-ed-installer/tree/main/helmcharts/obsrvbb/charts/dataproducts)

[Spark Automation](https://github.com/project-sunbird/sunbird-ed-installer/blob/main/helmcharts/obsrvbb/values.yaml#L359)

[Cronjobs](https://github.com/project-sunbird/sunbird-ed-installer/blob/main/helmcharts/obsrvbb/charts/cronjob/templates/spark-cronjob.yaml#L208)