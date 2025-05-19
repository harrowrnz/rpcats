# RealPython uv Tutorial & Git + GitHub Notes

## Background

While Ive been using astral's uv for a while as a replacement for pip, Id never really explored using it for projects.

When RealPython did a tutorial on it, I felt it was about time to look into starting to use it more fully. 
See [Managing Python Projects With uv: An All-in-One Solution – Real Python](https://realpython.com/python-uv/)

Alongside this, Im also working with git for the first time, and putting this project into github. 

## Tutorial Synopsis

### Install uv

#### Ubunutu

On Ubutunu, snap is the easiest as it should auto-update, though isnt always the absolutely latest release

#### Mac

install using homebrew and then will again, be auto-updated.

### Create uv Project

> **Note**: 
> 
> Install git prior to creating a project, or else the git-related project components will not be created

In parent directory (above where you want the project), run:

```shell
uv init rpcats
```

This will create the following structure with a placeholder main.py

```shell
rpcats/
├── .git
├── .gitignore
├── main.py
├── pyproject.toml
├── .python-version
└── README.md
```

### Using Git for Version Control

[https://docs.github.com/en/get-started/using-git/about-git](https://docs.github.com/en/get-started/using-git/about-git) 

[https://docs.github.com/en/get-started/start-your-journey/hello-world](https://docs.github.com/en/get-started/start-your-journey/hello-world)

#### Setup

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

Main GitHub 'Getting Started' URL above suggests this basic workflow for setting up a Git Repo. Note that you have to create a new blank repo on GitHub first, either using GUI or GitHub CLI (`gh`).

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

#### Create local Git repo

First of all, check current status of git repo:

```shell
git status

On branch master

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

On branch master

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

#### Create New Repo in GitHub

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

#### Push Local Repo to GitHub Repo

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

#### Create New Git Branch

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

#### Update Base Project Files

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

Updated README.md

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

Push

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

#### Merge Feature to main (See Note)

> **Note:** I think you should do a pull request in GitHub to merge a feature to main, doing it this way somewhat breaks the model if you had multiple people working on the repo.

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

#### Re-Sync local Repo with GitHub

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

### First Run of Project

#### Check out new feature branch in Git

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

#### Run Project for First Time

Change into the rpcats folder and then run project for first time. This will create the venv (`.venv` folder) automatically and will also create a new file, `uv.lock`

```shell
uv run main.py

Using CPython 3.13.3 interpreter at: /usr/bin/python3.13
Creating virtual environment at: .venv
Hello from rpcats!
```

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
