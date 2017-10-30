---
published: true
---
* Step by step Cmder commands  


```bash
$ pip install bitbucket-cli
$ bitbucket create --private --protocol ssh --scm git YOUR_REPO_NAME

$ git remote
	# check if it's a git repository
$ git init
$ git remote
    # check again
$ git remote add [short-name: origin] git@bitbucket.org:mania7539/YOUR_REPO_NAME.git
$ git add .
$ git status
    # check the added and modified files 
$ vi .gitignore
	# /build	// this directory should not be ignored
$ git commit -m "first commit"
$ git status
	# check the added and modified files again
$ git push [short-name] master
	# the shortname should be as the same one as the above command
```


## Reference
**[Read: Create Git Repository With Heroku Cloud Service](https://mania7539.github.io/articles/create-git-repository-with-heroku-cloud-service.html)**
