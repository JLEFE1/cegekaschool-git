# Start exercise
git checkout fugufusion
git merge master

# Solve exercise
## Create local branches
git checkout newfugu

## Create new branch from correct possition of our code
git checkout -b test 0efd99fe
git merge newfugu

## Cherry pick latets correct changes onto the brench
git cherry-pick 15f6809b
git cherry-pick 9ad99f9b
git cherry-pick 67f52924
git cherry-pick 6acce8ed
git cherry-pick 9ad2fad5
git cherry-pick 41cd40d6

> git cherry-pick 15f6809b..41cd40d6
> Gave some errors. Need to abort and apply all commits one after one

## Reset master to the last correct position
git checkout master
git reset --hard 8e80419d

## Add all correct commits to master
git merge test

## Remove incorrect commits
git pull
git push origin master
git merge test




git fetch origin
git reset --hard origin/master
git reset --hard origin/fugufusion
git reset --hard origin/newfugu


# To check
(do not change history)[https://stackoverflow.com/questions/253055/how-do-i-push-amended-commit-to-the-remote-git-repository]
I actually once pushed with --force and .git repository and got scolded by Linus BIG TIME. In general this will create a lot of problems for other people. A simple answer is "Don't do it".

I see others gave the recipe for doing so anyway, so I won't repeat them here. But here is a tip to recover from the situation after you have pushed out the amended commit with --force (or +master).

Use git reflog to find the old commit that you amended (call it old, and we'll call the new commit you created by amending new).
Create a merge between old and new, recording the tree of new, like git checkout new && git merge -s ours old.
Merge that to your master with git merge master
Update your master with the result with git push . HEAD:master
Push the result out.
Then people who were unfortunate enough to have based their work on the commit you obliterated by amending and forcing a push will see the resulting merge will see that you favor new over old. Their later merges will not see the conflicts between old and new that resulted from your amending, so they do not have to suffer.

## Permanently delete commits from remote branch
(Permanently delete commits from remote branch)[https://stackoverflow.com/questions/3293531/how-to-permanently-remove-few-commits-from-remote-branch]