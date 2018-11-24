# Production Readiness

Before launching a new service or application to production, it SHOULD be reviewed by the team to ensure production readiness and adherence with engineering standards.

Not all categories may be applicable for certain services or applications (e.g. Accessibility for a back-end service).

A pre-launch checklist SHOULD be completed and can be completed in a pre-launch team meeting:

![Production Readiness Whiteboard](../images/production-readiness.jpg)

## Sample Pre-Launch Checklist

| Category                                                                                                                                                                                                                                                   | Completeness (1-10) |
|---------------------------------------------------------------------------------------------|---------------------|
| Documentation [1](documentation.md)                                                         |                     |
| Peer Review [1](peer-review.md)                                                             |                     |
| Logging [1](logging.md)                                                                     |                     |
| Deployment [1](node-lambda.md)                                                              |                     |
| Coding Standards [1](coding-standards.md), [2](naming-conventions.md)                       |                     |
| Testing [1](test-coverage.md)                                                               |                     |
| Accessibility [1](accessibility.md)                                                         |                     |
| Security [1](../security/README.md), [2](../security/oauth.md), [3](../security/secrets.md) |                     |
| Privacy & Data Retention [1](privacy.md)                                                    |                     |
| Monitoring & Alarms [1](alerting.md)                                                        |                     |


## AWS Billing Tags
If your service uses AWS, please add billing tags to your production readiness checklist.  You can read more about the tags on the billing-tags document page.
