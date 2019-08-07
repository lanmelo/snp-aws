---
title: Configuring
parent: ParallelCluster
nav_order: 3
---

# Configuring ParallelCluster
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### The config file
You can access your config file using an editor such as `vim` from `~/.parallelcluster/config`
Learn more with ParallelCluster's
[Configuration](https://docs.aws.amazon.com/parallelcluster/latest/ug/configuration.html) documentation.

### Example config file
```
[aws]

[cluster default]
vpc_settings = public
ebs_settings = shared
key_name = MyKeyPair
compute_instance_type = t2.large
max_queue_size = 10
scheduler = slurm
cluster_type = ondemand
custom_ami = {{ site.custom_ami }}
s3_read_write_resource = arn:aws:s3:::nadeaulab*
base_os = ubuntu1604

[vpc public]
vpc_id = vpc-082eb572
master_subnet_id = subnet-453d230f

[ebs shared]
shared_dir = shared
volume_type = st1
volume_size = 500

[global]
cluster_template = default
update_check = true
sanity_check = true

[aliases]
ssh = ssh {CFN_USER}@{MASTER_IP} {ARGS} -i ~/.ssh/MyKeyPair.pem
```

### Config parameters
* `compute_instance_type`: defaults to t2.micro
	* You can choose other instance types for the Compute Nodes
* `max_queue_size`: defaults to 10
	* This determines the maximum number of Compute Nodes that can be created
	* It might have to be reduced to 1 or 5, depending on the instance type being used
	- there are limits to how many instances of each type can be created in each region, although you can request Amazon to increase those limits
* `scheduler`: defaults to sge
	* The options are sge, torque, slurm, or awsbatch
	* Slurm is the same job scheduler that is used in Sherlock
* `cluster_type`: defaults to ondemand
	* If you choose “spot” instead, your nodes will be created using a bidding system
	* This is a lot cheaper, but if the market price goes too high, your node will be deleted, and any work not saved will be lost
* `custom_ami`: defaults to Amazon Linux
	* There are several prebuilt choices for each region, and you can also use the lab’s custom AMI ({{ site.custom_ami }}) which comes with built-in bioinformatics modules
* `s3_read_write_resource`
	* This allows your cluster to access the specified S3 bucket
	* Format: arn:aws:s3:::MyBucketName*
* `base_os`: defaults to alinux
	* The options are alinux, centos6, centos7, ubuntu1404, or ubuntu1604
	* If you are not using the default Amazon Linux, you must update this to the specific OS of the AMI you are using
* `volume_type` and `volume_size`: defaults to gp2 and 20
	* This determines the type and size of the /shared directory 
	* The default gp2 is SSD; st1 is HDD and has a minimum volume_size of 500
* `[aliases]`
	* If you put “-i ~/path/to/EC2-key.pem” at the end of the alias, you will not have to type the path to the key every time you access the cluster

