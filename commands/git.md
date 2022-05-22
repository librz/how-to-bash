### config

under `$HOME` folder, a file named .gitconfig stores global git configs

- `git config --global --list`

- `git config --local --list`

- `git config --local user.name 'rz'`

- `git config --local user.email 'rz19960718@gmail.com'`

### init & basic inspection

- `git --version`

- `git init`

- `git status`

- `git remote -v`

- `git clone git@github.com:librz/shell-scripts.git`

- `git branch -v`

- `git log --oneline -n4 --graph`

- `git diff --shortstat 021b1e39`

### stage & commit

- stage(track) files/folders: `git add file1.js folder1`

- stage all changes(tracked & untracked files): `git add .` or `git add -A`

- stage updates to tracked files: `git add -u`

- mv or rename file/folder: `git mv add.js Add.js`

- commit changes in staging area: `git commit -m 'update readme'`

- forfeit current changes in staging area & working tree: `git reset --hard`

### sync (local <=> remote)

`git fetch origin`

`git push`

`git pull`

### branching

- start a new branch based on header of current branch: `git checkout -b {{new branch name}}`

- start a new branch based on commit whose commit id is 021b1e39: `git checkout -b {{new branch name}} 021b1e39`

- delete branch: `git branch -D {{branch name}}`

- merge current branch with another branch: `git merge {{another branch's name}}`

### history navigation

- `git checkout 021b1e39`
