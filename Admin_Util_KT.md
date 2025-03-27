# Referred as Admin util or API manager util

# Main Purpose
Wrapper for Kong Admin API, providing a general signing service for generating JWT tokens (RS256). The service should be placed behind an API gateway and not exposed directly to the internet.

# Key Components
- **TokenSignStep**: Handles JWT token generation.
- **RegisterCredentialStepChainV2**: Manages credential registration in Kong.
- **ConsumerController**: Handles API endpoints for consumer operations.

# Security Features
- JWT token generation with the RS256 algorithm.
- Key management system for private/public key pairs.
- Integration with Kong for API management.

# Setup Requirements
- Requires key pairs for JWT token generation.
- Configuration through `application.properties`.
- Integration with Kong gateway.

# References

Postman collection to generate refresh token will be attached

[API spec](https://lern.sunbird.org/use/developer-guide/user-and-org-service/apis/api-management-service)
[Microsite](https://lern.sunbird.org/use/developer-guide/user-and-org-service/apis/api-management-service)