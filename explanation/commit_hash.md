> What other forms of the hash does Git accept?

```sh
> git log 672e562
...
> git log 672e56
...
> git log 672e5
...
> git log 672e
...
> git log 672

fatal: ambiguous argument '672': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
```

The absolute minimum is 4 characters.

It also has to be unique, so as a Git repository gets bigger/older there is more
likely to be what is known as a "collision", where the same short hash refers
to 2 (or more) different commits (and other things we haven't talked about).
7 characters is usually enough to be unique for most repositories though.
