> Does a merge have _anything_ to do with remotes?

No. Nothing. Nada. Never.

The `merge` command simply takes two commits and creates a new merge commit.
This is all done in your _local_ repository.
Of course one of those commits might only be "on" a remote ref,
but Git doesn't care.

Remember that `pull` = `fetch` + `merge`.
The `fetch` step _does_ all the talking to the remote repository, downloading
new commits.  The merge on the other hand is completely local.
Don't let `pull` hide that fact.
