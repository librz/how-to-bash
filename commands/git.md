### config

- `git config --global --list`

- `git config --local --list`

- `git config --local user.name 'rz'`

- `git config --local user.email 'rz19960718@gmail.com'`

### init & basic inspection

`git init`

`git status`

`git remote -v`

`git clone git@github.com:librz/shell-scripts.git`

`git branch -v`

`git log --oneline -n4 --graph`

`git diff --shortstat 021b1e39`

### history navigation

`git checkout 021b1e39`

### stage & commit

`git add file1.js folder1`

`git add .` or `git add -A`

`git add -u`

`git mv add.js Add.js`

`git commit -m 'update readme'`

`git reset --hard`

### sync (local <=> remote)

`git fetch origin`

`git push`

`git pull`

### branching

`git checkout -b {{new branch name}}`

`git checkout -b {{new branch name}} 021b1e39`

`git branch -D`

`git merge {{another branch's name}}`
