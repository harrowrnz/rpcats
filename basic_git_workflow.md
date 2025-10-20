# Basic GIT Workflow

```shell
# ... checkout main branch / other branch ...
git checkout main

# ... create branch ...
git checkout -b feature/add-utils

# ... edit code ...

# ... stage files ...
git add src/utils.py    # add single file
git add .               # add all files in dir

# ... commit branch ...
git commit -m "Add new helper functions"

# ... switch to main branch ...
git checkout main

# ... merge feature branch to main ... 
git merge feature/add-utils

# ... OPTIONALLY delete feature branch ...
git branch -d feature/add-utils
```

# Example branch names
ℹ️ Tip:
Use descriptive branch names:  
* feature/add-logging  
* bugfix/fix-cli-error  
* chore/update-readme  

