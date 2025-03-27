# User and Org Service - Knowledge Transfer Document

## Overview
The User and Org Service is a core component that manages user, organization, and location information in the system. This document provides a comprehensive understanding of its architecture and components.

## Core Components

### 1. Service Components
- **UserOrg-service**: Built using Play Framework
  - Key Modules:
    - Request/Error Handlers
    - Akka Integration
    - Authentication
    - Controllers
    - Filters (AccessLog, CustomFilter)
    - Application Setup
    - Actor Binding

---

### 2. Key Management and Validation
- **KeyManager**: Handles public keys for JWT token
- **Validator**: Performs profile user type and location validation

---

### 3. Data Storage
- **Cassandra**: In the UserOrg service, Cassandra is used as the primary data store. Before setting up the service, a Cassandra migration (executed via the sunbird-utils migration tool) is performed to create the necessary tables in the sunbird keyspace. The various tables in Cassandra (e.g., user, organisation, user_lookup, etc.) support the storage and retrieval of user and organizational data needed by the service.
- **Elasticsearch**: Elasticsearch in the UserOrg service is utilized as a secondary data store. It is responsible for storing and indexing various data types such as user details, userfeed data, user notes, organization information, and location data. Specifically, the service uses several Elasticsearch indices including:

  - userv3: Stores user data (mapped to user_alias)

  - userfeed: Stores user feed data

  - usernotes: Stores user notes

  - orgv3: Stores organization data (mapped to org_alias)

  - location: Stores location data

  This use of Elasticsearch enhances the performance of search operations by efficiently indexing the data stored in the primary data store (Cassandra).
- **PostgreSQL**: For keycloak. To storage federated user data. Also stores reports metadata.
- **Redis**: In the UserOrg service, Redis is utilized for caching user data. The service uses the User Cache Updater Flink job to de-normalise the user data and store it in Redis. This cached data includes user details metadata, where the Redis key is typically the UUID of the user.

---

### 4. Authentication & Authorization
- **Keycloak**: In the UserOrg service, Keycloak is used for user authentication. This means that all user authentication processes are handled by Keycloak, ensuring secure access and identity verification within the service.

- **Channel-service**:In the context of the UserOrg service, the channel service is used to map and manage the channels associated with organisations. When a tenant organisation is created, a channel must be assigned and registered via the channel API in the content-service. This registration links the organisation’s ID with a channel ID/code, which is then used by the content-service to manage properties such as content, framework. Essentially, while the UserOrg service handles user and organisation details, the channel service in the content-service maintains and validates the channel configuration and its associated properties.

  For non-tenant organisations, an existing tenant’s channel is referenced internally to establish the necessary mapping.

---

## Data Flow and Processing

### 1. Kafka Topics Integration
- T1 → "{env}.telemetry.raw"
- T2 → "{env}.lms.user.account.merge"

## Core Entities


### 1. Location Management
- Supports geographical hierarchy:
  - State
  - District
  - Block
  - Cluster

---

### 2. Organisation Hierarchy

- Tenant Organisation: This is an entity in the UserOrg service against which all users are mapped. A tenant organisation must have a unique channel and slug (a URL-compatible abbreviation of the organisation name). A default tenant organisation known as the custodian org is created during setup. The tenant organisation is also registered with the content-service, meaning its channel is not only unique but is used for further content and framework mappings in Sunbird Ed.

- Non-Tenant Organisation: These organisations are created by referring to an existing tenant's channel. They do not have their independent tenant properties but are internally mapped to a tenant organisation by specifying the tenant's channel. In this case, the channel of a non-tenant organisation is a reference or association to an already registered tenant org, and for applications like Sunbird Ed, this channel relation is not used directly.

Both these types are used to manage different organisational setups and associations in the UserOrg service, each with its own specific set of rules regarding channel mapping and user association.

---

### 3. Organisation Types

In the UserOrg service, organisation types are stored as integer values where each type is represented by a bit position. For example, the system uses bit positions to indicate whether an organisation is a board, school, or content organisation. According to the documentation:

- Bit 0 is used to indicate that the organisation is a board.

- Bit 1 is used to indicate that it is a school.

- Bit 2 is used to indicate if the organisation can create content (content organisation).

- Bit 3 is mentioned again for board.

This configuration results in specific integer values for each type. For instance, the value for a board is given as 5, and for a school it is 2.

---

### 4. User Categories
- **LUA (Logged in User)**:
  - Requires email/phone for login
  - Full system access
- **MUA (Managed User)**:
  - No direct login credentials
  - Accessed through LUA credentials
  - Limited profile functionality
  - This might involve scenarios such as provisioning user credentials by an administrator, controlling access through centralized policies, or managing users in an educational environment like Sunbird Lern.

---

### 5. SSO user:
  - An SSO user in the context of Sunbird is a user who logs into the system through a Single Sign-On mechanism. This means that instead of using separate login credentials for Sunbird, the user is authenticated via an external, trusted system that provides a secure token (for example, a JWT).

  - When using SSO, a custom authentication page from the tenant system handles the initial authentication. After verifying the credentials externally, it redirects the user to the Sunbird SSO URL along with the user’s token. If the user already exists in the Sunbird system under a specified tenant, they are automatically logged in. If the user is not found, they may be prompted to provide additional details (e.g., a phone number) to create a new account, after which the login process continues seamlessly.

---

### 6 User roles:
The following roles are available in the system for managing different responsibilities and access levels:

  - Course Mentor
  - Content Reviewer
  - Program Designer
  - Report Admin
  - Org Admin
  - Book Creator
  - Book Reviewer
  - Report Viewer
  - Public
  - Program Manager
  - Content Creator

## System settings
  System settings refer to the configurable options and parameters within a system that allow an administrator to manage and adjust the behavior of the system for various purposes. The provided context shows that there are specific API endpoints such as /data/v1/system/settings/set and /data/v1/system/settings/list that are used to configure and retrieve settings. Additionally, the context mentions the role of a System Administrator in using these settings to configure the system.
  The post API will be used to create update the settings and the get API will be used to retrieve the settings.
  After each call, we might need to refresh cache in user org service.

## OTP Management
  The OTP APIs provided are:

  /otp/v1/generate: An endpoint for generating OTPs.

  /otp/v1/verify: An endpoint for verifying OTPs.

## Data Sync APIs
  the data synchronization endpoint is designed to work with data coming from a primary data store and being synchronized to a secondary data store. Cassandra is used as the primary data store and ElasticSearch is used as the secondary data store.
  Curl will be available in the user org postman collection.
  [Source Code](https://github.com/Sunbird-Lern/userorg-service/blob/master/controller/app/controllers/sync/SyncController.java)

## References 

[Postman collection](https://github.com/Sunbird-Lern/userorg-service/tree/master/api-tests/Collections)

[User org Microsite](https://lern.sunbird.org/use/developer-guide/user-and-org-service)