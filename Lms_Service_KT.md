# Sunbird Course and Batch Management Service

## Sample Functionalities of LMS Service APIs
The LMS Service APIs can be used for the following functionalities on the platform:

- **Creation of a new batch for an existing/new course:**  
  This enables tracking a cohort of users who are expected to take the course.
  
- **Batch Configurations:**  
  - End date for batch enrollment.
  - Certificate criteria (completion of the course and minimum score of 70% for the course assessment).
  

---

## What is a Course?

A **Course** is any collection that has the attribute. It represents a set of learning activities, lessons, or assessments.

---

## Course Batch

- A **batch** is created to enable users to enroll in a course and consume the content. There is a **1:1 relationship** between a course and a batch, though a course can have multiple batches.
  
- **Batch Role:**  
  - Batches allow the course admin or creator to issue certificates to users after completion.

---

## Who Can Update a Batch?

- **Creator or Mentors** can update the batch.  

### Roles for Batch Creation:
- **Content Creator:**  
  Can create courses and batches for their own course.
  
- **Creator + Course Mentor:**  
  Can create an **open batch** only if the course was created by themselves.
  
- **Course Mentor:**  
  A role alone does not allow creating a batch, but the mentor can be added as one of the **show watchers** for open batches created by the creator.

---

## How is the Batch Status Updated?

- Batch status is updated by the **CourseBatchStatusUpdater**, which runs every 30 minutes to automatically update the batch status.

---

## Batch Metadata

- **StartDate:**  
  The beginning date of the batch. Users can start consuming the course from this date.

- **EndDate:**  
  The end date of the batch, by which time all users must have completed their course.

- **EnrollmentEndDate:**  
  The enrollment deadline. This date cannot go beyond the **endDate**. By default, it is set to one day before the **endDate** if not defined.

- **CreatedBy:**  
  The user who created the batch. Only this user can update the batch.

- **Mentors:**  
  Users who have permission to update the batch.

- **CreatedFor:**  
  The organization for which the batch is created.

- **Status:**  
  - `0` = The batch is not started: **Upcoming Batches**.
  - `1` = In Progress: **Ongoing Batches**.
  - `2` = Batch Ended.

- **EnrollmentType:**  
  - `Open`
  - `Invite-only` (private)

---

## Trackable Collections - Exhaust

The following are the available **exhausts** for a **trackable collection**:

- **Progress Exhaust:**  
  Contains progress-related information for the collection and nested collections, including assessment-related scores. The nested collections and assessments are transposed as columns, so the columns for each collection exhaust file will vary.

- **User Info Exhaust:**  
  Contains additional personal information of the users who have joined the collection. This includes personal details like **Email, Phone number**, etc. Personal information is provided only with the explicit consent of the user.

- **Response Exhaust:**  
  Contains the user responses to each question for all question sets in a trackable collection.

    `Note: Details about these jobs will be shared in Reports section.`
---

## Group Activity Aggregator

The **Group Activity Aggregator** feature fetches and aggregates activity data for a group. It works as follows:

1. **Fetches Group Members:**  
   Retrieves the group members associated with a given group ID.

2. **Retrieves User Activity Aggregates:**  
   It fetches activity aggregates for a specific **activity ID** and **activity type** based on the group members.

3. **Aggregates Data:**  
   Combines the group and user data to construct a response containing aggregated information.

4. **Score Aggregates:**  
   The response contains score aggregates, including **completed count**, **enrollment count**, and **score aggregates**, if the collection includes self-assessments.

### Dependencies:
- This feature has a dependency on the **Groups Service** to get related group information.

---

## Visualization of Group Activity Aggregator Response

The **Group Activity Aggregator** provides a response containing various aggregated activity data, including:

- **Completed Count:** The number of users who have completed a certain activity or course.
- **Enrollment Count:** The total number of users who have enrolled in the group or activity.
- **Score Aggregates:** Includes score averages, max, and min scores for the group in relation to specific activities, assessments, or courses.


## References


[API source code](https://github.com/Sunbird-Lern/lms-service/tree/release-7.0.0)

[Postman Collection](https://github.com/Sunbird-Lern/lms-service/tree/master/api-tests/Collection)

[Exhaust jobs source code](https://github.com/Sunbird-Lern/data-products/tree/master/lern-data-products/src/main/scala/org/sunbird/lms/exhaust)

[Microsite](https://lern.sunbird.org/use/developer-guide/lms-service)