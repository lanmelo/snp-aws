---
title: Add modules
parent: Contributing
nav_order: 3
---

# Add modules
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Create a module
1. You should first try installing the module into a new instance to identify all of the dependencies required for the module
1. When adding a module to a custom AMI, it is best to download the source files to `/modules/src` and install the program to `/modules/bin` from source or binary, instead of using a package manager
	1. See `/modules/install/python-packages.sh` and `r-packages.sh` for how to install Python and R packages and libraries
1. Save all of the commands required to install the program to `/modules/install`, and all dependencies (installed with `sudo apt-get install`) to `/modules/ami-setup.sh`
1. Under `/modules/modulefiles`, create a directory for your program
1. In your program’s directory, create a file (known as a Modulefile) with the same name as the version number
1. Fill in the Modulefile like the [example below](#example-modulefile)
	1. `prepend-path VARIABLE VALUE`: prepends the value to the start of the existing environment variable
	1. `setenv VARIABLE VALUE`: creates a new environment variable with the specified value
	1. `prereq MODULE`: a module that must be loaded in order to load the module you are making
	1. `conflict MODULE`: a module that cannot be loaded in order to load the module you are making
	1. `set-alias SHORTCUT COMMAND`: creates a new shortcut for accessing a specified command - if the command contains spaces, enclose it in double quotes
1. Always add the module as a conflict to itself - when newer versions are installed, it is clearer to the user which one is currently being used
1. Create a .version file like the [example below](#example-version-file) in the same directory as the Modulefile
	1. Replace the numbers in quotes with the name of your Modulefile
	1. This determines which of the versions is the default (usually the most recent)
1. Use [Creating an image](/aws-docs/docs/awsservices/ec2#creating-an-image) to update the custom AMI
1. If your module also depends on the creation of specialized indexes, add them to the
[nadeaulab bucket](https://s3.console.aws.amazon.com/s3/buckets/nadeaulab) and update the
[bucket-lib](https://github.com/nadeaulab/bucket-lib) repository

### Example modulefile
```
#%Module 1.0

proc ModulesHelp { } {
    
    puts stderr "Tophat v2.1.1"
    puts stderr "Spliced read mapper for RNA-seq"
    puts stderr "Note: Requires bowtie2 and samtools"
    puts stderr "For help enter 'tophat' in the command line"

}

module-whatis    "Spliced read mapper for RNA-seq"

prepend-path    PATH            /modules/src/tophat-2.1.1.Linux_x86_64

prereq       	samtools

prereq        	bowtie2

conflict        tophat
```

### Example .version file
```
#%Module 1.0

set ModulesVersion "2.1.1"
```
