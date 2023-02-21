> We've seen that the `git checkout` command can be used to checkout branches which are just references to commits. Can `git checkout` command be used to checkout commits directly? What happens to `ref/heads` if this is the case?

Git certainly does let us checkout commits directly. As an example we can checkout our second commit as follows:

```sh
> git checkout 672e562

Note: switching to '672e562'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

HEAD is now at 672e562 Second commit

> git log --graph --oneline --decorate --all

* 41ce7fa (master) Third commit
* 672e562 (HEAD, hello) Second commit
* 406bb3b Initial commit
```

Notice, there's no arrow pointing to from `HEAD` to our `hello` branch in our log (which usually happens when we checkout a **branch**). Interestingly, no knew reference is created in the `.git/refs/heads` although `.git/HEAD` is still updated to reflect this new change. However instead of pointing to a reference of a branch, it refers directly to the commit we checked out.

```sh
> ls -F .git/refs/heads

hello   master

> cat .git/HEAD

672e5628856f61c36e5671cd2d2c5789149a1538
```

As alluded to by the `git checkout` message from above, this is know as a _detached HEAD state_. Surprisingly, we can actually create commits in a detached HEAD state.

```sh
> echo "hello experiment" >> file.txt

> git add .

> git commit -m "Experimental change"

[detached HEAD 1fcdb7e] Experimental change
 1 file changed, 1 insertion(+)

> git log --graph --oneline --decorate --all

* 1fcdb7e (HEAD) Experimental change
| * 41ce7fa (master) Third commit
|/
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

The caveat is, if we want git to remember these changes, we need to create a new branch for them.

```sh
> git branch experimental

> git log --graph --oneline --decorate --all

* 1fcdb7e (HEAD, experimental) Experimental change
| * 41ce7fa (master) Third commit
|/
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

To move out of a detached HEAD state, all we need to do is checkout any branch within our repository.

```sh
> git checkout master

Previous HEAD position was 1fcdb7e Experimental change
Switched to branch 'master'

> git log --graph --oneline --decorate --all

* 1fcdb7e (experimental) Experimental change
| * 41ce7fa (HEAD -> master) Third commit
|/
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

Notice, that the arrow from our `HEAD` to our checked out branch appears once again in our log.