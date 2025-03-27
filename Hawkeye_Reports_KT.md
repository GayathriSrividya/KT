# Reports CRUD API

The Report Service in Sunbird is designed to facilitate the creation and consumption of reports within user interfaces and applications. It allows for the dynamic rendering and management of reports through configurable settings, ensuring scalability, ease of updates, and flexibility in data visualization.

## Hawkeye Reports

### 1. Data Sources:
   - **Models and Ingestion:**
     - Data models, such as Data, Content, User, and Device, are defined to effectively structure the incoming data.
     - Ingestion specifications (Ingestion Specs) detail the methods and schedules for importing data into the system.
     - Raw telemetry data is collected, providing granular insights into user interactions and system performance.
     - Summaries aggregate raw data, offering high-level overviews for quick analysis.

### 2. DRUID (Analytics Database):
   - **Data Storage and Processing:**
     - Druid serves as a high-performance, column-oriented distributed data store optimized for real-time analytics on large datasets.
     - It ingests data from various sources, including raw telemetry and summaries, enabling fast query responses and complex analytical operations.

### 3. Apache Superset:
   - **Data Exploration and Visualization:**
     - Superset connects to Druid, allowing users to perform interactive data exploration and create dynamic dashboards.
     - It supports a wide range of visualization types, facilitating the representation of data in various formats to suit analytical needs.
     - The internal dashboard provides stakeholders with customizable views of key metrics and performance indicators.

### 4. Data Team:
   - **Ad-Hoc Queries and Publishing:**
     - Data analysts and engineers can execute ad-hoc queries against Druid to extract specific insights.
     - The team is responsible for publishing reports and dashboards, ensuring stakeholders have access to up-to-date and relevant information.

### 5. Jobs:
   - **Scheduled Data Processing:**
     - Jobs are scheduled via APIs to process incoming data, including POST requests containing analytics data.
     - These jobs handle tasks such as data transformation, aggregation, and report generation, ensuring efficient system operation and timely data processing.

### 6. S3/Blob Store:
   - **Report Storage:**
     - Generated reports are stored in scalable storage solutions like Amazon S3 or Blob Storage.
     - Reports are organized by report ID and channel, facilitating easy retrieval and management.
     - Storing reports in formats like CSV and JSON ensures compatibility with various data processing and analysis tools.

### 7. Portal and Dashboard:
   - **User Interface and Reporting:**
     - The portal serves as the user interface, allowing stakeholders to access reports, dashboards, and other analytical tools.
     - Dashboards provide visual representations of data, enabling users to monitor key metrics and make informed decisions.
     - The system ensures that reports are easily accessible, up-to-date, and tailored to the needs of different user groups.

This architecture exemplifies a robust data pipeline capable of collecting, processing, analyzing, and visualizing large volumes of data. By leveraging technologies like Druid and Superset, the system ensures real-time analytics and interactive data exploration, supporting data-driven decision-making across the organization.


# References

[Superset source code](https://github.com/Sunbird-Ed/incubator-superset)

[Superset Deployment](https://github.com/project-sunbird/sunbird-ed-installer/tree/main/helmcharts/obsrvbb/charts/superset)

[More details in Confluence](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/865436288/Reports+Scale)

[Microsite](https://obsrv.sunbird.org/previous-versions/sb-5.0-version/learn/product-and-developer-guide/report-service)

[Automation](https://github.com/project-sunbird/sunbird-ed-installer/tree/main/helmcharts/obsrvbb/charts/dataproducts)

[Cronjob](https://github.com/project-sunbird/sunbird-ed-installer/blob/main/helmcharts/obsrvbb/charts/cronjob/templates/spark-cronjob.yaml#L366)