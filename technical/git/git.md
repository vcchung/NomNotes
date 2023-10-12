# Git
- show config and file origin
  - `git config -l --show-origin`

- git fetch vs git pull
  - three areas
    - remote repo
    - local repo
    - working directory
  - git pull will pull changes from remote repo to local repo and working directory
  - git fetch will pull changes from remote repo to local repo
  - git merge will merge the working directory with local repo

- git fetch for all branches
  - `git fetch --all`

- git list all branches
  - `git branch -a`

- git log with graph
  - `git log --graph`

- git four tress
  - three tress in local, one tree in remote
    - working directory
    - index/cache
    - local repo
    - remote repo
  - git add
    - add to index/cache from working dir
  - git commit
    - add from index/cache to local repo
  - git push 
    - add from local repo to remote repo
  - git fetch
    - download from remote repo to local repo
  - git pull
    - download from remote repo to local repo, index and working dir
  - git diff HEAD
    - diff working dir vs local repo
  - git diff
    - diff working dir vs index/cache

- git three reset mode
  - `git reset --soft <commit>`
    - move HEAD to commit, keep index/cache/staging area and working dir untouched
  - `git reset --mixed <commit>`
    - move HEAD and index/staging area to commit, keep working dir unchanged
  - `git reset --hard <commit>`
    - move HEAD and index and working dir to commit

- How to squash last 3 commit?
  - `git reset --soft HEAD~3`
    - after that, all the three commit is in index, but remove from local repo
  - `git commit -m "msg"`
    - commit change to local repo
  - `git push -f`
    - force push to remote repo
  
