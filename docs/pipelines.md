---
title: Pipelines
nav_order: 4
---

# Pipelines
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Download the pipelines
All of the pipelines are stored at [github.com/nadeaulab](https://github.com/nadeaulab).
You can easily clone them into your directory with the Terminal command:
```
git clone https://github.com/nadeaulab/pipelines.git 
```

### How are the pipelines structured?
The `/steps` directory contains individual steps, which only require a single program and are submitted to Compute Nodes separately.
The folder for each technology, such as `/RNA-seq`, contains a variety of pipeline options.
Each one manages the submission of all of the jobs for a specific read or pair of reads.
Finally, a user-created script such as `/example_project/scripts/submit_pipeline.sh` calls the selected pipeline on all of the reads chosen.

### How can I create a project?
You can just copy the `/example_project` directory and customize the script to get started! Here are a few details:

#### Data organization
Your project directory should look something like this:
```
MyProject
  ├── logs
  ├── raw_data  
  ├── results
  └── scripts
```
The `/scripts` folder should contain all of the scripts that you run on the data in `/raw_data`.
The scripts should be configured to write all of the output from the job scheduler to `/logs` and all of the programs’ results to `/results`.
The `/example_project` does this automatically.

#### The submit_pipeline file
This file contains all of the variables that are required by the scripts.
For example, all of the scripts in `/steps` assume that the vCPU variable exists, whereas all of the different pipeline scripts assume that the `results_dir`, `logs_dir`, and `steps` variables exist.

It then recursively calls the selected pipeline on the files described by `reads.txt`.
This file contains an identifier for the read or pair of reads, followed by the path to the actual FASTQ files.

