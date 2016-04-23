> If your local branch is (also) called `master`, what happens if you run `git log master`?
> Which branch are you asking about?

Fortunately Git will _never_ resolve the remote branch based on just the name.
So `git log master` _only_ refers to the head ref, never the remote ref.
You need to specify `origin/<name>`.
