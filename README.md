# Adding a local repo to origin
check origin info : git origin -v
add new origin : git remote add origin https://xyz.github.com
set upstream and push : git push --set-upstream origin master
We created some commits in our branch, and now want to set the tracking branch to be master : git branch -u origin/master

# Squash Commits -

git rebase -i HEAD~4  //Will squash last 4 commits

1. In the interactive shell, change all commits except the first one, from pick to squash
2. :wq
3. Review/Change commit message
4. Push the changes to the remote branch

git push origin branch-name --force


# Rename Commits - 
git commit --amend -m "Your new message here"

If you have other commits to reword

git rebase -i HEAD^
then replace 'pick' with 'r' or 'reword' and save, editor should pop up again to edit the msg

Because this commit has a new SHA1 due to the change of the contents, you will need to force push the new reference. The force is needed because it tells git to forget about the previous commit. It's a safety measure.

git push origin your-branch-name -f

# Reverting to all changes on remote repo (Will discard all local commits and changes)
git revert --hard orgin/branch-name

# Cherrypick
git cherry-pick <commit-hash>
then push the changes to the remote. We can also use multiple hashes separated by space to cherrypick multiple commits

# Rebase
git checkout feature-branch
git rebase master

It will rewrite all commits made in feature branch after rebasing it to master, resulting in a linear branch history.
Should be only applied on Feature branches which are not public (used by any other), as the history will be re-written and it may cause issues.
  
# Snapshots
The git commit command captures a snapshot of the project's currently staged changes. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicitly ask it to. 
  
Assume we have a file called "a.txt". After we commit this file, it will create some folders under .git/objects path. Every time we do COMMIT git will save snapshots to disk instead of the delta between the new version to the old version of the same file (it will create new folders whenever we commit). Even if we just changed one letter of one file, git will save the whole file as a snapshot.

This also called the loose object format.
  
In this case, git will cost more disk space than the other vcs(such as subversion) which saves delta between the new version to the old version of the same file. But the benefits of using snapshot shorten the time at commit stage.

But the brilliant git will do another jobgit gc after this from time to time which created PACKFILES and removes the snapshot which contents are similar to shrink the size of itself. After these workgit gc, the disk cost by git will just like the other VCS which uses delta ways.
Through snapshot and git gc. Git will faster than other VCS which use delta ways at commit stage and costed the disk size just be similar to the other VCS that use delta ways.
Git finds a balanced way between the performance and disk space cost.

The packfiles is under .git/objects/pack
You can see it after execute "git gc" command by yourself.

# ToDo
1. ~~Snapshots in Git
2. ~~Rebase
3. Sync Branches
4. Upstream Downstream
5. Moving Head
6. Discarding/Reverting Commits/PR
7. Ahead and Behind
8. Git Log
9. Git Bisect
10. gitk
