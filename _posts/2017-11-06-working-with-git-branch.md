---
published: true
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

## Reference
* [Squash Multiple Git Commits Into One]({{site.url}}{{site.baseurl}}/squash-multiple-git-commits-into-one.html)

## Future Work
* 要怎麼切換到比較先前的commit?
* 如果切換到不同的branch，會在commit的什麼位置?
* 要怎麼用command line merge?
* 如果用command line merge，出現conflict的時候要怎麼處理?
* 這些問題應該都可以用一個新的git test repository來測試
