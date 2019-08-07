---
title: EC2
parent: AWS services
nav_order: 2
---

# EC2
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### What is EC2?
The Elastic Compute Cloud, or
[EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html),
is the main computing service provided by AWS.
Each computer in EC2 is called an instance, and their software is defined by Amazon Machine Images, or
[AMIs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html).
The storage attached to these instances is managed by Elastic Block Storage, or
[EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html).

### Create an EC2 Key Pair
{: .d-inline }
[<sup>1</sup>](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-ec2-keypairs.html)
{: .d-inline-block }
ParallelCluster uses the EC2 service for computing.
For this reason, you need an EC2 Key Pair in the region you are working in.
1. If the .ssh directory is not present in your home directory, enter:
        ```
        sudo mkdir ~/.ssh
        ```
1. To create a key pair, enter the following into your terminal:
        ```
        aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > ~/.ssh/MyKeyPair.pem
        ```
1. To make your key pair private (which is required for creating a cluster), enter
        ```
        chmod 400 ~/.ssh/MyKeyPair.pem
        ```
1. Later, if you wish to delete a key pair, enter the following into your terminal
        ```
        aws ec2 delete-key-pair --key-name MyKeyPair

### Creating an EC2 instance
{: .d-inline }
[<sup>2</sup>](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
{: .d-inline-block }
1. From the management console, navigate to the
[EC2 Management Dashboard](https://console.aws.amazon.com/ec2/) and click on Launch Instance
1. Enter the image ID for the AMI that you want to use - if you want it to be compatible with ParallelCluster, you can choose from one of its prebuilt choices
1. Select an instance type from [AWS’ options](https://aws.amazon.com/ec2/instance-types/)
	1. t2.micro is usually enough, and qualifies for free tier
1. Press Review & Launch, and Launch with the key pair you made earlier during

### Using an instance
{: .d-inline }
[<sup>3</sup>](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)
{: .d-inline-block }
To use ssh or scp, you must know the Public DNS of your instance, which is shown under the Instances menu from the EC2 Management Dashboard
* To ssh into your instance, enter the following into your Terminal:
	```
	ssh -i /path/MyKeyPair.pem ubuntu@ec2-198-51-100-1.compute-1.amazonaws.com
	```
* To copy files from your computer into the instance, enter the following into your Terminal
	```
	scp -i /path/MyKeyPair.pem file ubuntu@ec2-198-51-100-1.compute-1.amazonaws.com:/path
	```
	* Use the -r flag if you are copying an entire directory

### EC2 limits
Every AWS account comes with limits, which are imposed by Amazon to restrict the number of each type of resource that you can create in a region.
To view your limits, click on the “Limits” tab on your
[EC2 Management Dashboard](https://console.aws.amazon.com/ec2/).
You can also request AWS to increase your limit by clicking on “Request limit increase” next to the desired resource.
[<sup>4</sup>](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-resource-limits.html)

### Reserved and spot instances
Regular instances are fairly expensive.
However, you can reduce the cost by using reserved or spot instances.

#### Reserved instances
[Reserved instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-reserved-instances.html)
allow you to get a discount by specifying a specific instance family and the number of hours you will use it ahead of time.
The greater the amount of time you reserve it for, the greater the discount.

#### Spot instances
[Spot instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)
allow you to bid on an instance type.
Usually, this price is much lower than the on-demand rate.
However, if the market price goes above your bid price, you lose your instance and all of the information attached to it.

### Creating an image
1. If your instance is built off of one of the ParallelCluster images, enter the following into the instance:
[<sup>5</sup>](https://aws-parallelcluster.readthedocs.io/en/latest/tutorials/02_ami_customization.html)
	```
	sudo /usr/local/sbin/ami_cleanup.sh
	```
1. Enter the following commands into your instance:
[<sup>6</sup>](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/building-shared-amis.html)
	```
	sudo shred -u /home/ubuntu/.ssh/* /root/.ssh/* /etc/ssh/*_key /etc/ssh/*_key.pub /etc/ssh/ssh_host_*
	shred -u ~/.*history
	history -cw
	```
1. From the Instances menu in the
[EC2 Management Dashboard](https://console.aws.amazon.com/ec2/),
select your instance and stop it (Actions > Instance State > Stop)
1. Create an image from it (Actions > Image > Create Image)
1. Once the image is created, you can delete the instance (Actions > Instance State > Terminate)
1. Make your AMI public so that other people can have access to it by selecting it from the AMIs menu in the EC2 Management Dashboard (Actions > Image Permissions)
1. If you are adding to the lab’s custom AMI, clearly document all of the commands used to customize the instance and update the
[parallelcluster-ami](https://github.com/nadeaulab/parallelcluster-ami) GitHub
	1. Also update this documentation's [Installed Modules](/docs/parallelcluster/installedmodules) page
