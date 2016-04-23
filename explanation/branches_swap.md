> How would you swap the two `master` and `hello` branches around?

This is actually more common than you might think.
Imagine the scenario - the current branch (ie. `HEAD`) is `master`
and you make a commit. At this point you realise that you really
want to do this work "on" a branch. How do you get the `master`
branch back to where it was?

So from this starting point:

```sh
> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master) Third commit
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

The quickest/dodgiest way is to update the refs files manually:

```sh
echo 672e562c008009ec391e11a1fa3574af39428ae1 > .git/refs/heads/master
echo 41ce7faa5b8b2cf480d44c3b12f0545fed9683c3 > .git/refs/heads/hello

> git log --graph --oneline --decorate hello

* 41ce7fa (hello) Third commit
* 672e562 (HEAD, master) Second commit
* 406bb3b Initial commit
```

Keep in mind that because we didn't run `checkout` that the working files
haven't changed _at all_, so you'll see be seeing content from the
"Third commit" (in this example the "goodbye" line).

The "safe" way is a little more involved. Moving a branch "forwards"
can be done with `merge`. There's no "safe" way to move `master`
back, although plenty of unsafe ways.

Let's swap the branches back.

```sh
> git merge hello master

Fast-forward
 file.txt | 1 +
 1 file changed, 1 insertion(+)

> git branch --force hello 672e562

> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master) Third commit
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

If you tried to use `branch --force` on the `HEAD` branch you'll see an error.

```sh
> git branch --force master hello

fatal: Cannot force update the current branch.
```

This is where you might reach for [reset](../reset.md).
