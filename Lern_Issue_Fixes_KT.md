https://project-sunbird.atlassian.net/browse/SBCOSS-96?atlOrigin=eyJpIjoiNGE5NjYxOGYzMTU0NDY3ZjgxNDAzOWZhNDJkMzc5ZTgiLCJwIjoiaiJ9

This issue occurred because the NodeBB plugins were not enabled.
To fix this, we need to port forward NodeBB, log in as an admin, and the NodeBB admin password can be found [here](https://github.com/project-sunbird/sunbird-ed-installer/blob/96d826af805f10a80bd7390e0e5044881a162560/helmcharts/edbb/charts/nodebb/configs/env.yaml#L6)

After logging in, we need to enable the plugins. Then, within the UI, we will need to restart and rebuild the application using the UI itself.

---

https://project-sunbird.atlassian.net/browse/SBCOSS-175?atlOrigin=eyJpIjoiNWZlNTEzZjZkNWFjNDU2ZTg0YWQyNDQzOTVhMTZiZmMiLCJwIjoiaiJ9

This issue needs to be checked in multiple places. First, check the enrollment list API response in the UI as the course owner. If the consumption status is in progress (or 0 or 1), even though a certain user has completed the course, further investigation is required.

The workflow will be as follows:

Creator → creates course → sends for review (reviewer) → publishes course → creates batch → adds certificate.

User → joins batch → consumes course.

Activity aggregator job → updates user activity → sends request event to Kafka topic → {{env}}.issue.certificate.request.

Certificate preprocessor job → processes and sends event to Kafka topic → {{env}}.generate.certificate.request.

Certificate generator job → reads certificate template → generates certificate → calls certificate sign API to sign the certificate → stores in ES index trainingcertificate.



[Reference](https://lern.sunbird.org/use/developer-guide/lms-service/architecture/code-flow)

Potential Issues:

ES Index Schema

The Registry service is supposed to generate schemas in the ES index schema.

However, because the Registry pod doesn't wait for the Elasticsearch pod, it exhausts retries and fails to generate schemas. This issue has been fixed.

[JIRA](https://project-sunbird.atlassian.net/browse/SBCOSS-188?atlOrigin=eyJpIjoiZWVhYzRmMzdiMWYwNDM2MDg5ZjlkYTVmNjk5MTlhOTIiLCJwIjoiaiJ9)
[Automation](https://github.com/project-sunbird/sunbird-ed-installer/blob/main/helmcharts/learnbb/charts/registry/templates/deployment.yaml#L32)


- an entity called PublicKey need to be generated
[Automation](https://github.com/project-sunbird/sunbird-ed-installer/blob/main/terraform/azure/template/install.sh#L55)

The certificate sign ConfigMap should have the secret properly parsed.

It will be mounted as config.json inside /etc/signer//config.json (the double slash is intentional, not a typo).

Verify all of these, and restart all concerned pods. You should see the certificate generated.

---