---
title: Public-private networking
parent: ParallelCluster
nav_order: 6
---

# Public-private networking

If you need to create more than five clusters, or if you want to close off the compute nodes from public internet access, it is necessary to implement a public-private networking module.
[<sup>1</sup>](https://github.com/aws/aws-parallelcluster/wiki/Public-Private-Networking)
1. Log onto your [AWS Management Console](https://console.aws.amazon.com)
1. Navigate to the [CloudFormation](https://console.aws.amazon.com/cloudformation/) page and click on “Create Stack”
1. For the Amazon S3 URL, enter: https://s3.amazonaws.com/nadeaulab/lib/PublicPrivateVPC.template.yml" and click next
1. Enter a stack name and continue clicking next to create the stack
1. Click on the “Outputs” tab to view the names of the PrivateSubnet and the PublicSubnet
1. Update the ParallelCluster config file as follows:
	```
	[cluster default]
	. . .
	vpc_settings = public-private
	. . .

	[vpc public-private]
	vpc_id = vpc-[VPC you created]
	master_subnet_id = subnet-[public subnet]
	compute_subnet_id = subnet-[private subnet]
	use_public_ips = false
	```

