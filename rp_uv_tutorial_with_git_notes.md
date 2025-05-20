# RealPython uv Tutorial & Git & GitHub Notes

## Background

See [Managing Python Projects With uv: An All-in-One Solution – Real Python](https://realpython.com/python-uv/)

> :information_source: **Note**:
> Most of the intial part of this document was done using Ubuntu 25.04 before moving onto a Mac, so most installation commands will relate to Ubuntu rather than MacOS.
> Assumption is that local git client is already installed.

## Install uv

#### Ubunutu

On Ubutunu, snap is the easiest as it should auto-update, though isnt always the absolutely latest release

```shell
sudo snap install astral-uv --classic
```

#### Mac

install using homebrew and then will again, be auto-updated.

```shell
brew install uv
```

## Create uv Project

> **Note**: 
> 
> Install git prior to creating a project, or else the git-related project components will not be created

In parent directory (above where you want the project), run:

```shell
uv init rpcats
```

This will create the following structure with a placeholder main.py  
Note that the git scaffolding is also created with a `.git` folder and a `.gitignore` file

```shell
rpcats/
├── .git
├── .gitignore
├── main.py
├── pyproject.toml
├── .python-version
└── README.md
```

## Using Git & GitHub for Version Control

[https://docs.github.com/en/get-started/using-git/about-git](https://docs.github.com/en/get-started/using-git/about-git) 

[https://docs.github.com/en/get-started/start-your-journey/hello-world](https://docs.github.com/en/get-started/start-your-journey/hello-world)

### Local Git Configuration

Tell git who I am:

```shell
git config --global user.email "harrowr@gmail.com"
git config --global user.name "HarrowRNZ"
```

Set git to use main instead of master:

```shell
git config --global init.defaultBranch main
```

```shell
git config --list

user.email=harrowr@gmail.com
user.name=HarrowRNZ
init.defaultbranch=main
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
```

### GitHub Generic "Getting Started" Workflow

> **Note**:
> [GitHub: Getting Started](https://docs.github.com/en/get-started/using-git/about-git) suggests this basic workflow for setting up a Git Repo.  
> Note that you have to create a new blank repo on GitHub first, either using GUI or GitHub CLI (`gh`).

```shell
# create a new directory, and initialize it with git-specific functions
git init my-repo

# change into the `my-repo` directory
cd my-repo

# create the first file in the project
touch README.md

# git isn't aware of the file, stage it
git add README.md

# take a snapshot of the staging area
git commit -m "add README to initial commit"

# provide the path for the repository you created on github
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git

# push changes to github
git push --set-upstream origin main
```

### Create local Git repo

As uv already scaffolds a git repo as part of creating a uv project, creating the repo (as per previous section) isnt necessary.

First of all, check current status of git repo:

```shell
git status

On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    .gitignore
    .python-version
    README.md
    main.py
    pyproject.toml

nothing added to commit but untracked files present (use "git add" to track)
```

Files must be staged into git before they can be committed.

Stage newly created uv project files (. does all files in directory)

```shell
git add .
```

Now show current git status again:

```shell
git status

On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
    new file:   .gitignore
    new file:   .python-version
    new file:   README.md
    new file:   main.py
    new file:   pyproject.toml
```

Commit the uv project to Git

```shell
git commit -m "Initial Commit for rpcats uv project"
[main (root-commit) 63e5942] Initial Commit for rpcats uv project
 5 files changed, 24 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 .python-version
 create mode 100644 README.md
 create mode 100644 main.py
 create mode 100644 pyproject.toml
```

Now show status

```shell
git status

On branch main
nothing to commit, working tree clean
```

### Create New Repo in GitHub

Will need to install `gh` (GitHub CLI) if not already installed.

```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key C99B11DEB97541F0
sudo apt-add-repository https://cli.github.com/packages
sudo apt update
sudo apt install gh
```

https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories?tool=cli

https://docs.github.com/en/github-cli/github-cli/about-github-cli

```shell
gh repo create rpcats
To get started with GitHub CLI, please run:  gh auth login
Alternatively, populate the GH_TOKEN environment variable with a GitHub API authentication token.
```

Authenticate:

```shell
gh auth login

? What account do you want to log into? GitHub.com
? What is your preferred protocol for Git operations on this host? HTTPS
? Authenticate Git with your GitHub credentials? Yes
? How would you like to authenticate GitHub CLI? Login with a web browser

! First copy your one-time code: 1234-5678
Press Enter to open github.com in your browser... 
- gh config set -h github.com git_protocol https
✓ Configured git protocol
✓ Logged in as harrowrnz
```

Create GitHub Repo:

```shell
gh repo create

? What would you like to do? Push an existing local repository to GitHub
? Path to local repository .
? Repository name rpcats
? Description RealPython uv Tutorial Repo
? Visibility Public
✓ Created repository harrowrnz/rpcats on GitHub
  https://github.com/harrowrnz/rpcats
? Add a remote? No
```

### Push Local Repo to GitHub Repo

```shell
git remote add origin https://github.com/harrowrnz/rpcats.git
git branch -M main
git push -u origin main
```

```shell
git remote add origin https://github.com/harrowrnz/rpcats.git
git branch -M main
git push -u origin main

Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 4 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (7/7), 702 bytes | 702.00 KiB/s, done.
Total 7 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/harrowrnz/rpcats.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

### Create New Git Branch

As an experiment in branching, Im going to create a new feature prior to updating the base uv project files.

```shell
git checkout -b initial_base_project_updates

Switched to a new branch 'initial_base_project_updates'
```

```shell
git status

On branch initial_base_project_updates
nothing to commit, working tree clean
```

Push new branch to GitHub - note that HEAD is just the current branch that Im sitting in presently. I could also have specified the actual branch name

```shell
git push -u origin HEAD
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: 
remote: Create a pull request for 'initial_base_project_updates' on GitHub by visiting:
remote:      https://github.com/harrowrnz/rpcats/pull/new/initial_base_project_updates
remote: 
To https://github.com/harrowrnz/rpcats.git
 * [new branch]      HEAD -> initial_base_project_updates
branch 'initial_base_project_updates' set up to track 'origin/initial_base_project_updates'.
```

### Update Base Project Files

Ive updated the Description field in `pyproject.toml`

```shell
cat pyproject.toml

[project]
name = "rpcats"
version = "0.1.0"
description = "RealPython uv Project Tutorial, also using local Git & GitHub"
readme = "README.md"
requires-python = ">=3.13"
dependencies = []
```

```shell
git status

On branch initial_base_project_updates
Your branch is up to date with 'origin/initial_base_project_updates'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   pyproject.toml

no changes added to commit (use "git add" and/or "git commit -a")
```

```shell
git commit -a -m "Updated pyproject.toml description field for project"

[initial_base_project_updates bb3ca6f] Updated pyproject.toml description field for project
 1 file changed, 1 insertion(+), 1 deletion(-)
```

```shell
git status

On branch initial_base_project_updates
Your branch is ahead of 'origin/initial_base_project_updates' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

Push local repo changes to GitHub

```shell
git push -u origin HEAD

Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 433 bytes | 433.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/harrowrnz/rpcats.git
   63e5942..bb3ca6f  HEAD -> initial_base_project_updates
branch 'initial_base_project_updates' set up to track 'origin/initial_base_project_updates'.
```

Updated `README.md`

```shell
git status

On branch initial_base_project_updates
Your branch is up to date with 'origin/initial_base_project_updates'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

```shell
git commit -a -m "Updated README.md"

[initial_base_project_updates 718dfab] Updated README.md
 1 file changed, 11 insertions(+)
```

Push to GitHub

```shell
git push

Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 685 bytes | 685.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/harrowrnz/rpcats.git
   bb3ca6f..718dfab  initial_base_project_updates -> initial_base_project_updates
```

### Merge Feature to main (See Note)

> :information_source: **Note**:
> I think you should do a pull request in GitHub to merge a feature to main. Doing it this way somewhat breaks the model if you had multiple people working on the repo. 
> 
> ChatGPT has provided me some suggestions for the GitHub config, as well as local git hook setup to stop merges to main locally.

- [ ] :memo: **TODO**: Add suggested github and git local hook suggestions

Change into to main branch

```shell
git checkout main

Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

```shell
git status
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

```shell
git log

commit da842e1ea2535e2504ac8fd2b4fa5b0a8b8ba29c (HEAD -> main, origin/initial_base_project_updates, initial_base_project_updates)
Author: HarrowRNZ <harrowr@gmail.com>
Date:   Sun May 18 19:52:57 2025 +1200

    Updated README.md again

commit 718dfab0f1385d4b6291f6e8427e2a846ce70fdf
Author: HarrowRNZ <harrowr@gmail.com>
Date:   Sun May 18 19:41:40 2025 +1200

    Updated README.md

commit bb3ca6fae50e0c9e5c43bb512c775d649cfefcb4
Author: HarrowRNZ <harrowr@gmail.com>
Date:   Sun May 18 19:27:45 2025 +1200

    Updated pyproject.toml description field for project

commit 63e5942c091c789aa97d9536ffcba79a3d9c8922 (origin/main)
Author: HarrowRNZ <harrowr@gmail.com>
Date:   Sun May 18 18:31:21 2025 +1200

    Initial Commit for rpcats uv project
```

```shell
git push

Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/harrowrnz/rpcats.git
   63e5942..da842e1  main -> main
```

After this, i went onto GitHub GUI and deleted the branch I had been working in, so only had main.

### Re-Sync local Repo with GitHub

To force a sync back to local repo from GitHub after the above merge to main and deleting the branch:

```shell
git pull --prune

From https://github.com/harrowrnz/rpcats
 - [deleted]         (none)     -> origin/initial_base_project_updates
Already up to date.
```

```shell
git branch --list 
  initial_base_project_updates
* main
```

## First Run of Project

### Check out new feature branch in Git

```shell
git checkout main

Already on 'main'
Your branch is up to date with 'origin/main'.
```

```shell
git status

On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

```shell
git checkout -b initial_development

Switched to a new branch 'initial_development'
```

```shell
git status

On branch initial_development
nothing to commit, working tree clean
```

### Run Project for First Time

Change into the rpcats folder and then run project for first time.  
This will create the venv (`.venv` folder) automatically and will also create a new file, `uv.lock`

```shell
uv run main.py

Using CPython 3.13.3 interpreter at: /usr/bin/python3.13
Creating virtual environment at: .venv
Hello from rpcats!
```

### Review Changes and Update Git

```shell
git status

On branch initial_development
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    uv.lock

nothing added to commit but untracked files present (use "git add" to track)
```

```shell
git add .
```

```shell
git status

On branch initial_development
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    new file:   uv.lock
```

```shell
git commit -a -m "rpcats project - post first \"uv run main.py\""

[initial_development 9b820b2] rpcats project - post first "uv run main.py"
 1 file changed, 8 insertions(+)
 create mode 100644 uv.lock
```

### Push to GitHub

```shell
git push --set-upstream origin initial_development

Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 398 bytes | 398.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'initial_development' on GitHub by visiting:
remote:      https://github.com/harrowrnz/rpcats/pull/new/initial_development
remote: 
To https://github.com/harrowrnz/rpcats.git
 * [new branch]      initial_development -> initial_development
branch 'initial_development' set up to track 'origin/initial_development'.
```

## Move Computer (GitHub & Git)

After several additional changes to files in `initia_development` branch, I pushed to Git and then moved over to my main workstation. The Ubuntu box I was intially working on is primarily a docker server and I just happened to be on there when I started the tutorial. Good test for using multiple computers with a remote repo 😃

### Clone Repo from GitHub

```shell
git clone https://github.com/harrowrnz/rpcats.git

Cloning into 'rpcats'...
remote: Enumerating objects: 34, done.
remote: Counting objects: 100% (34/34), done.
remote: Compressing objects: 100% (30/30), done.
remote: Total 34 (delta 13), reused 17 (delta 2), pack-reused 0 (from 0)
Receiving objects: 100% (34/34), 11.39 KiB | 685.00 KiB/s, done.
Resolving deltas: 100% (13/13), done. Change to current working branch
```

### Review listing of current branch

Change into repo folder

```shell
cd rpcats/
```

```shell
ls -al

total 40
drwxr-xr-x@  8 harrowfr  staff   256 21 May 03:14 .
drwxr-xr-x@  8 harrowfr  staff   256 21 May 03:14 ..
drwxr-xr-x@ 12 harrowfr  staff   384 21 May 03:14 .git
-rw-r--r--@  1 harrowfr  staff   109 21 May 03:14 .gitignore
-rw-r--r--@  1 harrowfr  staff     5 21 May 03:14 .python-version
-rw-r--r--@  1 harrowfr  staff  1172 21 May 03:14 README.md
-rw-r--r--@  1 harrowfr  staff    84 21 May 03:14 main.py
-rw-r--r--@  1 harrowfr  staff   188 21 May 03:14 pyproject.toml
```

List the branches in the repo

```shell
git branch -a

* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/initial_development
  remotes/origin/main
```

```shell
git checkout initial_development

branch 'initial_development' set up to track 'origin/initial_development'.
Switched to a new branch 'initial_development'
```

Review rpcats directory, note changes compared with previous listing

```shell
ls -al

total 88
drwxr-xr-x@ 11 harrowfr  staff    352 21 May 03:14 .
drwxr-xr-x@  8 harrowfr  staff    256 21 May 03:14 ..
drwxr-xr-x@ 12 harrowfr  staff    384 21 May 03:14 .git
-rw-r--r--@  1 harrowfr  staff    109 21 May 03:14 .gitignore
-rw-r--r--@  1 harrowfr  staff      5 21 May 03:14 .python-version
-rw-r--r--@  1 harrowfr  staff   1172 21 May 03:14 README.md
-rw-r--r--@  1 harrowfr  staff   1485 21 May 03:14 main.py
-rw-r--r--@  1 harrowfr  staff   1014 21 May 03:14 markdown_callout_shortcodes.md
-rw-r--r--@  1 harrowfr  staff    188 21 May 03:14 pyproject.toml
-rw-r--r--@  1 harrowfr  staff  14473 21 May 03:14 rp_uv_tutorial_with_git_notes.md
-rw-r--r--@  1 harrowfr  staff    126 21 May 03:14 uv.lock
```

### Commit Changes to Local Git

Ive now updated this document with the notes for moving computer, so push changes to GitHub before going to bed :smile:

Check for changes to branch (ie any new files)

```shell
git status

On branch initial_development
Your branch is up to date with 'origin/initial_development'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   rp_uv_tutorial_with_git_notes.md

no changes added to commit (use "git add" and/or "git commit -a")
```

```shell
git commit -a -m "Moved computer & updated tutorial document"

[initial_development 35ac510] Moved computer & updated tutorial document
 1 file changed, 75 insertions(+), 23 deletions(-) 
```

Confirm changes commited

```shell
git status

On branch initial_development
Your branch is ahead of 'origin/initial_development' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

### Push to GitHub

As I have moved computer, need to reauthenticate to GitHub

```shell
gh auth login

? Where do you use GitHub? GitHub.com
? What is your preferred protocol for Git operations on this host? HTTPS
? Authenticate Git with your GitHub credentials? Yes
? How would you like to authenticate GitHub CLI? Login with a web browser

! First copy your one-time code: 1234-5678
Press Enter to open https://github.com/login/device in your browser... 
✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
✓ Logged in as harrowrnz
```

Now push branch

```shell
git push

Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 10 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 1.21 KiB | 1.21 MiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/harrowrnz/rpcats.git
   2839fa6..35ac510  initial_development -> initial_development
```

Review my local git config - need to update this so that Im using my personal GitHub username for commits on this repo.

- [ ] :memo: **TODO**: Set config for local repo to personal GitHub account

```shell
git config --list
init.defaultbranch=main
user.email=first.last@work.com
user.name=First Last
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
remote.origin.url=https://github.com/harrowrnz/rpcats.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.main.remote=origin
branch.main.merge=refs/heads/main
branch.initial_development.remote=origin
branch.initial_development.merge=refs/heads/initial_development
```
