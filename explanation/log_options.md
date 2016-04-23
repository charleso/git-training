> What does each of those options do?

```sh
> git log --graph 41ce7fa

* commit 41ce7faa5b8b2cf480d44c3b12f0545fed9683c3
| Author: Charles O'Farrell <charleso@charleso.org>
| Date:   Sun Apr 17 11:26:45 2016 +1000
|
|     Third commit
|
* commit 672e562c008009ec391e11a1fa3574af39428ae1
| Author: Charles O'Farrell <charleso@charleso.org>
| Date:   Sun Apr 17 10:56:55 2016 +1000
|
|     Second commit
|
* commit 406bb3bffbd02113ad5e2fecb4da364c01b20bb3
  Author: Charles O'Farrell <charleso@charleso.org>
    Date:   Sun Apr 17 10:35:29 2016 +1000

          Initial commit
```

```sh
> git log --oneline 41ce7fa

41ce7fa Third commit
672e562 Second commit
406bb3b Initial commit
```

```sh
> git log --decorate 41ce7fa

commit 41ce7faa5b8b2cf480d44c3b12f0545fed9683c3 (HEAD, master)
Author: Charles O'Farrell <charleso@charleso.org>
Date:   Sun Apr 17 11:26:45 2016 +1000

    Third commit

commit 672e562c008009ec391e11a1fa3574af39428ae1
Author: Charles O'Farrell <charleso@charleso.org>
Date:   Sun Apr 17 10:56:55 2016 +1000

    Second commit

commit 406bb3bffbd02113ad5e2fecb4da364c01b20bb3
Author: Charles O'Farrell <charleso@charleso.org>
Date:   Sun Apr 17 10:35:29 2016 +1000

    Initial commit
```
