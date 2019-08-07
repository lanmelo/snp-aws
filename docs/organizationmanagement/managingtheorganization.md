---
title: Managing the organization
parent: Organization management
nav_order: 2
---

# Managing the organization
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Service Control Policies (SCPs)
[Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scp.html)
are used to manage which actions organization members can take.
You can view them under the Policies tab in the
[Organizations](https://console.aws.amazon.com/organizations/) console,
and you can attach or detach them from all accounts (Root) under the Organize accounts tab.

### CloudTrail
[CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
is a service that is used to track all of the actions that all members take, down to the object level.
The organization has a trail called OrganizationTrail, which saves its logs to the S3 bucket
[snp-logs](https://console.aws.amazon.com/s3/buckets/snp-logs/AWSLogs/o-jmqx7czvm0/028482200074/CloudTrail/?region=us-west-1).

### Artifact
Artifact is a service that is used to accept the Business Associate Addendum (BAA) with Amazon Web Services to allow PHI to be stored and analyzed with AWS Services.
You can view the agreement by navigating to the
[Artifact](https://console.aws.amazon.com/artifact)
and clicking on the Agreements tab, and then the
[Organization agreements](https://console.aws.amazon.com/artifact/home?region=us-west-1#!/agreements?tab=organizationAgreements) tab.
