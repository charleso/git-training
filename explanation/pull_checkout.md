> If you wanted to view `remote.txt` how might you do that with the commands you already know?

```sh
> git log --graph --oneline --decorate origin/master

* c6756d7 (origin/master) Working remotely
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

This should be easy enough.

```sh
> git branch new_master origin/master

Branch new_master set up to track remote branch master from origin.

> git checkout new_master

Switched to branch 'new_master'
Your branch is up-to-date with 'origin/master'.

> git log --graph --oneline --decorate origin/master

* c6756d7 (HEAD, new_master, origin/master) Working remotely
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

You can also [detach HEAD](remotes_checkout_remote.md) if you don't want
to create a new branch.

```sh
> git checkout origin/master

<blah blah blah>
```

Finally, the best way to _specifically_ see the file contents of is with `show`,
a command we haven't seen before.

```sh
> git show origin/master:file.txt

hello
hello again
goodbye
```
