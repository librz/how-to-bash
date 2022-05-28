### config

under `$HOME` folder, a file named `.gitconfig` stores global git configs

under current folder, a folder name `.git` stores all things related to git. inside it a file name `config` stores local git config

- `git config --global --list`

- `git config --local --list`

- `git config --local user.name 'rz'`

- `git config --local user.email 'rz19960718@gmail.com'`

- `git config --local http.proxy http://proxyUsername:proxyPassword@proxy.server.com:port`

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

- `git fetch origin`

- `git push`

- `git pull`

### branching

- start a new branch based on a certain commit: `git branch {{commit id}}`

- start a new branch based on head of current branch: `git checkout -b {{new branch name}}`

- start a new branch based on commit whose commit id is 021b1e39: `git checkout -b {{new branch name}} 021b1e39`

- delete branch: `git branch -D {{branch name}}`

- merge current branch with another branch: `git merge {{another branch's name}}`

### history navigation

- `git checkout 021b1e39`

---

### about the `.git` folder

several interesting files/folders under `.git` folder

- `config` file: stores all local git configs
- `HEAD` file: shows which branch the HEAD is currently pointing at (branch points to the lastest commit of that branch, so HEAD in essense is a reference to a specific commit)
- `refs/heads` folder: stores latest commit of each branch
- `objects` folder: stores objects that git relies upon under the hood (commit, tree & blob)

From the user's perspective, git is a VCS(verion control system). But from the perspective of implementation, git is a file based database. Every commit has an unique hash (primary key) that corresponds to the snapshot (folder structure & file content) at the time of commit. Besides that, a commit also stores the id of its parent commit & things like author & commit mesage.

The DS(data structure) of commit can be defined as:

```typescript
interface Commit {
  id: string;
  parent_commit_id?: string;
  tree_id: string; // reference to project snapshot
  timestamp: string;
  author: string;
  message: string;
  ...
}
```

Notice, commit by itself is very small. That's because it doesn't directly store snapshot information such as folder structure & file content, it simply stores the correspond tree_id & reference the tree.

Tree is a representaion of folder structure, the DS of tree can be defined as:

```typescript
interface Tree {
  id: string;
  // id of file content if it's located directly under "this" folder
  blob_1_id?: string; 
  blob_2_id?: string;
  ...
  // id of sub folder if it's located directly under "this" folder
  sub_tree_1_id?: string; // exist if a sub 
  sub_tree_2_id?: string;
  ...
}
```

As you can see, tree by itself doesn't use a lot of space either. It has an id & reference ids of files & folders under it.

Finally, files are stored as blobs. It's DS can be defined as:

```typescript
interface Blob {
  id: string;
  content: Binary; // actual file content, if it's text file, you can print it out using `git cat-file -p {{blob id}}`
}
```
