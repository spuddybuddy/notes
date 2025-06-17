# How to rebase Chromium at a specific commit

Rebase follow this form (the -i is for interactive which I use to verify the
list of changes that will be rebased):

```$ git rebase -i [branch/tag/revision] [original branch you were working on]```

`[original branch]` defaults to current branch.

At this point your DEPS and other repo's will still be at head, though.  To
sync those up run:

```$ gclient sync -t -D -r src@[revision or tag from above]```

Individuals commits are a sha5, like `ceb8f07ac29b`

Branch cuts are usually referred to like `branch-heads/3257`

If you know the specific commit on the branch and you want to be one before that
you can add a `~` to get the previous commit.  So for example `ceb8f07ac29b~` refers
to the commit just before `ceb8f07ac29b`.  You can also add a number to go back
more commits `~2`, `~3` etc.
