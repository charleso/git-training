> We've seen that the `git checkout` command can be used to checkout
 branches which are just references to commits. Can `git checkout` command
  be used to checkout commits directly? What happens to `ref/heads` if this 
  is the case?

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

Notice, there's no arrow pointing to from `HEAD` to our `hello` branch in 
our log (which usually happens when we checkout a **branch**). 
Interestingly, no new reference is created in the `.git/refs/heads` 
although `.git/HEAD` is still updated to reflect this new change. However 
instead of pointing to a reference of a branch, it refers directly to the 
commit we checked out.

```sh
> ls -F .git/refs/heads

hello   master

> cat .git/HEAD

672e562c008009ec391e11a1fa3574af39428ae1
```

As alluded to by the `git checkout` message from above, this is know as a 
_detached HEAD state_. Surprisingly, we can actually create commits in a 
detached HEAD state.

```sh
> echo "hello experiment" >> file.txt 

> git add .

> git commit -m "Experimental change"

[detached HEAD b049fe5] Experimental change
 1 file changed, 1 insertion(+)

> git log --graph --oneline --decorate --all

* b049fe5 (HEAD) Experimental change
| * 41ce7fa (master) Third commit
|/
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

To move out of a detached state, we can just checkout any branch.

```sh
> git checkout hello

Warning: you are leaving 1 commit behind, not connected to
any of your branches:

  b049fe5 Experimental change

If you want to keep it by creating a new branch, this may be a good time
to do so with:

 git branch <new-branch-name> b049fe5

Switched to branch 'hello'
```

What is git warning us about here? Basically, since our newly created 
commit isn't the parent of any branch refs, git will eventually garbage 
collect this commit. Fortunately, this won't happen immediately and we can 
still find our commit by running the [reflog](../reflog.md) command (which we will see more of in soon).

```sh
> git reflog | head -n 3

672e562 HEAD@{0}: checkout: moving from b049fe51bce14781e0597e81099806c483cd196b to hello
b049fe5 HEAD@{1}: commit: Experimental change
672e562 HEAD@{2}: checkout: moving from master to 672e562

> git checkout b049fe5

Note: switching to 'b049fe5'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

HEAD is now at b049fe5 Experimental change
```

We can now create a new branch for this commit to make sure it isn't 
garbage collected in future.

```sh
> git branch experimental

> git log --graph --oneline --decorate --all

* b049fe5 (HEAD, experimental) Experimental change
| * 41ce7fa (master) Third commit
|/
* 672e562 (hello) Second commit
* 406bb3b Initial commit

> git checkout experimental

Previous HEAD position was b049fe5 Experimental change
Switched to branch 'master'

> git log --graph --oneline --decorate --all

* b049fe5 (HEAD -> experimental) Experimental change
| * 41ce7fa (master) Third commit
|/
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

Notice, that the arrow from our `HEAD` to our checked out branch appears 
once again in our log signifying we are no longer in a detached HEAD state. 
This means any new commits will be made to our experimental branch.
