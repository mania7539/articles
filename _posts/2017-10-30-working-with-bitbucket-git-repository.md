---
published: true
tags:
  - git
  - bitbucket
---
* Step by step **Cmder** commands  


```bash
$ pip install bitbucket-cli
$ bitbucket create --private --protocol ssh --scm git YOUR_REPO_NAME
    # enter your username and password
$ git remote
	# check if it's a git repository
$ git init
$ git remote
    # check again
$ git remote add [short-name: origin] git@bitbucket.org:mania7539/YOUR_REPO_NAME.git
	# remove current remote repository
    # $ git remote rm [short-name: origin]
    #
$ git add .
	# can check the difference of the updated files with:
    # $ git diff --cached
    # 
    # can undo this command with 
    # $ git reset .
$ git status
    # check the added and modified files 
$ vi .gitignore
	# /build	// this directory should not be ignored
$ git commit -m "first commit"
$ git status
	# check the added and modified files again
$ git push [short-name: origin] [branch-name: video2_2017-11-15]
	# the branch-name should be as the same one as your branch of commit is (normally it's 'master')
	# or you will get error message as below:
	# 	fatal: 'video2_2017-11-15' does not appear to be a git repository
	# 	fatal: Could not read from remote repository.
	#
```

* Discard changes git command

```bash
$ git stash -u
```


## Merge branch after you complete the feature or solve the software issue

* Fast-Forward Merge


```bash
$ git checkout master
	# switch branch from branch-name: 'video2_2017-11-15' to 'master'
$ git merge [new-feature: video2_2017-11-15]
	# merge the last node of 'video2_2017-11-15' to 'master' 
$ git branch -d [new-feature: video2_2017-11-15]
	# delete the branch
    
```

* 3-Way Merge
Someone merge their works into master before you merge your branch

```bash
$ git mergetool
	# It opens a GUI that steps you through each conflict, and you get to choose how to merge. Sometimes it 	# requires a bit of hand editing afterwards, but usually it's enough by itself. It is much better than
    # doing the whole thing by hand certainly.
    #
    # or you can try:
    #
    # $ git config --global merge.conflictstyle diff3
    #
    # 	In addition to the <<<<<<<, =======, and >>>>>>> markers, it uses another ||||||| marker 
    # 	that is followed by the original text.
    #
```


## Solving Error When Pushing to Bitbucket Git Server

* **Git push** got error below:

```
Warning: Permanently added 'bitbucket.org,104.192.143.3' (RSA) to the list of known hosts.
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

* Then try the bash commands with **MINGW64** below:

```bash
$ ssh-add -l
	# Check the connection to your authentication agent

$ ssh-add ~/.ssh/identity
	# Check the connection to your authentication agent
    	# If getting "Could not open a connection to your authentication agent.", then go to the next steps
        
$ ssh-keygen    
$ ll ~/.ssh
	# -rw-r--r-- 1 XDrz 197121  391 十一  2 18:59 id_rsa
	# -rw-r--r-- 1 XDrz 197121  391 十一  2 18:59 id_rsa.pub

```


* Open the **id_rsa.pub** file with text editor and copy paste the contents to a new SSH key in

```
Bitbucket Avatar > Bitbucket Settings > SSH Keys > Add key
```


* **Git push** with similar error below:

```
$ git push origin develop_android-version_jni
	# git@bitbucket.org: Permission denied (publickey).
	# fatal: Could not read from remote repository.
	# 
	# Please make sure you have the correct access rights
	# and the repository exists.
```

* Try to locate the public key with the bash commands below:

```bash
$ ssh -T hg@bitbucket.org
	# hg@bitbucket.org: Permission denied (publickey).

$ ssh-add -l
	# The agent has no identities.

$ ls ~/.ssh/
	# config                   known_hosts              mania7539-Bitbucket      mania7539-Bitbucket.pub 

$ ssh-add ~/.ssh/mania7539-Bitbucket
	# 'mania7539-Bitbucket' is a public key while 'mania7539-Bitbucket.pub' is a private key 

$ git push origin develop_android-version_jni
	# It should work fine now.
    
	# Counting objects: 4280, done.
	# Delta compression using up to 8 threads.
	# Compressing objects: 100% (4168/4168), done.
	# Writing objects: 100% (4280/4280), 6.76 MiB | 530.00 KiB/s, done.
	# Total 4280 (delta 1485), reused 0 (delta 0)
	# ...	
```

<!--
## Reference
**[Read: Create Git Repository With Heroku Cloud Service](https://mania7539.github.io/articles/create-git-repository-with-heroku-cloud-service.html)**
-->
