> The `HEAD` files points to a ref, the remote branches are just refs.
> What happens if you manually change the `HEAD` file to point to `refs/remote/origin/master`?
> If you do, and then make a commit, what happens if you `fetch` after that ?

Here be dragons.

```sh
> echo "ref: refs/remotes/origin/master" > .git/HEAD
```

This is the only way you cheat and "checkout" a remote branch.
There is no command that I know of that will do this for you,
for good reason as I'll try to show.

```sh
> git log --graph --oneline --decorate HEAD

* 41ce7fa (HEAD, origin/master) Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit

> echo "dodgy" >> file.txt
> git add .
> git commit -m "Don't try this at home"

[refs/remotes/origin/master 19d9431] Don't try this at home
 1 file changed, 1 insertion(+)

> git log --graph --oneline --decorate HEAD

* 19d9431 (HEAD, origin/master) Don't try this at home
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

So far this remote branch has behaved just like a normal branch.
Why doesn't Git want us to do this?

```sh
> git fetch

From ../test
 + 19d9431...41ce7fa master     -> origin/master  (forced update)

> git log --graph --oneline --decorate HEAD

* 41ce7fa (HEAD, origin/master) Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

Woah, that's not cool! So by running a normally "safe" command `fetch`,
Git has just blown away any commits that we did whilst working on that ref.

And if you think about the purpose of the remote refs, it makes sense.
It's meant to be "read only" view of what _was_ the state of the
refs in another repository. By checking it out, and then changing the
value, we've effectively "lied" and pretended like the remote branch is somewhere
else. It's not. The `fetch` is doing the Right Thing and putting it back to where
it belongs.

I can't say this enough - you **cannot checkout remote branches**.
Remember that even when you have a local branch called `master`,
which just so happens to have the same name as the remote branch.

Checkout (ha ha) the sections on [pull](../pull.md) and [push](../push.md)
to see exactly how the local and remote branches interact.
