# batch-example

This repository will store and allow versioning and approval of a batch configuration.

This repository **only** contains exported configuration.  It does not contain any binary files (eg equipment-model.cfg nor system state or log files).  These are excluded using the **.gitignore** file.


you will need to:

give a bot user (eg batch-bot) write access

generate a new token for this user https://sigyl.com/git/user/settings/applications with 

* write:issue
* write:repository
* read:user

set an action secret called BOT_TOKEN to it


## change process

tea is here (i had to change docker file to just be based on node:latest)

https://gitea.com/gitea/tea/src/branch/main/docs/CLI.md


On ?tag ? push to master
clone master
branch deployed
yml -> xml
push deployed


pull to production PC and import

pull to development, import, modify, export
push from development to format branch

on format-branch pull, xml -> yml, push to product-development and PR

### FTBatch development pc on development branch

```sh
?git branch -D format-branch
git checkout format-branch
git merge deployed

```

make changes and export files

commit and push back to server

```sh
git add -A
git commit
git push origin format-branch
```

### format-bot pc

```sh
git branch -D format-branch
git fetch origin
git checkout -b format-branch
git checkout master
git pull
git branch -D product-development
git checkout -b product-development
git merge --squash --no-commit --no-ff --strategyoption=theirs format-branch

```

run the formatter

```sh
git add -A
git commit
git push origin product-development
git push origin --delete format-branch

```

create a pull request

```sh
git fetch --tags
gotea pr c --base=master --head=product-development   --repo another-user/batch-example --title="WIP: this is a PR! it rocks!"

```

closing a pull request (not used)
```sh
gotea pr close --repo another-user/batch-example 11
```

build

```sh

git checkout master
git pull
git checkout deployed
git merge master
```

make xml files

```sh
git add -A
git commit
git push origin deployed
```
