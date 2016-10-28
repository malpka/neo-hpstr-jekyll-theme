---
layout: post
title: "git log - list all commits from user"
date: 2014-04-22 09:50:25 +0200
comments: true
categories: git
facebook:
    image: /images/BGit-Logo-2Color.png
---

{% img /images/Git-Logo-2Color.png 455 190 git-logo %}

[git log](https://www.kernel.org/pub/software/scm/git/docs/git-log.html) is a powerfull command that allows to list all commits with specific criteria.

``` bash
git log --pretty=format:"%ad:%an:%s" --date=short --reverse --all --since=2.months.ago --author=john | grep -v "Merge branch"
```

* `--all` - from all branches
* `%ad` - date that respects `--date` specifier
* `%an` - author name
* `%s` - subject

```
...
2014-04-14:john:Customer entity
2014-04-15:john:Orders model
2014-04-18:john:Fixing security flaw
...
```

[source](http://stackoverflow.com/questions/10349302/how-to-git-log-from-all-branches-for-the-author-at-once)


