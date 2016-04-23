> How can you undo that merge commit?

So we've just created a merge commit.

```sh
> git log --graph --oneline --decorate my_master

* fdff1be (HEAD, my_master) Merge branch 'origin/master' into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (orign/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

The quickest way is to just update the refs file with the previous commit.

```sh
> echo 6a9bac963a839feb1bd7209d275ca1353a3607a > .git/refs/heads/my_master

> git log --graph --oneline --decorate my_master

* 6a9bac9 (HEAD, my_master) Working locally
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

Note that the working files won't change, so you'll have a "new" remote.txt file
still in your working directory.

The easiest way is to use the [reset --hard](../reset.md) command,
which we haven't looked at yet.

```sh
> git reset --hard 6a9bac9

HEAD is now at 6a9bac9 Working locally

> git log --graph --oneline --decorate my_master

* 6a9bac9 (HEAD, my_master) Working locally
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

It's like it never happened...
