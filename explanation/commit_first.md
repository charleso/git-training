> What happens when you use log to view the first commit?

```sh
> git log 406bb3bffbd02113ad5e2fecb4da364c01b20bb3

commit 406bb3bffbd02113ad5e2fecb4da364c01b20bb3
Author: Charles O'Farrell <charleso@charleso.org>
Date:   Sun Apr 17 10:35:29 2016 +1000

    Initial commit
```

Git log will _always_ start from a commit or commits and
work back through the parent (or parents) until it reaches
the first commit.
