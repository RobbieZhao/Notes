git configuration

    git config --global user.name "robbiezhao"
    git config --global user.email "dewdwedwdwed"
    
    git config --list

Help

    git help [verb]
    git [verb] --help

    
    git init

Three states

 - working directory
 - staging area
 - committed


Commands

    git add -A (all files)
    
    // Discard all unstaged files in the current working directory
    git checkout -- .
    
    git reset
    git reset filename
    
    git status
    git log


    git clone <url> <where to clone>
    
    git remote -v
    
    # show all local and remote branches 
    git branch -a 

    git diff
    
    # origin is the name of the remote repository
    # master is the branch to pull from or push to
    git pull origin master
    git push origin master

    git branch <name> 
    git checkout <name> 
    git push -u origin <name>
    
    git branch --merged
    git merge <name>
    git push origin master
    
    # delete the branch
    git branch -d <name>
    
    # delete the branch remotely
    git push origin --delete <name>
    
    # change the previous commit message (will also change the hash because the message is part of the hash)
    git commit --amend -m "commit message"
    
    # add a file to the previous commit
    git add filenaem
    git commit --amend
    
    git log --stat
    
    # bring a commit from another branch to the current branch
    git cherry-pick hash
    
    # delete a commit (but keep the changes of that commit, the changes are in the staging area)
    git reset --soft hash
    
    # delete a commit (but keep the changes of that commit, the changes are in the working directory)
    git reset hash (default is --mixed)
    
    # delete a commit (revert all the tracked files)
    git reset --hard hash
    
    # d gets rid of untracked directories
    # f gets rid of untracked files
    git clean -df
    
    git reflog
    
    # revert to a previous commit and make a new commit (this doesn't change the commit history)
    git revert hash
    
    # difference of two hashes
    git diff hash1 hash2
    
    # unstage all the changes
    git reset 

    
## save temporary changes

    git stash save "Worked on add function"
    
    git stash list
    
    # revert to the stash but not delete the stash
    git stash apply stash@{0}
    
    # revert to the stash and delete the stash
    git stash pop 
    
    git stash drop stash@{0}
    
    # delete all stashes
    git stash clear

## Branching

    # make a new branch
    git branch <branch-name>
    
    # switch to another branch
    git checkout <branch-name>
    
    # make a new branch and check it out at the same time
    git checkout -b <branch-name>
    
    # branch forcing
    git branch -f main HEAD~3
    
## merge

    # merge the branch with main branch
    git checkout <branch-name>
    git merge main

## Reverting changes

    git reset HEAD~1

## add

    # stage everything in the whole tree
    git add -A or git add --all
    
    git add dir/ or git add -A dir/
    
    # stage everything except deleted files
    git add --no-all dir/
    
    # stage everything except untracked files
    git add -u [dir/]
    
## relative refs

    // Moving one commit up
    git checkout main^ 
    
    // move a number of commits up
    git checkout HEAD~4
    
    
    // interactive rebase
    git rebase -i HEAD~4

## Branch

branches are essentially pointers to a specific commit, or "I want to include the work of this commit and all parent commits"

#### Create a new branch and switch to that branch

You could do
    
    git branch <new-branch>
    git switch <new-branch>

Or a shorthand to do that would be: 

    git switch -c <new-branch>

#### Branch off another branch

    git checkout -b newBranch oldBranch

#### Merge a branch into another branch

merge branch A into branch B, first switch to branch B

    git switch <branch-B>

then do the merge

    git merge <branch-A>
    
#### Move branches around

This moves main branch to be HEAD~3

    git branch -f main HEAD~3

## Reverting changes

### Reset

Suppose you have C1, C2, C3, the following command will change your commit history to be C1, C2.

    git reset HEAD~1
    
More generally, if you have C1, C2, C3, ..., Cn (n commits), and you do:

    git reset HEAD~k

It deletes k commits. So your commits history will be C1, C2, ... C(n-k) (a total of n-k commits).

### Revert

A reset changes history. A safer way to revert changes is to use `git revert`

    git revert HEAD
    
The changes this command does is

    [old] C1 C2 C3
    [new] C1 C2 C3 C3' 

C3 and C3' are completely the opposite of each other. C3' reverses the changes exactly made in C3. And now the repo looks exactly as C2, it appears as if C3 has never been made before.

Notice the difference between a reset and revert. reset changes history. revert keeps the history and adds to it.

A more general revert is:

    git revert --no-commit HEAD~k..HEAD
    git commit

This reverts k commits. The changes will be:

    [old] C1 C2 C3 ... C(n-k) C(n-k+1) ... Cn
    [new] C1 C2 C3 ... C(n-k) C(n-k+1)'

Notice the `--no-commit` option. This tells git not to make any commits after reverting. This is pretty helpful if you want to revert 50 commits. If you don't specify this option, git will prompts you to commit after each revert. Of course, after the reverting, you need to manually commit.