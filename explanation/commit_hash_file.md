> The full hash is stored as a file in `.git`, can you find it?

So we're looking for the hash `672e562c008009ec391e11a1fa3574af39428ae1`.

```sh
ls -F .git/objects

03/
67/
c4/
info/
pack/
```

So the hash started with `67` and there is a folder under `objects` with that name.

```sh
ls -F .git/objects/67

2e562c008009ec391e11a1fa3574af39428ae1
```

And the rest of the hash is a file under that.

Unfortunately you waon't be able to look at that file, it's compressed.

You _can_ use `git cat-file -p <hash>` to see the contents,
but that's out of the scope of this material.
