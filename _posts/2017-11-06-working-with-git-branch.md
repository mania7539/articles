---
published: true
tags:
  - git
  - bitbucket
---
* Type in commands in console (bash or cmd)

```bash
# create new branch #
$ git checkout -b [new-branch-name=arc_2017-11-06]

# list all branch #
$ git branch
    # * arc_2017-11-06
    # master
    
# move to the branch #
$ git checkout [branch-name=master]
    # Switched to branch 'master'
```

* You can create a new branch on different checkout node

```bash
$ git log
    commit a8a1908b7de8f658acd4173837ba5532aa8067dd
    Author: Liu Ray <manina7539@Lius-MacBook-Pro.local>
    Date:   Thu Dec 14 18:34:31 2017 +0800

        worst case 2: wrap a thread with start and join

    commit bd2eb5f294f0b5dffd9ab13ec89aa44f5465fb4f
    Author: Liu Ray <manina7539@Lius-MacBook-Pro.local>
    Date:   Thu Dec 14 18:21:00 2017 +0800

        worst case of time cost to do multithreading

    commit 8749c0ac501bb5c5be9ffc2cbfa42e1176123e9e
    Author: Liu Ray <manina7539@Lius-MacBook-Pro.local>
    Date:   Thu Dec 14 17:25:18 2017 +0800

        initial setup
      
$ git checkout 8749c0a
	# HEAD is now at 8749c0a... initial setup

$ git checkout -b master
	# Switched to a new branch 'master'
    # the branch position will be different with the same branch name if you use
    # $ git checkout a8a1908 and then $ git checkout -b master
    
```


<!--## Reference
* [Squash Multiple Git Commits Into One]({{site.url}}{{site.baseurl}}/squash-multiple-git-commits-into-one.html)
* [How To Switch To Different Git Commit]({{site.url}}{{site.baseurl}}/how-to-switch-to-different-git-commit.html)-->

## Future Work
* 要怎麼用command line merge?
* 如果用command line merge，出現conflict的時候要怎麼處理?
* 這些問題應該都可以用一個新的git test repository來測試
