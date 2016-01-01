#Git Cheat Sheet
##initial setup
find version of Git: `git --version`

##Help
`man git`

`git help`

## General use
Initialize new Git repo: `git init`

Add current directort to commit: `git add .`

Add a given file to commit: `git add FILE`

Commit changes: `git commit -m "Message"`

Remove files from Git: `git rm index.html`

Undo modifications (restore files from latest commited version): `git checkout -- index.html`

Restore file from a custom commit (in current branch): `git checkout 6eb715d -- index.html`

##Update & Delete
Test-Delete untracked files:
`git clean -n`

Delete untracked files (not staging):
`git clean -f`

Unstage (undo adds):
`git reset HEAD index.html`

Commit to most recent commit:
`git commit --amend -m "Message"`

Update most recent commit message:
`git commit --amend -m "New Message"`

##Branch
Show branches: `git branch`

Create branch: `git branch branchname`

Change to branch: `git checkout branchname`

Rename branch: `git branch -m branchname new_branchname` or: `git branch --move branchname new_branchname`

Show all completely merged branches with current branch: `git branch --merged`

Delete merged branch (only possible if not HEAD): `git branch -d branchname` or: `git branch --delete branchname`

Delete not merged branch: `git branch -D branch_to_delete`

##Merge
True merge (fast forward): `git merge branchname`

Merge to master (only if fast forward): `git merge --ff-only branchname`

Merge to master (forc a new commit): `git merge --no-ff branchname`

Stop merge (in case of conflicts): `git merge --abort`

##Gitignore & Gitkeep
About: https://help.github.com/articles/ignoring-files

Useful templates: https://github.com/github/gitignore

Add or edit gitignore:  `vim .gitignore`

##Log
Show commits: `git log`

Show oneline-summary of commits: `git log --oneline`

Show oneline-summary of commits with full SHA-1: `git log --format=oneline`

Show oneline-summary of the last three commits: `git log --oneline -3`

Show only custom commits:
`git log --author="Sven"`
`git log --grep="Message"`
`git log --until=2013-01-01`
`git log --since=2013-01-01`

Show only custom data of commit:
`git log --format=short`
`git log --format=full`
`git log --format=fuller`
`git log --format=email`
`git log --format=raw`

Show changes: `git log -p`

Show every commit since special commit for custom file only: `git log 6eb715d.. index.html`

Show changes of every commit since special commit for custom file only: `git log -p 6eb715d.. index.html`

Show stats and summary of commits: `git log --stat --summary`

Show history of commits as graph: `git log --graph`

Show history of commits as graph-summary: `git log --oneline --graph --all --decorate`


##Compare
Compare modified files: `git diff`

Compare modified files and highlight changes only: `git diff --color-words index.html`

Compare modified files within the staging area: `git diff --staged`

Compare branches: `git diff master..branchname`

Compare branches like above: `git diff --color-words master..branchname^`

Compare commits: `git diff 6eb715d` `git diff 6eb715d..HEAD` `git diff 6eb715d..537a09f`

Compare commits of file: `git diff 6eb715d index.html` or: `git diff 6eb715d..537a09f index.html`

Compare without caring about spaces: `git diff -b 6eb715d..HEAD` or: `git diff --ignore-space-change 6eb715d..HEAD`

Compare without caring about all spaces: `git diff -w 6eb715d..HEAD` or: `git diff --ignore-all-space 6eb715d..HEAD`

Useful comparings: `git diff --stat --summary 6eb715d..HEAD`

Blame: `git blame -L10,+1 index.html`


##Collaborate
Show remote: `git remote`

Show remote details: `git remote -v`

Add remote origin from GitHub project: `git remote add origin https://github.com/user/project.git`

Add remote origin from existing empty project on server: `git remote add origin ssh://root@123.123.123.123/path/to/repository/.git`

Remove origin: `git remote rm origin`

Show remote branches: `git branch -r`

Show all branches: `git branch -a`

Compare: `git diff origin/master..master`

Push (set default with `-u`): `git push -u origin master`

Push to default: `git push origin master`

Fetch: `git fetch origin`

Pull: `git pull`

Pull specific branch: `git pull origin branchname`

Merge fetched commits: `git merge origin/master`

Clone to localhost: `git clone https://github.com/user/project.git` or: `git clone ssh://user@domain.com/~/dir/.git`

Clone to localhost folder: `git clone https://github.com/user/project.git ~/dir/folder`

Clone specific branch to localhost: `git clone -b branchname https://github.com/user/project.git`

Delete remote branch (push nothing): `git push origin :branchname` or: `git push origin --delete branchname`

## Sparse Checkout
sparse checkout is used to only checkout specific subfolders in a project

for a new project
  * create folder `mkdir <repo> && cd <repo`
  * initilize the repo: `git init`
  * set the remote: `git remote add –f <name> <url> `
  * enable sparse checkout: `git config core.sparsecheckout true`
  * edit sparse checkout file: `vim .git/info/sparse-checkout`
  * add directories to sparse checkout file from .git root ex. `Dir\sub-dir`
  * Checkout the remote repo: git pull <remote> <branch>

for an existing project:
  * enable sparse checkout: `git config core.sparsecheckout true`
  * edit sparse checkout file: `vim .git/info/sparse-checkout`
  * add directories to sparse checkout file from .git root ex. `Dir\sub-dir`
  * update the working tree `git read-tree -mu HEAD`
