---
title: Home
nav_order: 1
---

# Learn computational biology
## This tutorial covers High Performance Computing (HPC), data analysis pipelines, and the Amazon Web Services (AWS) cloud
[Learn more](/aws-docs/docs/concepts){: .btn .fs-5 .mb-md-0 .mr-2 }
[Get started](/aws-docs/docs/getstarted){: .btn .btn-primary .fs-5 .mb-md-0 .mr-2 }

---

### Updates
Current AMI: {{ site.custom_ami }}

### Using the shell
This documentation assumes that you already know how to use a UNIX shell and write shell scripts.
If this is not the case, both
[LinuxCommand.org](http://linuxcommand.org) and the
[Linux Documentation Project](https://www.tldp.org/LDP/Bash-Beginners-Guide/html/index.html) have some beginners' guides.

### [ParallelCluster](/aws-docs/docs/parallelcluster)
ParallelCluster deploys a High Performance Computing (HPC) cluster in the Amazon Web Services (AWS) cloud.
It functions like any other cluster, except it automatically adds nodes as need based off of how many jobs are being submitted.
This means there is no waiting in queues, and you only pay for the computation and storage you use.

### [Pipelines](/aws-docs/docs/pipelines)
When getting started with bioinformatics, a lot of time is spent developing analysis pipelines for different technologies.
By creating shared, standardized pipelines, more time can be focused on interpreting the biologically relevant results from a sequencing technology or assay.

---
#### About
This tutorial was created for the
[Sean N. Parker Center for Allergy and Asthma Research](https://med.stanford.edu/allergyandasthma.html) by
[Lucas Melo](https://github.com/lanmelo)

