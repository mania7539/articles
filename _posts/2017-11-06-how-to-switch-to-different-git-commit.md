---
published: true
---
* Type in the commands as below (bash or cmd)


```bash
# list all commit of the current branch #
$ git log
	# commit 4f940d45eee9282da81a17ab23564f6498d6afef
	# Author: mania7539 <mania7539@gmail.com>
	# Date:   Mon Nov 6 16:06:10 2017 +0800
	# 
	# 	commit 7
	# 
	# 	commit 8
	# 
	# 	commit 9
	# 
	# commit b0220ebecdd055a9821d1c37f150c305d462c1a1
	# Author: mania7539 <mania7539@gmail.com>
	# Date:   Mon Nov 6 15:43:37 2017 +0800
	# 
	# 	commit 6
	# 
	# commit 9148588f5fb278bf5e7d1e4080420a43e37c6dcf
	# Author: mania7539 <mania7539@gmail.com>
	# Date:   Mon Nov 6 15:43:16 2017 +0800
	# 
	# 	commit 5
	#
	# commit ...
	
# switch to specific commit #
$ git checkout [commit-index=b0220eb]
	# use first 6-7 characters of index

# switch to the up-to-date commit in the specific branch #
$ git checkout [branch-name=master]
	# Previous HEAD position was b0220eb... commit 6
	# Switched to branch 'master'
	# Your branch is up-to-date with 'origin/master'.

```


## Which Git Commit Would You Be If Switching To Different Branch?


* Since we are using **_git checkout [branch-name=master]_**
* We should be in the **up-to-date** commit of the branch


```bash
# switch to the up-to-date commit in the specific branch #
$ git checkout [branch-name=master]
	# Previous HEAD position was b0220eb... commit 6
	# Switched to branch 'master'
	# Your branch is up-to-date with 'origin/master'.

```

## Reference
* [Working With Bitbucket Git Repository]({{site.url}}{{site.baseurl}}/working-with-bitbucket-git-repository.html)
* [Working With Git Branch]({{site.url}}{{site.baseurl}}/working-with-git-branch.html)
* [Create Git Repository With Heroku Cloud Service]({{site.url}}{{site.baseurl}}/create-git-repository-with-heroku-cloud-service.html)
