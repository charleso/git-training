> How would you delete a branch using just push?

So let's look at the the full push command.

```sh
> git push origin my_master:my_master
```

In particular `my_master:my_master`.
The first branch is _local_, and the second branch is the remote
branch you wish to update.

So what happens if you don't push anything to a remote branch.

```sh
> git push origin :hello

To ../test
 - [deleted]         hello
```

Weird.

There's also the (more obvious) `git push --delete origin hello` command,
but it's just a convient version of what we just did.
