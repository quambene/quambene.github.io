<!-- markdownlint-disable MD001 -->

# Git

- [Subcommands](#subcommands)
- [Status](#status)
- [Init](#init)
  - [Init remote repo](#init-remote-repo)
- [Clone](#clone)
- [Remote](#remote)
- [Checkout](#checkout)
- [Switch](#switch)
- [Branch](#branch)
- [Add](#add)
- [Commit](#commit)
- [Push](#push)
  - [Push existing project](#push-existing-project)
- [Fetch](#fetch)
- [Merge](#merge)
  - [Merge feature branch](#merge-feature-branch)
- [Pull](#pull)
- [Reset](#reset)
- [Revert](#revert)
- [Stash](#stash)
- [Clean](#clean)
- [Cherry-pick](#cherry-pick)
- [Tag](#tag)
  - [Rename tag](#rename-tag)
- [Worktree](#worktree)
- [Submodule](#submodule)
- [Show](#show)
- [Log](#log)
- [Diff](#diff)
  - [Compare branches](#compare-branches)
- [Config](#config)
- [Gitignore](#gitignore)
- [Repo size](#repo-size)
- [Pull request (PR)](#pull-request-pr)

### Subcommands

``` bash
git status          # Show current branch
git init            # Create an empty Git repository or reinitialize an existing one
git clone           # Clone remote repository
git remote          # Manage remote repositories
git checkout        # Switch to branch
git switch          # Switch branches
git branch          # List, create, or delete branches
git add             # Selects changes
git commit          # Records changes locally
git push            # Shares changes
git fetch           # Downloads new data from a remote repository; create and update remote-tracking branches
git merge           # Merge new data from a repository
git pull            # Integrates new data from a remote repository into current working files (fetch + merge)
git reset           # Remove files from the current index
git revert          # Revert commit
git stash           # Stash the changes in a working directory
git clean           # Remove untracked files from the working tree
git cherry-pick     # Apply the changes introduced by some existing commits
git show            # Show commit
git log             # Show commit history
git diff            # Show diffs
git config          # Get and set repository or global options
```

### Status

Displays paths that have differences between the index file and the current HEAD commit, paths that have differences between the working tree and the index file, and paths in the working tree that are not tracked by Git.

``` bash
git status
```

### Init

``` bash
git init # Create an empty Git repository or reinitialize an existing one
git init --bare # Initialize repo (without working directory)
git init --shared=group
git init --shared=0NNN # e.g. --shared=0660
```

#### Init remote repo

``` bash
sudo mkdir <my_dir>.git # Create directory
sudo chown -R git:git <my_dir>.git # Set ownership
sudo chmod -R g+rwx <my_dir>.git # Set permissions
cd <my_dir>.git
git init --bare
```

### Clone

``` bash
git clone user@host:path # Clone remote repo
git clone git@<host_name>:<repo_owner>/<repo_name>.git # Clone remote repo
git clone git@<host_name>:<repo_owner>/<repo_name>.git <folder_name> # Clone into specific folder
git clone --depth <N> https://<host_name>/<repo>.git # Clone commit history with depth=N
git clone --mirror <repo-url> temp-dir # Copy full git repo
```

### Remote

``` bash
git remote -v # Show remote repos
git remote show origin # Show more information
git remote rename origin <repo_name> # Rename repo
git remote rm origin # Remove remote repo

git remote add <shortname> <url> # Add remote repo named <shortname> for the repository at <url>
git remote add origin git@<host_name>:<repo_owner>/<repo_name>.git # SSH
git remote add origin https://<host_name>/<repo_owner>/<repo_name>.git # HTTPS
```

### Checkout

``` bash
git checkout <branch_name> # Switch to branch
git checkout -b <branch_name> # Create and switch to new branch
git checkout <commit_id> # Switch to commit
git checkout --track origin/<branch_name> # Create <branch_name> and set up "upstream" 
```

### Switch

``` bash
git switch <branch_name> # Switch branch
```

### Branch

``` bash
git branch # Show branches
git branch -a # Show all branches
git branch -r # Show remote branches
git branch --no-merged # Show list of branches which haven't been merged into your current branch
git branch <branch_name> # Create new branch
git branch -m <new_name> # Rename current branch
git checkout <old_name> && git branch -m <new_name> # Rename branch
git checkout master && git branch -m <old_name> <new_name> # Rename branch
git branch -d <branch_name> # Delete local branch (--delete)
git branch -D <branch_name> # Delete local branch (--delete --force)
git push origin --delete <branch_name> # Delete remote branch
git branch --merged | grep -v \* | xargs git branch -D # Delete all local branches
git branch --contains <branch_name> # Check whether a branch has been merged into another branch
```

### Add

``` bash
git add <my_file> # Stage my_file
git add -A # inlcudes "git add ." and "git add -u"
git add . # doesn't stage any 'rm' actions
git add -u # doesn't add any new files
```

### Commit

``` bash
git commit --amend # Edit commit message; amend recent commit
git commit -m 'My message' # Commit with message
git commit -a # Combine git add and commit
git commit -am "My message" # Add and commit
```

### Push

``` bash
git push # Push changes to the remote repo
git push --tags # Push tags to remote repo
git push -u <repo_name> <branch_name> # --set-upstream
git push -u origin <branch_name> # Set up local branch <branch_name> to track remote branch <branch_name> from origin
git push --force # Overwrite repo
```

#### Push existing project

``` bash
git init
git add -A
git commit -m 'My message'
git remote add origin git@<host_name>:<account_name>/<repo_name>.git
git push -u origin master
```

### Fetch

``` bash
git fetch
git fetch <branch> # Download new data from remote branch
git fetch -p # Prune remote branches
```

### Merge

``` bash
git merge <branch_name> # Merge branch_name into current branch
git merge --no-ff --no-commit <branch_name> # --no-ff flag for constructing a merge instead of fast-forwarding
git merge --abort # Equivalent to git reset --merge when MERGE_HEAD is present; MERGE_HEAD is present when a merge is in progress
git merge --squash <branch_name> # Squash all commits into one commit
```

#### Merge feature branch

``` bash
git checkout master
git pull origin master
git merge --no-ff --no-commit <branch_name>
git commit # no commit message required; commit message "Merge branch 'branch_name'" created automatically
git push origin master
```

### Pull

``` bash
git pull # git fetch plus either git rebase or git merge
git pull origin <branch_name>
```

### Reset

``` bash
git reset # Remove files from the current index
git reset <file> # Unstage file; remove file from the current index
git reset HEAD <file> # Unstage file; remove file from the current index
git reset --hard HEAD # going back to HEAD; any changes since last commit are discarded
git reset --hard HEAD~ # going back to the commit before HEAD
git reset --hard HEAD~2 # going back two commits before HEAD
```

### Revert

``` bash
# Revert (published commit)
git revert <commit_id> # Revert last commit
git revert <commit_id> -m 1 # Reverting a merge commit
git revert <commit_id> -m 2

# Revert multiple commits
git revert --no-commit <commit_id>
git revert --no-commit <commit_id>
git commit -m "My message"
```

### Stash

``` bash
git stash # Saves local modifications
git stash pop # Reverts local modifications

git stash -u # --include-untracked
```

### Clean

``` bash
git clean -f # Remove untracked files from the working tree
```

### Cherry-pick

``` bash
git cherry-pick <commit_id> # Apply the changes introduced by some existing commit
```

### Tag

``` bash
git tag v1.0.0 # Tag version
git tag v1.0.0 -m 'My message' # Tag version with message
git tag --delete <tag_name> # Delete tag
git push --delete origin <tag_name> # Delete tag in remote repo
git tag --list # Show all tags
git tag -l # Show all tags
git pull --tags
git push --tags
git checkout tags/<tag_name> -b <branch_name> # Check out specific tag
```

#### Rename tag

``` bash
git tag <new_tag> <old_tag>
git tag -d <old_tag>
git push origin <new_tag> :<old_tag>
```

### Worktree

``` bash
git worktree add <folder> <branch> # Add worktree
git worktree list # List all worktrees
git worktree remove <folder> # Remove worktree
```

### Submodule

``` bash
git submodule add git@<host_name>:<repo_owner>/<repo_name>.git <my_submodule>
git commit -m "Add my submodule"

git submodule status
git submodule add -b master
git submodule update
git submodule update --remote
git submodule update --init --recursive # First time repo is checked out
git submodule update --recursive --remote # Update remote branches
git submodule foreach git pull origin master
```

### Show

``` bash
git show <commit_id> # Show commit
```

### Log

``` bash
git log
git log --pretty=oneline # Pretty-print
git log --stat # Show lines added/changed/deleted
git log master
git log origin/master

# Pretty-print commit graph
git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(auto)%d%C(reset)'
```

### Diff

``` bash
git diff HEAD~1 # Show diff in last commit
git diff --name-only HEAD~1 # Show diff files in last commit

# Difftool
git difftool dev # Compare to feature branch
git difftool master # Compare to feature branch
git difftool master origin/master # Compare local and remote branch
git difftool --tool-help # Help
git difftool --tool=meld # Set difftool
git difftool <branch_1> <branch_2>
git difftool --tool=vscode <branch_1> <branch_2>
git difftool HEAD <commit-id> -- <file-name>
```

#### Compare branches

``` bash
git diff master # Compare to branch master and list differences
git diff --name-only master # Compare to branch master and list files
git diff --name-only master origin/master -- <path> # Show different files
git log <branch1>..<branch_2> # List commit differences

# Returns the commits that are present in the feature branch but are not unavailable in the master branch
git log master..feature −−oneline
```

### Config

``` bash
git config --global user.name "my_username" # Set username
git config --global user.email "my_email" # Set email
git config --list # Check settings
```

### Gitignore

``` bash
# Exclude from .gitignore
git reset <file_name> # Unstage file
git rm --cached <file_name> # Remove the file from the repo
git add -f <file_name> # Force to exclude file from gitignore ("!<file_name>")

# Include in .gitignore
git rm -rf --cached . # removes all files from the repository
git add . # adds them back
```

### Repo size

``` bash
du -hs .git
```

### Pull request (PR)

``` bash
git clone git@<host_name>:<repo_owner>/<repo_name>.git
git remote rm origin
git remote add origin git@<host_name>:<me>/<repo_name>.git
git remote add upstream git@<host_name>:<repo_owner>/<repo_name>.git
git checkout master
git pull upstream master
# git pull --rebase upstream master
git checkout -b <my_feature_branch>
git commit -m "My fix"
git push origin <my_feature_branch>
```
