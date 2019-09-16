---
title: Add members
parent: Organizations
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
It is always easier to create an account within an AWS Organization than to invite an account to it.
[<sup>1</sup>](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts.html)
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
1. Enter the 12-digit account ID number of the master account
1. Do not select Require external ID
1. On the Attach permissions policies page, choose the AWS managed policy named AdministratorAccess
1. On the Review page, give the role the name OrganizationAccountAccessRole
1. Copy the new role’s URL to access the member account from the master account, and copy the Role ARN for a later step
1. Sign in to the [IAM](https://console.aws.amazon.com/iam/) console for the master account
1. Navigate to Policies and then filter for Customer managed
1. Click on the OrganizationAccountAdministratorAccess
1. Click on the Edit policy button and add the Role ARN you copied previously under “Resource”
1. Click on Review policy and then Save changes

### Member account cleanup

#### Give IAM users access to the Billing Console
This allows usage and budgeting information to be accessed without root access credentials.
[<sup>2</sup>](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/grantaccess.html)
1. Using the member account's root access credentials, navigate to the
[My Account](https://console.aws.amazon.com/billing/home?#/account)
page from the right side of the navigation bar
1. Next to IAM User and Role Access to Billing Information, choose Edit
1. Select the Activate IAM Access check box and choose Update

#### Block S3 public access account-wide
This prevents users from making their buckets public.
They can still share buckets with individual AWS accounts.
[<sup>3</sup>](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/block-public-access-account.html)
1. Assume the OrganizationAccountAccessRole for the desired member account
1. Navigate to the account’s [S3 Console](https://s3.console.aws.amazon.com/s3/buckets/)
1. Click on Block public access (account settings)
1. Click on Edit and select Block all public access

#### Access a member account’s budgets
The MasterBudget can only be edited by the master account, and it can be modified to notify the master account whenever usage exceeds a certain cost.
1. Assume the OrganizationAccountAccessRole for the desired member account
[<sup>4</sup>](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_access.html#orgs_manage_accounts_access-cross-account-role)
1. Navigate to the account’s [Billing & Cost Management](https://console.aws.amazon.com/billing/home?#/account) console
1. Click on Budgets on the left and create a MasterBudget budget if it does not already exist

#### Multi-factor authentication
Multi-factor authentication (MFA) is required for all members of the organization.
[<sup>5</sup>](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)
1. Using the member account’s root access credentials, navigate to the
[My Security Credentials](https://console.aws.amazon.com/iam/home?region=us-east-1#/security_credentials)
page from the right side of the navigation bar
1. Under Multi-Factor Authentication, select Activate MFA and follow the prompts

