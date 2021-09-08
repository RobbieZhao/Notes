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
    
## merge

    git merge <branch>
    git commit

## add

    # stage everything in the whole tree
    git add -A or git add --all
    
    git add dir/ or git add -A dir/
    
    # stage everything except deleted files
    git add --no-all dir/
    
    # stage everything except untracked files
    git add -u [dir/]
    