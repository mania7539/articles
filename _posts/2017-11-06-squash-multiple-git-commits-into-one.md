---
published: true
tags:
  - git
  - bitbucket
---
* Type in commands as below for completing **multiple git commits** and **_push_**

```bash	
$ mkdir branch
$ cd branch

# initialize git #
$ bitbucket create --private --protocol ssh --scm git [YOUR_REPO_NAME=branch]
$ git remote
$ git init
$ git remote
$ git remote add git@bitbucket.org:mania7539/[YOUR_REPO_NAME=branch]

# edit file and commit for 3 times" #
$ echo add 1 > main.txt
$ git add .
$ git commit -m "commit 1"
$ echo add 2 >> main.txt
$ git add .
$ git commit -m "commit 2"
$ echo add 3 >> main.txt
$ git add .
$ git commit -m "commit 3"

# push 1 time #
$ git push --set-upstream origin master
```

* You can see the result from my bitbucket repository due to push

![commit-3_push-1.png]({{site.url}}{{site.baseurl}}/images/commit-3_push-1.png)



## How To Squash The Separate Commmits Into One Then Push? (Can only rebase in local)


* Type in commands which are similar as previous one, but an additional **_git rebase -i_**


```bash
# edit file and commit for 3 times" #
$ echo add 7 > main.txt
$ git add .
$ git commit -m "commit 7"
$ echo add 8 >> main.txt
$ git add .
$ git commit -m "commit 8"
$ echo add 9 >> main.txt
$ git add .
$ git commit -m "commit 9"

# check status #
$ git status
	# On branch master
	# Your branch is ahead of 'origin/master' by 3 commits.
	#  	(use "git push" to publish your local commits)
	# nothing to commit, working tree clean

# rebase - pick and squash #
$ git rebase -i
```

* It will show a rebase interactive editor as below
* Change the 2nd, 3rd line start from **_pick_** (which is the default command) to **_squash_**

![rebase_pick-squash.png]({{site.url}}{{site.baseurl}}/images/rebase_pick-squash.png)


* Then the commit message editor will show up as below for you to edit commit message
* Enter **_:x_** to save edit and complete the commit

![rebase_commit-combine-message.png]({{site.url}}{{site.baseurl}}/images/rebase_commit-combine-message.png)


* **_git push_** after rebase and previous steps

```bash	
# check status #
$ git status
	# On branch master
	# Your branch is ahead of 'origin/master' by 1 commit.
  	#	(use "git push" to publish your local commits)
	# nothing to commit, working tree clean
    
# push 1 time #
$ git push origin master
	# Counting objects: 3, done.
	# Delta compression using up to 8 threads.
	# Compressing objects: 100% (2/2), done.
	# Writing objects: 100% (3/3), 268 bytes | 0 bytes/s, done.
	# Total 3 (delta 0), reused 0 (delta 0)
	# To bitbucket.org:mania7539/branch.git
   	# b0220eb..4f940d4  master -> master
```

* Now you will get **only ONE commit** which is pushed in the repository

![bitbucket_rebase-result.png]({{site.url}}{{site.baseurl}}/images/bitbucket_rebase-result.png)


* Note: commit 4, 5, 6 is due to my incorrect manipulations, the commands above will work like a charm

<!--
## Reference
* [Working With Bitbucket Git Repository]({{site.url}}{{site.baseurl}}/working-with-bitbucket-git-repository.html)
* [Working With Git Branch]({{site.url}}{{site.baseurl}}/working-with-git-branch.html)
* [Create Git Repository With Heroku Cloud Service]({{site.url}}{{site.baseurl}}/create-git-repository-with-heroku-cloud-service.html)
-->
