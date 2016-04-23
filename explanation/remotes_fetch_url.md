> Can you fetch using the path/URL (ie `../test`) instead of the remote name?

```sh
> git fetch ../test

From ../test
 * branch            HEAD       -> FETCH_HEAD
```

So when you fetch with a path/URL it only creates/updates _one_ ref,
which is called the `FETCH_HEAD`.

```sh
> ls -F .git

COMMIT_EDITMSG
FETCH_HEAD
HEAD
ORIG_HEAD
branches/
config
description
hooks/
index
info/
logs/
objects/
refs/
```

So `FETCH_HEAD` a special ref somewhat like `HEAD` we've been playing with.

```sh
> cat .git/FETCH_HEAD

41ce7faa5b8b2cf480d44c3b12f0545fed9683c3                ../test

> git log --graph --oneline --decorate FETCH_HEAD

* 41ce7fa (origin/master) Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```
