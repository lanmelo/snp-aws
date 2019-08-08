---
title: Jekyll
parent: Contributing
nav_order: 4
---

# Jekyll
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

This documentation is stored in the
[aws-docs](https://github.com/nadeaulab/aws-docs) repository,
and it uses Jekyll for generating static pages.
To test your edits to the repository, you can locally host the website on your computer.

### Set up Jekyll
1. Generate a [GitHub token](https://github.com/settings/tokens) and copy the token
1. Enter the following into your Terminal:
[<sup>1</sup>](https://mycyberuniverse.com/fixing-jekyll-github-metadata-warning.html)
	```
	echo ‘export JEKYLL_GITHUB_TOKEN=”...”’ >> ~/.bashrc
	```
1. [Install Jekyll](https://jekyllrb.com/docs/installation/)

### Locally host the website
1. Go to the project’s root directory and enter the following into your Terminal:
	```
	bundle install
	```
1. To host the website, go to the project’s root directory and enter the following into your Terminal:
[<sup>2</sup>](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll)
	```
	bundle exec jekyll serve --watch
	```
	1. It might be useful to instead use a bash function saved to your ~./bashrc file, such as
		```
		function devsite {
			pushd $1 &> /dev/null;
			bundle exec jekyll serve --watch;
			popd &> /dev/null;
		}
		```
