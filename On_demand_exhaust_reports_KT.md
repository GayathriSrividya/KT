# Exhaust Jobs Documentation

## Overview
The exhaust jobs are batch processing jobs that generate reports from the Lern platform data. These jobs are designed to handle large volumes of data efficiently and provide insights into user activities, progress, and responses.

## Architecture

### High-Level Components
1. **Job Manager**: Orchestrates the execution of jobs, handles scheduling and retries using Spark.
2. **Data Processor**: Handles the actual data processing and report generation.
3. **Storage Layer**: Stores the generated reports in a structured format.
4. **Security Layer**: Handles encryption and access control for sensitive data.

### Data Flow
1. Job requests are received via API or scheduled triggers (cronjobs).
2. The Job Manager validates and queues the requests.
3. Data Processor fetches the required data from various sources (Cassandra, Redis, etc.).
4. Reports are generated and stored in the designated output paths.
5. Notifications are sent upon job completion.

## Logic and Workflow

## 1. UserInfo Exhaust Job
- **Purpose**: Generates user information reports for collections (courses/batches).
- **Key Features**:
  - Extracts user details like name, email, phone, organization, and location.
  - Handles encrypted fields (email, phone).
  - Validates requests with encryption keys.
  - Outputs reports in CSV format.
- **Output Path**: `/userinfo-exhaust/`
- **Data Sources**:
  - User Profile Service
  - Organization Service
  - Course Enrollment Data

## 2. Response Exhaust Job
- **Purpose**: Generates response data reports for assessments and quizzes.
- **Key Features**:
  - Captures user responses to questions.
  - Includes metadata like timestamps and scores.
- **Output Path**: `/response-exhaust/`
- **Data Sources**:
  - Assessment Service
  - Content Store
  - User Activity Logs

## 3. Progress Exhaust Job
- **Purpose**: Tracks and reports user progress in courses.
- **Key Features**:
  - Monitors completion status of course modules.
  - Includes metrics like time spent and progress percentage.
- **Output Path**: `/progress-exhaust/`
- **Data Sources**:
  - Course Progress Service
  - User Activity Logs
  - Content Metadata

# References


[Workflow](https://project-sunbird.atlassian.net/wiki/spaces/AN/pages/1665302547/Report-Jobs+with+On-demand+data+exhaust+API)

[Microsite with example report structure](https://lern.sunbird.org/use/developer-guide/lms-service/reports/on-demand-exhaust)

[Source code](https://github.com/Sunbird-Lern/data-products/tree/master/lern-data-products/src/main/scala/org/sunbird/lms/exhaust/collection)

[Automation](https://github.com/project-sunbird/sunbird-ed-installer/tree/main/helmcharts/obsrvbb/charts/dataproducts)

[Spark Automation](https://github.com/project-sunbird/sunbird-ed-installer/blob/main/helmcharts/obsrvbb/values.yaml#L359)

[Cronjobs](https://github.com/project-sunbird/sunbird-ed-installer/blob/main/helmcharts/obsrvbb/charts/cronjob/templates/spark-cronjob.yaml#L254)