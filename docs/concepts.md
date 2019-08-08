---
title: Concepts
nav_order: 2
---

# Concepts
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### What is the cloud?
The cloud refers to a network of remote servers that delivers computing services over the Internet.
Large companies like Amazon, Microsoft, and Google have massive servers all around the world.
When you use their cloud services, you actually pay to use those servers.
The cloud allows you to avoid having to maintain any of your own computing infrastructure.

#### What is AWS?
Amazon Web Services, or AWS, is the largest cloud provider in the world.
Their services are used for cloud computing at the Sean N. Parker Center.

#### High risk data
{: .d-inline-block }
Warning
{: .label .label-red .m-0 }
AWS is **NOT** approved for any kind of high risk data at the Sean N. Parker Center.
Do not use AWS for any kind of
[protected health information](https://med.stanford.edu/irt/security/hipaa.html).

### What is HPC?
High Performance Computing, or HPC, refers to the practice of combining multiple computers to solve large scientific problems.

#### What is a cluster?
Each computer is called a node, and a cluster is made up of a collection of nodes.
One cluster that you might be familiar with is
[Sherlock](https://www.sherlock.stanford.edu/docs/overview/introduction/),
which is located at Stanford.

#### What are login and compute nodes?
A cluster is made up of login nodes (in ParallelCluster, we call them master nodes) and compute nodes.
Login nodes give you access to a cluster, by connecting to them via SSH.
They are intended only for connecting the user to the cluster.
Compute nodes are more powerful computers, with greater memory and processing power that allows them to run complex, computationally intensive tasks.

#### Login nodes are not for computing
{: .d-inline-block }
Caution
{: .label .label-yellow .m-0 }
Login (or master) nodes should not be used for computationally intensive tasks.
Those should be submitted to compute nodes using job schedulers.

#### What are jobs?
When you want to run a script or program in a cluster, you have to submit it to a compute node.
When you do this, it becomes packaged into a job, which includes both the computational resources being requested and the software that will run on them.
Programs known as job schedulers manage the process of allocating the computational resources needed to execute a job.

### What are pipelines?
Pipelines, or workflows, refer to the chain of transformations that biological data undergoes in bioinformatic analysis.
At each step of a pipeline, a different program or script is executed.
The pipeline combines all of these steps together so that the same analysis can be performed on hundreds or thousands of different samples.
Typically, pipelines are written in Python, R, or Bash scripts.
You should always save your pipelines so that you can show exactly how you performed the analysis of your data.

#### Reusing pipelines
{: .d-inline-block }
Caution
{: .label .label-yellow .m-0 }
When you put a lot of work into creating a pipeline for one project, you might be tempted to reuse the same pipeline for another project.
However, the raw data in each project is unique - it is usually created using different technologies, and for different purposes.
For that reason, you should always tailor your pipelines to the project you are working on.
A standardized pipeline can never replace creating your own scripts that are specific to the decine of that specific experiment.
