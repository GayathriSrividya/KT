# Flink jobs used in the LMS service of Sunbird Lern:

- Merge User Courses: This job is responsible for merging user-course relationships, which helps in consolidating the user's course data into a more accessible format.

- Relation Cache Updater: This job updates the cache with the relationships between users and their enrolled courses, ensuring fast retrieval of this data for real-time use.

- Activity Aggregate Updater: It aggregates activity data across various courses to ensure that metrics like course progress and completion rates are accurately represented.

- Assessment Aggregator: This job aggregates the assessment data for users, generating summary reports and performance metrics for assessments taken.

- Enrolment Reconciliation: Ensures that users’ enrolments in courses are correctly synchronized and reconciled, tracking their progress and completion statuses.

- Collection Certificate Pre-Processor: It processes data for certificates that are to be issued to users after completing courses or activities.

- Collection Certificate Generator: After the pre-processing, this job handles the final certificate generation, ensuring that users receive the proper certificates for their completed courses or assessments.

# References

[Source Code](https://github.com/Sunbird-Lern/data-pipeline/tree/master/lms-jobs)

[Micro site](https://lern.sunbird.org/use/developer-guide/lms-service/lms-flink-jobs)

[Automation](https://github.com/project-sunbird/sunbird-ed-installer/blob/96d826af805f10a80bd7390e0e5044881a162560/helmcharts/learnbb/charts/flink/values.yaml#L194)
