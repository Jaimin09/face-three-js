create a branch with branchname

``` git checkout -b <branchname> ```

stage the changes in the branch

``` git add * ```

commit the changes in the "branchname" branch

``` git commit -m "comment" ```

change branch to master

``` git checkout master ```

List all the branches

``` git branch ```

Renaming a branch

``` git branch -m <oldbranch> <newbranch> ```

deleting a branch : If branch is not merged, then error message

``` git branch -d <branchname> ```

Force delete a branch

``` git branch -D <branchname> ```

Merging branches

``` git checkout <target-branch> ``` (target branch is where you need to merge eg. master) 

``` git merge <source-branch> ``` (branch you want to merge)

Compare branches: Produces a report on what is diff between branches. Doesn't merge or change anything

```git diff <branch1> <branch2> ```

### Rebase

- helps to clean up the local history
- reading rough draft vs final copy
- squash all commits into 1 single commit for better readability of history
- DO NOT USE rebase on public branches as it creates confusion. Also some teams never use rebase

2 ways to rebase:

1) Clean up history
2) Pull without merge (pull changes without merging)


##### 1. Clean up history
- squashes all commits into a single commit

``` git log --online ``` (Lists all commits made so far)

```git merge-base <branchname> master ``` Get the original base of the \<branchname\> created from master

``` git rebase -i <commit-sha> ``` (commit-sha is the sha number of that branch)

Git will then open up a new file with a list of commits, which you should look like this

``` pick    2334edu starting f1```

```*squash* 2334e8k more work in f1```

```*squash* 24532ek completed f1```

changepick to squash for the branches you want to squash. Save and close this file. 

Then another file for commits comments will open up. You can delete the previous comments and write a new comment. Save and close.

And rebase will be made. You can chech with ```git log --online``` again to see the new commits.

To see everything that happened before and after rebase:

``` git reflog ```

#### 2. Pull without merging
Let say you created a branch from master and then made changes into master. You want to pull these changes from master to your branches. You can do either merge or rebase. 

- If you rebase and not merge: Commits will be organized. (eg. all commits of master are together and all commits of branch are together)
- Otherwise: The history will be preserved as it is if you merge. 
- The final result for both will be same

to rebase you can run following command from your branch:

``` git rebase master ```


### Cherry-pick
- copies a specific commit to another branch
- use for bugfix for mutiple version of products
- use to caputer commits from inactive branch
- move specific commit to your branch (when entire branch is not ready to merge)
- It creates a duplicate commit in each branch




### Git Diff:

```git diff ``` changed and not staged for commit

```git diff --cached``` changed and staged for commit

``` git diff HEAD``` changed since last commit

``` git diff <commit>``` specific commit and current

``` git diff <commit1> <commit2>``` difference between two commits

```git diff feature master ``` difference between tips of branches

``` git diff feature...master``` changed in master since feature was started off of it

```git diff feature master file.txt ``` difference in file.txt on two branches
  

### Pull Request
- Easy way to let others review your changes in your branch
- Once you commit changes to your branch, you can create a pull request.
- Reviewers will review your commits and comment on spcific things if they think some changes are required.
- Based on the feedback/comments you received, you can perform those changes and commit again.
- Reviewer will (probably get the notification and) see the changes you have made and comment if necessary.
- Once everyone approves your commits in your branch, your branch can be safely merged with the master.
- Then you can delete your branch
  
### Best Practices:

- By default, git name your repository as 'origin'
- To change the name, you can use:
``` git remote add <name> <remote-url> ```
- List all remotes:
``` git remote -v ```
- Fetch v/s pull: pull = fetch + merge. Fetch only download the part which is not already on your local machine. It shows the changes but does not change merge them on your local machine
- Must not push ignore files and compiler generated files. You can open .gitignore file, you can specifiy *.zip (pattern) to ignore.
- Frequent smaller commits are better to manage than one giant commit
- remove comments. It costs time for your team members.
- git also sees white spaces. Different format means git will pick that up as difference. Make sure all team members use consistent format
- While merging the branches, conflict can occur. Git will highlight conficting code. You can resolve it and then merge. Don't forget to remove the file markers.
- ``` git merge --abort```: while resolving conflicts during merging if you realise something (that is not in conflict) should have been different, you should not make the during merging. You should abort the merge, make the change, merge and resolve the conflicing part.
