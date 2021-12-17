![App Ideas Image](./github-social.png)
some changes here
some more changes
## Contents
- [Adding a local repo to origin](#adding-a-local-repo-to-origin)

- [Changing/Setting username and email](#changingsetting-username-and-email)

- [Change Origin of an existing local repo](#change-origin-of-an-existing-local-repo)

- [Make a local branch point to a remote branch](#make-a-local-branch-point-to-a-remote-branch)

- [Squash Commits](#squash-commits)

- [Rename Commits](#rename-commits)

- [Reverting to all changes on remote repo](#reverting-to-all-changes-on-remote-repo)

- [Cherrypick](#cherrypick)

- [Rebase](#rebase)

- [Snapshots](#snapshots)

- [Git Commit Message Standards](#git-commit-message-standards)

  
---

### Adding a local repo to origin
check origin info : git origin -v
add new origin : git remote add origin https://xyz.github.com
set upstream and push : git push --set-upstream origin master


### Changing/Setting username and email
Set your username: git config --global user.name "FIRST_NAME LAST_NAME"
Set your email address: git config --global user.email "MY_NAME@example.com"

### Change Origin of an existing local repo
git remote set-url <remote_name> <remote_url>
ex. : git remote set-url origin https://git-repo/new-repository.git

### Make a local branch point to a remote branch
git branch --set-upstream-to=origin/remote-branch local-branch

### Squash Commits
git rebase -i HEAD~4  //Will squash last 4 commits

1. In the interactive shell, change all commits except the first one, from pick to squash
2. :wq
3. Review/Change commit message
4. Push the changes to the remote branch

git push origin branch-name --force

### Rename Commits
git commit --amend -m "Your new message here"

If you have other commits to reword

git rebase -i HEAD^
then replace 'pick' with 'r' or 'reword' and save, editor should pop up again to edit the commit message.

Because this commit has a new SHA1 due to the change of the contents, you will need to force push the new reference. The force is needed because it tells git to forget about the previous commit. It's a safety measure.

git push origin your-branch-name -f

### Reverting to all changes on remote repo
Note - It will discard all local commits and changes
git revert --hard orgin/branch-name

### Cherrypick
git cherry-pick <commit-hash>
then push the changes to the remote. We can also use multiple hashes separated by space to cherrypick multiple commits
  
### Rebase
git checkout feature-branch
git rebase master

It will rewrite all commits made in feature branch after rebasing it to master, resulting in a linear branch history.
Should be only applied on Feature branches which are not public (used by any other), as the history will be re-written and it may cause issues.
  
### Snapshots
The git commit command captures a snapshot of the project's currently staged changes. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicitly ask it to. 
  
Assume we have a file called "a.txt". After we commit this file, it will create some folders under .git/objects path. Every time we do COMMIT git will save snapshots to disk instead of the delta between the new version to the old version of the same file (it will create new folders whenever we commit). Even if we just changed one letter of one file, git will save the whole file as a snapshot.

This also called the loose object format.
  
In this case, git will cost more disk space than the other vcs(such as subversion) which saves delta between the new version to the old version of the same file. But the benefits of using snapshot shorten the time at commit stage.

But the brilliant git will do another jobgit gc after this from time to time which created PACKFILES and removes the snapshot which contents are similar to shrink the size of itself. After these workgit gc, the disk cost by git will just like the other VCS which uses delta ways.
Through snapshot and git gc. Git will faster than other VCS which use delta ways at commit stage and costed the disk size just be similar to the other VCS that use delta ways.
Git finds a balanced way between the performance and disk space cost.

The packfiles is under .git/objects/pack
You can see it after execute "git gc" command by yourself.

### Git Commit Message Standards
  http://karma-runner.github.io/6.3/dev/git-commit-msg.html
  
  1. Specify the type of commit:
   - feat: The new feature you're adding to a particular application
   - fix: A bug fix
   - style: Feature and updates related to styling
   - refactor: Refactoring a specific section of the codebase
   - test: Everything related to testing
   - docs: Everything related to documentation
   - chore: Regular code maintenance. (You can also use emojis to represent commit types)
  
  2. Separate the subject from the body with a blank line
  3. Your commit message should not contain any whitespace errors
  4. Remove unnecessary punctuation marks
  5. Do not end the subject line with a period
  6. Capitalize the subject line and each paragraph
  7. Use the imperative mood in the subject line
  8. Use the body to explain what changes you have made and why you made them.
  9. Do not assume the reviewer understands what the original problem was, ensure you add it.
  10. Do not think your code is self-explanatory

  ![image](https://user-images.githubusercontent.com/61384771/135752057-06cec24a-001b-4a3d-8b12-547465d677bc.png)

  
