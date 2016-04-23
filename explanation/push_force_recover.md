> How would you "recover" that "remote" commit?

If you've fetched then you use can use the commit hash as normal,
which will be in the [reflog](../reflog.md).

```sh
> git log origin/my_master

928b167 refs/remotes/origin/my_master@{0}: fetch: fast-forward

> git log --graph --oneline --decorate 0ae6ce0

* 928b167 Working remotely again
* fdff1be Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (origin/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commitk
```

And then use `git branch` to [create a new branch at that commit](reflog_recreate_branch.md).

If you _haven't_ fetched you're in a spot of bother.
You have to track down someone who has that commit locally and ask them to
push again, possibly to a different branch.

No really, I'm not joking.

Otherwise, the alternative solution will depend on where you pushed (eg. Github)

- https://objectpartners.com/2014/02/11/recovering-a-commit-from-githubs-reflog/

It's probably redundant at this point to mention again that
force pushing is **really dangerous**, and should be used with extreme care.
