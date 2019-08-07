---
title: Git
parent: Contributing
nav_order: 2
---

# Git
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### What are git and GitHub?
Git is a program that tracks all of the changes made to a project, which is managed under a special `.git` folder called a repository.
GitHub is used to manage all of the [lab’s repositories](https://github.com/nadeaulab).
This allows multiple people to make their own additions to our service in a clear, documented way.

### Set up git and GitHub
1. [Install git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
1. Type the following into the Terminal:
	```
	git config --global user.email “you@example.edu”
	git config --global user.name “Your Name”
	```
1. [Create a GitHub account](https://github.com/)
1. Type the following into the Terminal:
	```
	ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
	```
1. Copy the public key (\*.pub) in your ~/.ssh folder and paste it under GitHub’s
[SSH keys / Add new](https://github.com/settings/ssh/new) page in the Settings
[<sup>1</sup>](https://help.github.com/en/articles/connecting-to-github-with-ssh)
1. Test your connection by typing the following into your Terminal:
	```
	ssh -T git@github.com
	```

### Git commands
{: .d-inline }
[<sup>2</sup>](https://github.github.com/training-kit/downloads/github-git-cheat-sheet/)
{: .d-inline-block }
* To clone the repository, enter the following into your Terminal:
	```
	git clone git@github.com:nadeaulab/aws-docs.git
	`
* To test your own additions, first create your own branch:
	```
	git branch MyBranch
	```
* To switch between branches:
	```
	git checkout MyOtherBranch
	```
* To both create the branch and switch between branches:
	```
	git checkout -b MyBranch
	```
* To delete a branch:
	```
	git branch -d MyBranch
	```
* Once you have modified or created the files necessary, see the changes with:
	```
	git status
	```
* Stage the modifications for a new commit with:
	```
	git add /path/to/file OR git add .
	```
