---
title: Getting started
nav_order: 2
---

# Getting started
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### What is AWS?
Amazon Web Services, or AWS, is the largest cloud provider in the world.
Their services are used for cloud computing at the Nadeau Lab.

### Creating an account
To use AWS for research at the Nadeau Lab, your AWS account must be a member of the lab’s organization.
You can request that a member account be created for your Stanford email by sending us an
[email](mailto:nadeau-aws@stanford.edu).
If you already have an AWS account tied to that email, then your email must also contain the console login information of an IAM user with the AdministratorAccess policy for that account.
For help in creating this user, see
[Create an administrator IAM user](#create-an-administrator-iam-user).
Remember that all AWS accounts in the organization must have multi-factor authentication enabled.
This can be enabled with the My Security Credentials page from the right side of the navigation bar.

### Why use an administrator IAM?
One important principle of using AWS is that you should never use your account’s root access credentials unless strictly necessary.
The root user login that you first receive when creating an AWS account has maximum privileges.
However, according to the
[principle of least privileges](https://en.wikipedia.org/wiki/Principle_of_least_privilege),
every layer of computation should only have access to the information and resources needed for its purpose, and nothing else.
For that reason, we use Identity and Access Management (IAM) users.
These are entities within your AWS account that have their own associated login credentials and permissions.
Once you create an IAM user with administrator privileges, you should lock away the root access credentials and only use them for modifying root user details.
The organization’s Service Control Policy will block any attempts to use root access credentials for computing or storage management.
[<sup>1</sup>](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html)

#### Give IAM users access to the billing console
{: .d-inline }
[<sup>2</sup>](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/grantaccess.html)
{: .d-inline-block }
This is required to be a member of the lab’s AWS organization.
It allows usage and budgeting information to be accessed without root access credentials.
1. Log onto your [AWS Management Console](https://console.aws.amazon.com) with root access credentials
1. Navigate to the [My Account](https://console.aws.amazon.com/billing/home?#/account) page
1. Next to IAM User and Role Access to Billing Information, choose Edit
1. Select the Activate IAM Access check box and choose Update

#### Create an administrator IAM user
{: .d-inline }
[<sup>3</sup>](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console)
{: .d-inline-block }
1. Log onto your [AWS Management Console](https://console.aws.amazon.com) with root access credentials
1. Navigate to the [IAM Users](https://console.aws.amazon.com/iam/home#/users) page and click on “Add user”
1. Create a username and select both “Programmatic access” and “AWS Management Console access”
1. Under “Set permissions,” select “Attach existing policies directly” and add “AdministratorAccess” to the user
1. Once you create the user, copy the Access Key ID and the Secret Access Key and store them somewhere safe - if you lose these keys, you also lose access to your user

### Using the Command Line Interface (CLI)
{: .d-inline }
[<sup>4</sup>](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
{: .d-inline-block }
The AWS Command Line Interface (CLI) is used to access AWS services from a shell.
To learn more about the different commands you can use with CLI, see the
[AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/index.html).
1. Install CLI by entering the following into your Terminal
	```
	pip3 install awscli --upgrade --user
	```
1. If you type “aws” into the Terminal and you get “command not found” you have to add the directory to your path by entering the following into your Terminal
	```
	echo 'export PATH=$HOME/.local/bin:$PATH' >> $HOME/.bashrc`
	source $HOME/.bashrc
	```
1. Configure CLI by entering the following into your Terminal
	```
	aws configure
	```
1. Follow the prompts, filling in your user data with the Access Key ID and the Secret Access Key from the previous section
1. For “Default region name,” enter “us-east-1”
1. For “Default output format,” enter “json”
