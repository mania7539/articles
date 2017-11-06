---
published: true
---
* Type in command in console (bash or cmd)

```bash
git checkout -b [new-branch-name]
	## create new branch
git branch
	## list all branch
git checkout [branch-name]
	## move to the branch
```

## Reference
http://dont-be-afraid-to-commit.readthedocs.io/en/latest/git/commandlinegit.html


## Future Work

* 要怎麼切換到比較先前的commit?
* 如果切換到不同的branch，會在commit的什麼位置?
* 要怎麼用command line merge?
* 如果用command line merge，出現conflict的時候要怎麼處理?
* 如果git commit -m "" 之後沒有立刻 git push [branch-name]，而是多次(3次)commit，再push，這樣會發生什麼事?
* 這些問題應該都可以用一個新的git test repository來測試
