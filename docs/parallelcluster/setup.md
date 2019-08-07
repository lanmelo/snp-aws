---
title: Set up
parent: ParallelCluster
nav_order: 2
---

# Set up
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Use an IAM user
As mentioned in [Getting started](/aws-docs/docs/getstarted),
IAM users must always be used instead of root access credentials.
For ParallelCluster, the IAM user must have the AdministratorAccess policy attached to it.
[<sup>1</sup>](https://docs.aws.amazon.com/parallelcluster/latest/ug/iam.html#defaults)

### Create an EC2 Key Pair
See [Create an EC2 Key Pair](/aws-docs/docs/awsservices/ec2/#createanec2keypair)

### Install ParallelCluster
{: .d-inline }
[<sup>2</sup>](https://docs.aws.amazon.com/parallelcluster/latest/ug/getting_started.html)
{: .d-inline-block }
ParallelCluster is installed to your computer as a Python package.
1. Enter the following into your Terminal to install:
	```
	sudo pip3 install aws-parallelcluster
	```
1. Enter the following into your Terminal to configure:
	```
	pcluster configure
	```
1. Skip “AWS Access Key ID,” “AWS Secret Access Key,” and “Default region name,” since those were already stored in the system with CLI
1. For the other fields, select one of the options given
1. For “Key Name,” select the one that was created in the previous section

### Update ParallelCluster
ParallelCluster is frequently updated. To update your install, run the following command:

```
sudo pip3 install aws-parallelcluster --upgrade
```

