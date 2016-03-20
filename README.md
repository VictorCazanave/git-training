# Git Training
Git Training is a list of exercises to practice using Git.

For now these exercises are focused on the rebase workflow.

## How to use it
* Fork this repository
* Clone your repository on your local machine: `git clone https://github.com/<your name>/git-training.git`
* Launch init script to create all local branches: `sh init.sh`
* Do the exercises in the same order
* You can find help in the [tips and links](#tips-and-links)
* You can compare your solutions with [mine](#solutions)
* You can [open an issue](/issues) if you find a mistake/bug or if you have any question

## Exercises

### 01. Rebase without conflict
_The goal of this exercise is to do a basic rebase._

Rebase the ex01 branch on the master branch.

[Solution](#01-rebase-without-conflict-1)

### 02. Rebase with conflicts
_The goal of this exercise is to do a rebase with conflicts (no fear!)._

Rebase the ex02 branch on the master branch resolving the conflicts as you want.

[Solution](#02-rebase-with-conflicts-1)

### 03. Abort a rebase
_The goal of this exercise is to stop an ongoing rebase._

Start to rebase the ex03 branch on the master branch but when the conflict is detected, abort the rebase.

[Solution](#03-abort-a-rebase-1)

### 04. Cancel a local rebase
_The goal of this exercise is to cancel a rebase that has been done only on a local branch._

Rebase the ex04 branch on the master branch but **do not push** the rebased local branch and cancel all its changes.

[Solution](#04-cancel-a-local-rebase-1)

### 05. Rename a commit during a rebase
_The goal of this exercise is to change the message of a commit._

Rebase the ex05 branch on the master branch and rewrite the commit's message.

[Solution](#05-rename-a-commit-during-a-rebase-1)

### 06. Merge commits during a rebase
_The goal of this exercise is to merge commits._

Rebase the ex06 branch on the master branch and squash the two commits.

[Solution](#06-merge-commits-during-a-rebase)

### 07. Delete a commit during a rebase
_The goal of this exercise is to delete a commit._

Rebase the ex07 branch on the master branch and remove the first commit.

[Solution](#07-delete-a-commit-during-a-rebase)

### 08. Rewrite commits history during a rebase
_The goal of this exercise is to clean the commits history._

Rebase the ex08 branch on the master branch to have only one commit for each file.  
Using the previous exercises:
* Delete wrong commits
* Merge commits which update the same file
* Rewrite wrong commit messages

[Solution](#08-rewrite-commits-history-during-a-rebase-1)

## Tips and links

### Update the local master branch:
* Update the remote master branch: `git fetch origin master`
* Go on the master branch: `git checkout master`
* Update the local master branch: `git rebase master origin/master`

Since we will not commit directly on the master branch, we can also use:
* Go on the master branch: `git checkout master`
* Update the local master branch: `git pull origin master`

### Resolve a conflict
There are 3 ways to resolve a conflict:
* Choose the feature file as the right version: `git checkout --ours -- <paths>`
* Choose the master file as the right version: `git checkout --theirs -- <paths>`
* Edit the file to create a correct merged version and continue the rebase: `git add <paths>` then `git rebase --continue`

### Links
* [Git Documentation](http://git-scm.com/doc)

## Solutions
These are examples of solutions but it is not the only way to solve the exercises.

### 01. Rebase without conflict
* [Update the local master branch](#update-the-local-master-branch)
* Go on the ex01 branch : `git checkout ex01`
* Rebase the ex01 branch on master branch : `git rebase master`
* Update the remote ex01 branch: `git push -f origin ex01`

Since there is no conflict between master and ex01 branches, the rebase is easily done.

### 02. Rebase with conflicts
* [Update the local master branch](#update-the-local-master-branch)
* Go on the ex02 branch : `git checkout ex02`
* Rebase the ex02 branch on master branch : `git rebase master`
* [Resolve the conflicts](#resolve-a-conflict)
* Update the remote ex02 branch: `git push -f origin ex02`

### 03. Abort a rebase
* [Update the local master branch](#update-the-local-master-branch)
* Go on the ex03 branch : `git checkout ex03`
* Rebase the ex03 branch on master branch : `git rebase master`
* There also conflicts but in this case we will no resolve it.
* Abort the rebase: `git rebase --abort`

### 04. Cancel a local rebase
* [Update the local master branch](#update-the-local-master-branch)
* Go on the ex04 branch : `git checkout ex04`
* Rebase the ex04 branch on master branch : `git rebase master`
* The local ex04 branch is now rebased but we will reset it: `git reset --hard origin/ex04`

### 05. Rename a commit during a rebase
* [Update the local master branch](#update-the-local-master-branch)
* Go on the ex05 branch : `git checkout ex05`
* Rebase the ex05 branch on master branch : `git rebase -i master`
* Change the pick command of the commit to reword it: `reword 72c9250 Update file05 with wrong commit message`
* Write the new commit's message: `Update file05`
* Update the remote ex05 branch: `git push -f origin ex05`

### 06. Merge commits during a rebase
* [Update the local master branch](#update-the-local-master-branch)
* Go on the ex06 branch : `git checkout ex06`
* Rebase the ex06 branch on master branch : `git rebase -i master`
* Change the pick command of the second commit to fixup the first one: `fixup c944dd5 Update file06`
* Update the remote ex06 branch: `git push -f origin ex06`

### 07. Delete a commit during a rebase
* [Update the local master branch](#update-the-local-master-branch)
* Go on the ex07 branch : `git checkout ex07`
* Rebase the ex07 branch on master branch : `git rebase -i master`
* Delete the first commit's line: `pick a5779a9 Commit to delete`
* Update the remote ex07 branch: `git push -f origin ex07`

### 08. Rewrite commits history during a rebase
* [Update the local master branch](#update-the-local-master-branch)
* Go on the ex08 branch : `git checkout ex08`
* Rebase the ex08 branch on master branch : `git rebase -i master`
* The commits history should look like this:
   ```
   pick 14a9611 Update file08-1
   pick befa615 Update file08-3
   pick 7d5dfc9 Update file08-1
   pick 634e37a Wrong commit message to update file08-2
   pick 5760138 Wrong commit to update file08-3
   pick 9723627 Update file08-2
   pick 34e3c2f Update file08-1
   ```

* Modify the commits history to :
  * Delete the wrong commit: `pick 5760138 Wrong commit to update file08-3`
  * Group the commits about the same file keeping the same order:
    * file01:
      ```
      pick 14a9611 Update file08-1
      pick 7d5dfc9 Update file08-1
      pick 34e3c2f Update file08-1
      ```

    * file02:
      ```
      pick 634e37a Wrong commit message to update file08-2
      pick 9723627 Update file08-2
      ```

    * file03:
      ```
      pick befa615 Update file08-3
      ```

  * Merge the commits about the same file:
    * file01:
      ```
      pick 14a9611 Update file08-1
      fixup 7d5dfc9 Update file08-1
      fixup 34e3c2f Update file08-1
      ```

    * file02:
      ```
      pick 634e37a Wrong commit message to update file08-2
      fixup 9723627 Update file08-2
      ```

  * Rewrite the wrong commit message: `reword 634e37a Wrong commit message to update file08-2`

* The final result should look like this:
   ```
   pick 14a9611 Update file08-1
   fixup 7d5dfc9 Update file08-1
   fixup 34e3c2f Update file08-1
   reword 634e37a Wrong commit message to update file08-2
   fixup 9723627 Update file08-2
   pick befa615 Update file08-3
   ```

* Update the remote ex08 branch: `git push -f origin ex08`
