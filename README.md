# Git Commands - How to avoid reading the manual

Hi. Thanks for reading this. These are the git commands I use. Don't just use them without thinking.

Sometimes I ran into problems. I have added the solutions. 

When possible, I share the sources where I found the information.

## Remove git from a folder
After cloning a repo from github, you should remove their reference to github and eventually replace it with your own. 

`rm -rf .git` should suffice. That will blow away all git-related info.

[Source: How to remove git tracking from a project](https://stackoverflow.com/questions/4754152/git-how-to-remove-git-tracking-from-a-project)

## New Project and Repository

### …or create a new repository on the command line
````
echo "# My New Project" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/my-github-profile-name/My-New-Project.git
git push -u origin master
````

|**Command**|**Explanation**|
| :- | :- |
|`git clone *link*`|Clone project from github|
|<p>or ...</p><p>`mkdir new\project`</p><p>`cd new_project`</p><p>`git init`</p><p>**`hub create`**</p>|<p>Create new project manually</p><p></p><p></p><p>It will get the name of your folder</p><p></p><p>https://hub.github.com/hub-create.1.html</p>|
|<p>`git status`</p>|What has changed since last commit|
|<p>`git add .`</p><p>`git add filename`</p>|<p>git add all</p><p>Adding the changes to the staging area</p>|
|`git commit -m "message"`|Commit the changes to the history|
|<p>`git log`</p>|Change history|
|<p>`git diff filename or folder`</p><p>`git diff`</p><p></p>|<p>What has changed</p><p>No argument gives all changes</p><p>Only changes not added or committed. Only unstaged files</p>|
|`git pull origin master`|Download latest changes from github|

## Most used commands
````
git checkout -b name-of-new-branch

> make your changers

git status
git add .
git commit -m 'description of changes'
git push origin name-of-new-branch
git checkout master

> accept pull request on Git Hub

git pull origin master
git push heroku master (If you are deploying your chages to Heroku)
````

## More reading
[Git Cheatsheet](http://www.ndpsoftware.com/git-cheatsheet.html)

[Solving Conflicts](https://github.com/Eschults/useful_stuff#conflicts-solving)

[When cloning](https://gist.github.com/jagregory/710671)

[Readme.md: Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

## Persisting password
````
ssh-add -K   
````

## Check your path to Github and Heroku
````
test-app-vue-01 git:(master) git remote -v

heroku	https://git.heroku.com/test-app-vue-01.git (fetch)
heroku	https://git.heroku.com/test-app-vue-01.git (push)
origin	https://github.com/my-github-profile-name/test-app-vue-01.git (fetch)
origin	https://github.com/my-github-profile-name/test-app-vue-01.git (push)
````

## Install git-open
[git open](https://github.com/paulirish/git-open)

Type `git open` to open the repo website (GitHub, GitLab, Bitbucket) in your browser.

````
npm install --global git-open
````

## Your branch is ahead of 'origin/develop'
On branch develop

Your branch is ahead of 'origin/develop' by 3 commits.

(use `git push` to publish your local commits)

nothing to commit, working tree clean

````
git reset --hard origin/develop
````

or

````
git reset --hard origin/master
````

## How do I force “git pull” to overwrite local files?
https://stackoverflow.com/questions/1125968/how-do-i-force-git-pull-to-overwrite-local-files

**Important:** If you have any local changes, they will be lost. With or without `--hard option`, any local commits that haven't been pushed will be lost. If you have any files that are *not* tracked by Git (e.g. uploaded user content), these files will not be affected.

I think this is the right way:

````
git fetch --all
````

Then, you have two options:

````
git reset --hard origin/master
````

OR If you are on some other branch:

````
git reset --hard origin/<branch_name>
````
## If you made changes on the master branch
````
git stash 
git branch -b tempbranch 
git stash pop
````

then …

````
git status
git add .
git push origin tempbranch
make pull request and merge
git checkout master
git pull origin master
````

and continue your work as if nothing happened. 

## Merge your branch with master 
````
git checkout master
git pull origin master
git checkout your-branch
git merge master
````

This procedure works. 

if conflict solve the conflict and make a

````
git add .
git commit -m 'conflict solved'
git push
````

## Syncing a fork
https://help.github.com/articles/syncing-a-fork/

## Clone or Fork
[The difference between forking and cloning a repository](https://github.community/t5/Support-Protips/The-difference-between-forking-and-cloning-a-repository/ba-p/1372)

## Git show-branches
````
git show-branches --all
````
## Blame
Click the Blame button on GitHub to see changes to a single file.

## Add .gitignore
[Source: Ignoring files](https://help.github.com/articles/ignoring-files/)

https://www.atlassian.com/git/tutorials/saving-changes/gitignore

1. In Terminal, navigate to the location of your Git repository.
1. Enter `touch .gitignore` to create a *.gitignore* file.

or copy it from another similar project

## SSH
https://help.github.com/en/articles/connecting-to-github-with-ssh#platform-windows


## Setting your username in Git
https://help.github.com/en/articles/setting-your-username-in-git

Setting your Git username for every repository on your computer.

Set a Git username:

````
$ git config --global user.name "my-github-user-name"
````

Confirm that you have set the Git username correctly:

````
$ git config --global user.name
> my-github-user-name
````

Setting your email address for every repository on your computer.

Set an email address in Git. You can use your GitHub-provided no-reply email address or any email address.

````
$ git config --global user.email "my-github-email@gmail.com"
````

Confirm that you have set the email address correctly in Git:

````
$ git config --global user.email
>my-github-email@gmail.com
````


## Help, I keep getting a 'Permission Denied (publickey)' error when I push!
https://gist.github.com/adamjohnson/5682757#help-i-keep-getting-a-permission-denied-publickey-error-when-i-push
