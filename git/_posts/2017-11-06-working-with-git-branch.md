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

## Reference (script)
    {% for post in site.categories.git %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}

* [Squash Multiple Git Commits Into One]({{site.url}}{{site.baseurl}}/squash-multiple-git-commits-into-one.html)
* [How To Switch To Different Git Commit]({{site.url}}{{site.baseurl}}/how-to-switch-to-different-git-commit.html)

## Future Work
* 要怎麼用command line merge?
* 如果用command line merge，出現conflict的時候要怎麼處理?
* 這些問題應該都可以用一個新的git test repository來測試
