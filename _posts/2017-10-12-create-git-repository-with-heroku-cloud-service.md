---
published: true
---
*Step by step bash commands  


```bash
$ heroku create
	# will get a new git repository url
	# first need to register an heroku account and install heroku 
	sudo add-apt-repository "deb https://cli-assets.heroku.com/branches/stable/apt ./"
	curl -L https://cli-assets.heroku.com/apt/release.key | sudo apt-key add -
	sudo apt-get update
	sudo apt-get install heroku

$ git remote
	# check if it's a git repository
$ git init
$ git remote
    # check again
$ git remote add [short-name] [git-repository-url]
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
