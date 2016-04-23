> What happens if you try commiting without changing the file?

```sh
> git commit -m "Empty commit"
Changes not staged for commit:
        modified:   file.txt

no changes added to commit
```

Nothing apparently. It doesn't really make sense to make commits without changes,
and so Git doesn't let you.
