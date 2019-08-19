---
title: Using clusters
parent: ParallelCluster
nav_order: 4
---

# Using clusters
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### ParallelCluster commands
Learn more with ParallelCluster's
[CLI Commands](https://docs.aws.amazon.com/parallelcluster/latest/ug/commands.html)
documentation.
* To create a cluster, enter the following into your Terminal:
	```
	pcluster create MyCluster
	```
* To update a cluster to a new config file, enter the following into your Terminal:
	```
	pcluster update MyCluster
	```
* To ssh into the cluster, enter the following into your Terminal:
	```
	pcluster ssh MyCluster -i ~/.ssh/MyKeyPair.pem
	```
* To delete a cluster, enter the following into your Terminal:
	```
	pcluster delete MyCluster
	```
* To list all of the currently running clusters:
	```
	pcluster list
	```
* To list the status and IP address of MyCluster:
	```
	pcluster status MyCluster
	```

### Why use Compute Nodes?
Don’t run things directly to the Master Node!
It should be small and underpowered.
Using it for computation clogs it up and makes it difficult to use the entire system.
Instead, submit jobs to the Compute Nodes using the job scheduler specified in your config file.
The more jobs you submit, the more Compute Nodes are created to automatically adapt to the work being done.

### Slurm
[Slurm](https://slurm.schedmd.com/documentation.html)
is a job scheduler used to submit jobs to Compute Nodes, and is also used by Sherlock.
* `sbatch SCRIPT`
	* Submits your bash script to the job scheduler
* `squeue`
	* Shows all of the jobs that are running or waiting in the queue
	* Note: this only shows you the first few letters of each job name;
		if you need more, set an alias to `squeue -o "%.18i %.9P %.20j %.8u %.8T %.10M %.6D %R"` instead
* `scontrol show job [JOBID]`
	* Shows all of the information specific to the specified job
* `scancel [JOBID]`
	* Deletes specified job
* `sinfo -N`
	* Shows the status of the Compute Nodes

### Environment Modules
The custom AMI ({{ site.custom_ami }}) contains multiple programs provided as modules, which are managed using the
[Environment Modules](https://modules.readthedocs.io/en/latest) package.
Although all of the modules are already installed to your instance, you have to load a module before using it.
* `module avail`
	* Lists all of the available modules
* `module load MODULE`
	* Loads the chosen module into your environment
* `module unload MODULE`
	* Unloads the chosen module from your environment
* `module list`
	* Lists the currently loaded modules in your environment
* `module help MODULE`
	* Prints helpful information about using the module
* `module whatis MODULE`
	* Prints what the module does
* `module show MODULE`
	* Prints the specific commands that the Modulefile runs when a module is loaded
* `module purge`
	* Unloads all of the currently loaded modules

See which modules are installed in the custom AMI with the
[Installed Modules](/aws-docs/docs/parallelcluster/installedmodules) page.

### Packages and containers
You can install the
[Conda](https://docs.conda.io/en/latest) and
[Spack](https://spack.readthedocs.io/en/latest)
managers by running the script `/modules/pkg-man-install.sh` in the custom AMI.

### Singularity
[Singularity](https://sylabs.io/guides/latest),
the container platform for HPC, is installed as a module in the custom AMI ({{ site.custom_ami }}).
It is compatible with Docker containers, as well as other resources such as
[DockerHub](https://hub.docker.com).

### Mounts
Only the shared directory (`/shared`) is visible to all of the nodes.
If you want to access files and programs in jobs submitted to the compute nodes, you must store them in the `/shared` directory.

### Shared S3 bucket
The sharedbucket is accessible to all members of the lab's AWS organization.
It contains indexes for all of the modules that require them,
and can be used to collaborate with other member accounts.
Read the [S3 documentation](/aws-docs/docs/awsservices/s3) to learn more.
