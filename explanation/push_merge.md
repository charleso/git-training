> Can you try to push the `my_master` branch successfully?

The first thing you should always do when lost in Git is look at the current graph.

```sh
> git fetch origin

remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (2/2), done.
From ../test
   fdff1be..928b167  my_master  -> origin/my_master

> git log --graph --oneline --decorate my_master

* b49a323 (HEAD, my_master) Working locally again
| * 928b167 (origin/my_master) Working remotely again
|/
* fdff1be Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (origin/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

Before we can push we need to make the push "fast-forward".
Which basically means that we'll need to merge.

```sh
> git merge origin/my_master

Merge made by the 'recursive' strategy.
 remote.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 remote.txt

> git log --graph --oneline --decorate my_master

* ab98291 (HEAD, my_master) Merge branch 'origin/my_master' into my_master
|\
* | b49a323 Working locally again
| * 928b167 (origin/my_master) Working remotely again
|/
* fdff1be Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (origin/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

And then you can push quite happily.

```sh
> git push origin my_master

Counting objects: 6, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 289 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To ../test
 + fdff1be...b49a323 my_master -> my_master

> git log --graph --oneline --decorate my_master

* ab98291 (HEAD, my_master, origin/my_master) Merge branch 'origin/my_master' into my_master
|\
* | b49a323 Working locally again
| * 928b167 Working remotely again
|/
* fdff1be Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (origin/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```
