# Some git commands

This is some git commands that I usually use.

**Clone a repository**
```bash
git clone <URL> [<DEST Directory>]
```

**Clone from specific branch**
```bash
git clone --branch <BRANCH NAME> <URL> [<DEST Directory>]
```

**Pull code from remote master branch and merge to current banch**
```bash
git pull origin master
```

**Push code from local DEV branch to remote MASTER branch**
```bash
git push origin dev:master
```

**Create local branch**
```bash
git checkout -b <BRANCH NAME>
```

**Switch local branch**
```bash
git checkout <BRANCH NAME>
```
<!--more-->
**List all branch**
```bash
git branch -a
```

**Delete local branch**
```bash
git branch -d <BRANCH NAME>
```

**Delete remote branch**
```bash
git push origin --delete <BRANCH NAME>
```

**View files status**
```bash
git status
```

**Add files to commit**

. mean all changed files.
```bash
git add .
```

**Rename a branch**

```bash
git branch -m "new-branch-name"
git branch -m "old-branch-name" "new-branch-name"
```
(updating ....)

