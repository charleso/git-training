> What happens if you create other types of `refs/` (eg. `refs/something`)?

```sh
echo 672e562c008009ec391e11a1fa3574af39428ae1 > .git/refs/something

> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master) Third commit
* 672e562 (refs/something, hello) Second commit
* 406bb3b Initial commit
```

Interesting, so unlike `master`, `hello` and anything under `refs/heads`,
in this case we see the fully qualified name.

```sh
> git branch

  hello
* master
```

It's also not a branch, which makes sense, they're only refs under `refs/heads`.

In general this is not something that's useful in every-day Git.
Git uses different "types" of refs for different purposes (and treats some of them differently)

- We've seen `heads` are just another name for branches.
- There are also [tags](https://git-scm.com/docs/git-tag) which are just refs that can't be checked out.
- Git [notes](https://git-scm.com/docs/git-notes) for annotating commits with extra values.
- More importantly they're used for remote refs which we'll seen [soon](../remotes.md).
