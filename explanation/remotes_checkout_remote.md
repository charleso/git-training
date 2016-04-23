> What happens if you _do_ try to checkout a remote branch
> (eg. `git checkout origin/master`)?
> How does that change the `HEAD` file?
> Is that what you would expect?

```sh
> git checkout origin/master

Note: checking out 'origin/master'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b new_branch_name

HEAD is now at 41ce7fa... Third commit
```

The error message says it all really.

```sh
> cat .git/HEAD

41ce7faa5b8b2cf480d44c3b12f0545fed9683c3
```

So the `HEAD` interesting points to a _commit_, not a ref.
As the error says this is known as "detached HEAD".

Let me ask another question - what happens if you commit while in this state?

```sh
> echo "detached" >> file.txt
> git add .
> git commit -m "Detached"

[detached HEAD a86f1c6] Detached
 1 file changed, 1 insertion(+)

> git log --graph --oneline --decorate HEAD

* a86f1c6 (HEAD) Detached
* 41ce7fa (origin/master) Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

So far so good, but now when you try to checkout a branch:

```sh
> git checkout origin/master

Warning: you are leaving 1 commit behind, not connected to
any of your branches:

  a86f1c6 Detached

If you want to keep them by creating a new branch, this may be a good time
to do so with:

 git branch new_branch_name a86f1c6

HEAD is now at 41ce7fa... Third commit
```

Again, the error message here is surprisingly good
(it didn't used to say this in older versions of Git).
If you didn't know what was going on, and you didn't understand the message,
you might lose that commit and any work it contained.

```sh
> git log --graph --oneline --decorate --all

* 41ce7fa (HEAD, origin/master) Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

As always, the faithful [reflog](../reflog.md) has our back.
