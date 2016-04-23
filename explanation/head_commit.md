> If you make another commit what changes? Is it `HEAD` or the ref?

```sh
> cat .git/refs/heads/master

41ce7faa5b8b2cf480d44c3b12f0545fed9683c3

> cat .git/HEAD

ref: refs/heads/master

> echo "more" >> file.txt
> git add .
> git commit -m "Fourth commit"

[master f196996] Fourth commit
 1 file changed, 1 insertion(+)

> cat .git/refs/heads/master

f196996db07d23b6ef6558ec450750fad92686b2

> cat .git/HEAD

ref: refs/heads/master
```

No, so committing doesn't change `HEAD`, it updates the branch that
it references. The current branch.
