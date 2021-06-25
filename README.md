#Squash Commits -

git rebase -i HEAD~4  //Will squash last 4 commits

1. In the interactive shell, change all commits except the first one, from pick to squash
2. :wq
3. Review/Change commit message
4. Push the changes to the remote branch

git push origin branch-name --force


#Rename Commits - 
git commit --amend -m "Your new message here"

If you have other commits to reword

git rebase -i HEAD^
# then replace 'pick' with 'r' or 'reword' and save, editor should pop up again to edit the msg

Because this commit has a new SHA1 due to the change of the contents, you will need to force push the new reference. The force is needed because it tells git to forget about the previous commit. It's a safety measure.

git push origin your-branch-name -f






#TODO
1. Snapshots in Git
2. Rebase
3. Sync Branches
4. Upstream Downstream
5. Moving Head
6. Discarding/Reverting Commits/PR
