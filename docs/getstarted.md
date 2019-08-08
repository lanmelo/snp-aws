---
title: Get started
nav_order: 3
---

# Get started
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Create an account
To use AWS for research at the Nadeau Lab, your AWS account must be a member of the lab’s organization.
You can request that a member account be created for your Stanford email by sending us an
[email](mailto:nadeau-aws@stanford.edu).

If you already have an AWS account tied to that email, then your email must also contain the console login information of an IAM user with the AdministratorAccess policy for that account.

Make sure that your account also has multi-factor authentication enabled.
This can be enabled with the My Security Credentials page from the right side of the navigation bar.

### Administrator IAM
One important principle of using AWS is that you should never use your account’s root access credentials unless strictly necessary.
The root user login that you first receive when creating an AWS account has maximum privileges.

For that reason, we use Identity and Access Management (IAM) users.
These are entities within your AWS account that have their own associated login credentials and permissions.
[<sup>1</sup>](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console)

Once you create an IAM user with administrator privileges, you should lock away the root access credentials and only use them for modifying root user details.
The organization’s Service Control Policy will block any attempts to use root access credentials for computing or storage management.
1. Log onto your [AWS Management Console](https://console.aws.amazon.com) with root access credentials
1. Navigate to the [IAM Users](https://console.aws.amazon.com/iam/home#/users) page and click on “Add user”
1. Create a username and select both “Programmatic access” and “AWS Management Console access”
1. Under “Set permissions,” select “Attach existing policies directly” and add “AdministratorAccess” to the user
1. Once you create the user, copy the Access Key ID and the Secret Access Key and store them somewhere safe - if you lose these keys, you also lose access to your user

### Command Line Interface (CLI)
The AWS Command Line Interface (CLI) is used to access AWS services from a shell.
To learn more about the different commands you can use with CLI, see the
[AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/index.html).
1. Install CLI by entering the following into your Terminal
	```
	pip3 install awscli --upgrade --user
	```
1. If you type “aws” into the Terminal and you get “command not found” you have to add the directory to your path by entering the following into your Terminal
	```
	echo 'export PATH=$HOME/.local/bin:$PATH' >> $HOME/.bashrc
	source $HOME/.bashrc
	```
1. Configure CLI by entering the following into your Terminal
	```
	aws configure
	```
1. Follow the prompts, filling in your user data with the Access Key ID and the Secret Access Key from the previous section
1. For “Default region name,” enter “us-east-1”
1. For “Default output format,” enter “json”

### Regions
AWS services are distributed across multiple Regions.
For example, in the US, there are us-east-1 (N. Virginia), us-west-1 (N. California), and others.
[<sup>2</sup>](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html)
You should try to use us-east-1 for everything, because it is cheaper, has greater support, and contains the lab's shared resources.

