---
title: Add members
parent: Organization management
nav_order: 2
---

# Add members
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Add members
{: .d-inline }
[<sup>1</sup>](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts.html)
{: .d-inline-block }
#### If the email has no AWS account linked to it
1. Sign in to the [Organizations](https://console.aws.amazon.com/organizations/) console
1. In the Accounts tab, choose Add account and then choose Create account
1. Enter the name that you want to assign to the account
1. Enter the email address for the owner of the new account
1. Choose Create

#### If the email already has an AWS account linked to it

##### Invite the account
1. Sign in to the [Organizations](https://console.aws.amazon.com/organizations/) console
1. On the Accounts tab, choose Add account and then choose Invite account
1. Enter the email address for the owner of the account
1. Choose Invite

##### Create the OrganizationAccountAccessRole
1. Sign in to the [IAM](https://console.aws.amazon.com/iam/) console for the member account
1. Navigate to Roles and then choose Create Role
1. Choose Another AWS account
1. Enter the 12-digit account ID number of the master account (028482200074)
1. Do not select Require external ID
1. On the Attach permissions policies page, choose the AWS managed policy named AdministratorAccess
1. On the Review page, give the role the name OrganizationAccountAccessRole
1. Copy the new role’s URL to access the member account from the Master account, and copy the Role ARN for a later step
1. Sign in to the [IAM](https://console.aws.amazon.com/iam/) console for the master account
1. Navigate to Policies and then filter for Customer managed
1. Click on the OrganizationAccountAdministratorAccess
1. Click on the Edit policy button and add the Role ARN you copied previously under “Resource”
1. Click on Review policy and then Save changes

### Member account cleanup

#### Give IAM users access to the Billing Console
{: .d-inline }
[<sup>2</sup>](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_billing.html)
{: .d-inline-block }
1. Using the member account’s root access credentials, navigate to [My Account](https://console.aws.amazon.com/billing/home?#/account)
1. Next to IAM User and Role Access to Billing Information, choose Edit.
1. Then select the check box to Activate IAM Access and choose Update.

#### Block S3 public access account-wide
{: .d-inline }
[<sup>3</sup>](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/block-public-access-account.html)
{: .d-inline-block }
1. Assume the OrganizationAccountAccessRole for the desired member account
1. Navigate to the account’s [S3 Console](https://s3.console.aws.amazon.com/s3/buckets/)
1. Click on Block public access (account settings)
1. Click on Edit and select Block all public access

#### Accessing a member account’s budgets
{: .d-inline }
[<sup>4</sup>](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_access.html#orgs_manage_accounts_access-cross-account-role)
{: .d-inline-block }
1. Assume the OrganizationAccountAccessRole for the desired member account
1. Navigate to the account’s [Billing & Cost Management](https://console.aws.amazon.com/billing/home?#/account) console
1. The MasterBudget can only be edited by the Master account, and you can set it to a specific budget and notify the Master account user to track the member’s usage

#### Multi-factor authentication
{: .d-inline }
[<sup>5</sup>](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)
{: .d-inline-block }
1. Navigate to the [My Security Credentials](https://console.aws.amazon.com/iam/home?region=us-east-1#/security_credentials)
page from the right side of the navigation bar
1. Under Multi-Factor Authentication, select Activate MFA and follow the prompts

