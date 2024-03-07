# git-prunning
Delete old git branches with ease.

To delete all local branches which has been merged:
```
git branch --merged | egrep -v "(^\*|master|dev)" | xargs git branch -d
```
Explanation:

`git branch –merged`  : first, you are simply listing all the branches currently merged with your current checked out branch;
`egrep -v "(^*|main|dev)"` : you are using the invert matching feature of grep in order to exclude any branches that may be called “main” or “dev”.
`xargs git branch -d` : you are deleting every single branch listed before.

To delete all unused remote branches which has not been merged:

```
git branch -r --merged | egrep -v "(^\*|master|dev)" | xargs -n 1 git push --delete origin
```

Same as before, but the `-r` is for remote.

To delete remote references:

```
git remote prune origin
```

The git remote prune origin command is used to remove local references to remote branches that have been deleted on the remote repository (in this case, "origin").

When you fetch updates from a remote repository, your local repository keeps references to remote branches. If a branch is deleted on the remote repository, your local repository might still have references to it. Running git remote prune origin will remove these stale references, keeping your local repository in sync with the remote one.

Do it automatically with (this happens on every fetch)
```
git config --global fetch.prune true
```
