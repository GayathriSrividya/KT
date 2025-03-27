The Groups Service is a component of the Groups tool on Sunbird. It provides the APIs that allow users to create and manage virtual groups, assign assets to these groups, and review the progress of assets associated with the users. 

- The Group Service is designed as a pluggable component within the Sunbird ecosystem. It is responsible for group-related operations such as creating virtual groups, assigning assets, and monitoring user asset progress. Specifically, the Group Service integrates with several other services:

- User & Org Service: It fetches group member details and system settings by interacting with the UserOrg service. This service is critical for operations that involve managing the members of a group as well as retrieving organization details.

- Notification Service: CRUD operations in the Group Service trigger notifications (e.g., when a group is created) sent via the Notification Service.

- Content Service: It is used to search and retrieve details of activities associated with groups through content queries (such as looking up activity configurations).

- Data Storage and Caching: Cassandra is used as the primary data store for group data while Redis is employed for caching purposes.

- Telemetry: Every API call made within the Group Service generates telemetry data. This data is dispatched (via logstash-logback) to a dedicated Kafka topic for further processing, ensuring that system behavior and interactions are closely monitored.


# References

Screenshots were attached to refer how to create a group

[Microsite](https://lern.sunbird.org/use/developer-guide/groups)


[Source Code](https://github.com/Sunbird-Lern/groups-service/tree/release-7.0.0)

[Postman Collection](https://github.com/Sunbird-Lern/groups-service/tree/release-7.0.0/api-tests/collections)
