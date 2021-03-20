# Git command

## Staging
### git rest --soft HEAD^ 
Undo last commit. Changes return to staging state (and still there in our mechine)
### git reset --hard HEAD^ 
Undo last commit and all changes. Files in our mechine reset to last commit too
### git reset --hard HEAD^^
The same but reset to 2 last commit
### git commit --amend -m "New message"
Change the last commit

## Remote
git remote add name 'www.github.com/address'
git push -u origin master (-u = next time don't have to specify origin master)

## Branch
### git branch branchname
create a new branch
### git checkout branchname
switch to that branch
### git checkout -b branchname
create a new branch, switch to that branch
### git merge branchname
- have to be in master branch, then merge branchname into master
- After merge, Vi editor appeared asked us why we need to merge
- Able to modify the message at line 1 if wanted too
- **:wq** + enter to save and quit
### git branch -d branchname
delete a local branch
### git branch -D branchname
delete a remote branch (that someone else created)
### git remote prune origin
clean all deleted branch
### git push origin branchname
push the branch to gihub
### git branch -r
see all remote branch
### git remote show origin
show all the local, remote branches

## Collaboration: when there is conflict
- The push will be reject
### git pull first then push
- if cannot pull, there is a file both person had edited
- Jump to VS code, there will be some text that signify the conflicts. Delete one of them
- git commit -a, skip the mesage
- git push

## Tag
- A reference to a specific commit. Click on the tag in git hub and we can see the stage our code was in that time
- Mainly used for release verison
### git tag
list all tag
### git tag -a v0.0.3 -m "version 0.0.3"
add a new tag
### git push --tags
push the tag

## Rebase
- Merge commit are messy
- Best if it's a brand new branch. For old branch, better with merge
- Instead of pull and push, we can use rebase
### git rebase
- 1. Move all changes to master to a temporary area (if it is not in origin/master)
- 2. Run all origin master commit, 1 a time
- 3. Run all commit in the temporary area, 1 a time
### Merge branch using rebase (merge admin to master)
- git checkout admin
- git rebase master
### rebase conflict
- git fetch
- git rebase
- Conflict dialog appeared. It asked to either open code editor and solve, or skip this patch, or stop rebase
- After solved conflict in text editor, git add -a
- git rebase --continue


