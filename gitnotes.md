# decorate git log, make it more readable
  `git log --graph --oneline --decorate`

# git add . is useless when committing with `-am` flag
  git commit -am "change"

# Create aliases for repeated commands
  git config --global alias.ac "commit -am"
  git ac "new commit"

# force overwrite from local changes to remote git
  git push --force

# force overwrite local from remote git
  git fetch origin
  git reset --hard origin/master
  git clean -df

# make a new branch
  git checkout -b feature

# switch branch
  git checkout master

# save changes for later
  git stash
  git stash save coolstuff

# load up the saved changes again
  git stash pop
  git stash list
  git stash apply 0
