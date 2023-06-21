Git is a distributed SCM(source control management) tool. It's safe, flexible, efficient but complicated. Aside from its numerous commands, sometimes you has to understand how it works internally to use it well :(

Suppose you go through all the hurdles to try to understand its internals (you know git is a content-addressable file system, it uses SHA-1, it's model for storage is linkage between commit -> tree -> blob), you still have to learn how to use it's command line interface which can be daunting to look at. Never the less we have to use it just because it's popular.

### config

under `$HOME` folder, a file named `.gitconfig` stores global git configs, here's an example:

```git
[user]
	name = john
	email = john1996@gmail.com
[init]
	defaultBranch = main
[core]
	# force git to be case sensitive (which it by default is not under macOS)
	ignoreCase = false
[alias]
	fo = fetch origin
	fu = fetch upstream
```

under current folder, a folder name `.git` stores all things related to git. inside it a file named `config` stores local git config

if the same item exist both in local & global git config, local config will take effect (overwriting global config)

- `git config --global --list`

- `git config --local --list`

- `git config --local user.name 'john'`

- `git config --local user.email 'john2000@gmail.com'`

- `git config --local http.proxy http://proxyUsername:proxyPassword@proxy.server.com:port`

### init

- `git init {{ foldername }}` (foldername is optional, by default it's the current directory)

- `git clone {{ url }}` (url protocol could be ssh, git, http[s] or ftp[s]. example of url using git protocol: `git@github.com:librz/shell-scripts.git`)

### init & basic inspection

- `git --version`

- `git status` (status of current branch & it's relation with its remote tracking branch)

- `git remote -v` (v for verbose mode,)

- `git branch -av` (without the -a flag, git will only show local branches; with the -v flag, commit id & message of each head will be printed)

- `git log --oneline -n10 --decorate --graph`

- `git diff` by default, git diff without any option or parameter shows diff between working tree & HEAD

- `git diff --cached` show diff between staging area & HEAD

- `git diff --shortstat {{commit id}}` (the --shortstat shows only number of changed files as well as added & deleted lines)

- `git diff b77bfd22 e67337d4` diff between commit `b77bfd22` and `e67337d4`

- `git diff e67337d4 e67337d4~` diff between commit `e67337d4` and it's parent commit (`~` sign means parent)

- `git show-ref --heads` print all 

### stage & commit

- stage(track) files/folders: `git add file1.js folder1`

- stage all changes(tracked & untracked files): `git add .` or `git add -A`

- stage updates to tracked files: `git add -u`

- mv or rename file/folder: `git mv add.js Add.js`

- commit changes in staging area: `git commit -m 'update readme'`

- unstage all changes (moving changes from staging area to working tree): `git reset HEAD` or `git restore --staged .` (note git restore is only available after v2.23)

- discard all changes in working tree: `git checkout -- .` or `git restore .` (note git restore is only available after v2.23)

### sync (local <=> remote)

- `git fetch {remote}` fetch status of all branches from remote

- `git fetch {remote} {branch}` fetch status of specified branch from remote

- `git fetch --prune {{remote name}}` Without `--prune `, remote-tracking branches will stay forever on local cache even some of them may have been removed on remote

- `git push` push to remote branch (suppose you already specified a remote branch before)

- `git push -u {remote} {branch}` set upstream branch & push to it

- `git push -f {remote} {branch}` force push to remote branch, this is DANGEROUS (never force push to a shared branch)

- `git pull` pull changes from remote branch

sometimes, when you do `git status` or `git pull`, git tells you `your local branch has diverged with remote`, usually it means the `HEAD` of your local barnch & remote branch is different (having different commit IDs). If you want to forfeit your local `HEAD`, you could just do `git reset --hard {remote}/{branch}`. [More details](https://stackoverflow.com/questions/2452226/master-branch-and-origin-master-have-diverged-how-to-undiverge-branches)

### branching

- switch branch `git checkout {branch}` or `git switch {branch}` (note: git switch is a relatively new command, available in git v2.32(release in 2019-08-16) or above)

- start a new branch based on head of current branch: `git checkout -b {branch}` or `git switch -c {branch}`

- start a new branch based on commit whose commit id is 021b1e39: `git checkout -b {branch} 021b1e39`

- delete local branch: `git branch -D {branch}`

- delete remote branch: `git push {remote} --delete {branch}`

- merge current branch with another local branch: `git merge {branch}`

- merge current branch with remote branch: `git merge {remote}/{branch}`

- rename current branch: `git branch -m {new name}`

- start a new branch based on head of remote branch: `git checkout -b {branch} {remote}/{branch}`

- start a new branch based on head of remote branch but do not track the remote branch `git checkout -b {branch} --no-track {remote}/{branch}` (this can be useful when you want to checkout a branch from the official branch but do not want or simply don't have the access to push directly to it, instead you want to push to a forked repo and then raise a PR to merge into the official repo's branch)

### history navigation

- `git checkout 021b1e39`

### rewrite history

- change commit message of last commit: `git commit --amend -m "new message"` (note: this will delete the old commit & generate a new commit with a new commit id and message)
- include more changes to last commit without updating commit message: `git commit --amend --no-edit`
- change any message in history: `git rebase -i {{ any parent commit id before the commit you want to change }}` then change the action for the targeted commit from `pick` to `reword`
- squash multiple commits into one: `git rebase -i {{ any parent commit id before the commits you want to squash }}` then change the action for commits you want to squash from `pick` to `squash` (note you should pick the oldest commit among the commits you want to squash to serve as the destination for squash) (note you can reorder commits when rebasing but it can cause conflict, only do it when you are very confident of what you are doing)
- delete commits until a certain commit(dangerous): `git reset --hard {{commit id}}`, you can also do `git reset --hard HEAD~{{count}}` (`count` is the number of commits you'd like to delete)
- delete commits but keep the changes in working directory: `git reset --soft {{commit id}}` or `git reset --soft HEAD~{{count}}` (I think you can emit the `--soft` as it's default behavior)
- push to remote branch after history is rewritten: `git push -f` (note: -f is dangerous especially when there are other team members who work on the same branch, only do this if the commit you are rewriting is already pushed to remote branch & no other team member is working on that remote branch)

### stash

stash changes that are not ready for commit & you may need to come back to it later

git stashes are orgnized as a stack

- stash changes(tracked files only): `git stash`
- stash changes in tracked files & give it a message: `git stash push -m "to be continue: feature blabla"`
- stash changes(including untracked files): `git stash -u` or `git stash --include-untracked`
- list all stashes: `git stash list`
- apply latest stash: `git stash pop` or `git stash apply`
- apply/drop specific stash: `git stash apply/drop stash@{index}`
- drop all stashes: `git stash clear`
- show changes in a stash: `git stash show stash@{index}`

### miscellaneous

- list all files tracked by git: `git ls-tree --full-tree --name-only -r {commit}`
- tell git to stop traking file: `git rm --cached {file}`
- tell git to stop tracking folder & files under it: `git rm -r --cached {folder}`

---

### about the `.git` folder

the `.git` folder is the databse of git, if you do `rm -rf .git`, all trakcing done by git will be lost. This is how you can `uninit` a git repo.

several interesting files/folders under `.git` folder

- `config` file: stores all local git configs
- `HEAD` file: HEAD (as its name suggests) refers to the head (latest commit) of current branch you are on
- `refs/heads` folder: stores head(latest commit) of each branch
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

Finally, files are stored as blobs. It's stucture can be defined as:

```typescript
interface Blob {
  id: string;
  content: Binary; // actual file content, if it's text file, you can print it out using `git cat-file -p {{blob id}}`
}
```

More Info: https://git-scm.com/book/en/v2/Git-Internals-Git-Objects

### thinking

- What's the point of staging area? Why not commit changes in working tree directly?

Fine grained control. Suppose you made a lot of changes in working tree & only want to commit some of changes (maybe because the rest changes are experimental & not ready for commit), you can stage only the changes you want to commit & then commit them.
