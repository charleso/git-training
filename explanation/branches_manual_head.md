> Try changing the `HEAD` file manually.
> Does that change the `branch` and `log --graph` ouput as you expect?

```sh
> echo "ref: refs/heads/hello" > .git/HEAD

> git branch

* hello
  master

> git log --graph --oneline --decorate master

* 41ce7fa (master) Third commit
* 672e562 (HEAD, hello) Second commit
* 406bb3b Initial commit
```

So updating `HEAD` file manually seemed to work as expected.

But not everything is the same as `checkout`.

```sh
> cat file.txt

hello
hello again
something
```

So in my case I was on the `master` branch, and manually switching
to `hello` (obviously) didn't update the working files magically.
That's something you need `checkout` for.

So in some ways you can think of `checkout` as two operations:

1. Update working files to the contents of the referenced commmit
2. Update `HEAD`
