# Git Commands - How to avoid reading the manual

Hi. Thanks for reading this. These are the git commands I use. Don't just use them without thinking.

Sometimes I ran into problems. I have added the solutions. 

When possible, I share the sources where I found the information.

*Note: I use Mac. There might be some difference for Linux and PC users.*

## Remove git from a folder
After cloning a repo from github, you should remove their reference to github and eventually replace it with your own. So that you don't try to edit their project. 
````
rm -rf .git
````
That will blow away all git-related info.

This is also useful if you want to start the over. 

[Source: How to remove git tracking from a project](https://stackoverflow.com/questions/4754152/git-how-to-remove-git-tracking-from-a-project)

## New Project and Repository

… or create a new repository on the command line.
````
echo "# My New Project" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/my-github-profile-name/My-New-Project.git
git push -u origin main
````

*Note that the `-u` in the push command is important. This allows you to simply write `git push` in the future.*

|**Command**|**Explanation**|
| :- | :- |
|`git clone <link>`|Clone project from github|
|<p>or ...</p><p>`mkdir new\project`</p><p>`cd new_project`</p><p>`git init`</p><p>**`hub create -p`**</p>|<p>Create new project manually</p><p></p><p></p><p>It will get the name of your folder</p><p></p><p>https://hub.github.com/hub-create.1.html</p>|
|<p>`git status`</p>|What has changed since last commit|
|<p>`git add .`</p><p>`git add filename`</p>|<p>git add all</p><p>Adding the changes to the staging area</p>|
|`git commit -m "message"`|Commit the changes to the history|
|<p>`git log`</p>|Change history|
|<p>`git diff filename or folder`</p><p>`git diff`</p><p></p>|<p>What has changed</p><p>No argument gives all changes</p><p>Only changes not added or committed. Only unstaged files</p>|
|`git pull origin main`|Download latest changes from github|

## Most used commands
Before making changes, you should always make a new branch. 


On the project, select Settings, Branches, Branch protection rule. Enter `main` in the Branch name pattern, and check the first setting *Require pull request reviews before merging*. You will not regret it. 

````
git checkout -b name-of-new-branch

> make your changes

git status
git add .
git commit -m 'description of changes'
git push origin name-of-new-branch
git checkout main

> accept pull request on Git Hub

git pull origin main
git push heroku main (If you are deploying your chages to Heroku)
````

## More reading
[Git Cheatsheet](http://www.ndpsoftware.com/git-cheatsheet.html)

[Solving Conflicts](https://github.com/Eschults/useful_stuff#conflicts-solving)

[When cloning](https://gist.github.com/jagregory/710671)

[Readme.md: Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

# Troubleshooting

## Persisting password
If Github keeps asking for your password, try this. 

````
ssh-add -K   
````

## Check your path to GitHub and Heroku
Is your link to GitHub missing? Try this. 
````
test-app-vue-01 git:(main) git remote -v

heroku	https://git.heroku.com/test-app-vue-01.git (fetch)
heroku	https://git.heroku.com/test-app-vue-01.git (push)
origin	https://github.com/my-github-profile-name/test-app-vue-01.git (fetch)
origin	https://github.com/my-github-profile-name/test-app-vue-01.git (push)
````

## Install git-open
Do you want a quick way to open the project page on GitHub?

[Source: git open](https://github.com/paulirish/git-open)

Type `git open` to open the repo website (GitHub, GitLab, Bitbucket) in your browser.

````
npm install --global git-open
````

## Your branch is ahead of 'origin/develop'
You are getting this message. I recommend you google it, but here are some ideas. 

On branch develop

Your branch is ahead of 'origin/develop' by 3 commits.

(use `git push` to publish your local commits)

nothing to commit, working tree clean

````
git reset --hard origin/develop
````

or

````
git reset --hard origin/main
````

*Note: Please, read about the `reset` command before using it.*

## How do I force “git pull” to overwrite local files?
You made some changes and now you regret. Google it. Do not use the `reset` option before undstanding what it does.. 

https://stackoverflow.com/questions/1125968/how-do-i-force-git-pull-to-overwrite-local-files

**Important:** If you have any local changes, they will be lost. With or without `--hard option`, any local commits that haven't been pushed will be lost. If you have any files that are *not* tracked by Git (e.g. uploaded user content), these files will not be affected.

I think this is the right way:

````
git fetch --all
````

Then, you have two options:

````
git reset --hard origin/main
````

OR If you are on some other branch:

````
git reset --hard origin/<branch_name>
````
## If you made changes on the main branch
I told you not to do it. But I know your problem. 
You got all excited about your new idea and forgot to branch. 
Don't worry. You are certainly not the first. 

````
git stash 
git checkout -b tempbranch 
git stash pop
````

then …

````
git status
git add .
git push origin tempbranch

> make pull request and merge

git checkout main
git pull origin main
````

and continue your work as if nothing happened. 

## Merge your branch with main
````
git checkout main
git pull origin main
git checkout your-branch
git merge main
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
You don't want everything in your folder or on your computer to be copied to GitHub. 
Try to find someone who already have a good gitignore file for that kind of project and stick to it. 

[Source: Ignoring files](https://help.github.com/articles/ignoring-files/)

https://www.atlassian.com/git/tutorials/saving-changes/gitignore

1. In Terminal, navigate to the location of your Git repository.
1. Enter `touch .gitignore` to create a *.gitignore* file.

or copy it from another similar project

## SSH
https://docs.github.com/en/github/authenticating-to-github/about-ssh

## Setting your username in Git
If Git don't know who you are, try this.

https://help.github.com/en/articles/setting-your-username-in-git

Setting your Git username for every repository on your computer.

Set a Git username:

````
$ git config --global user.name "Finn Pedersen"
````

Confirm that you have set the Git username correctly:

````
$ git config --global user.name
> Finn Pedersen
````

Setting your email address for every repository on your computer.

Set an email address in Git. You can use your GitHub-provided no-reply email address or any email address.

````
$ git config --global user.email "finnpedersenfrance@gmail.com"
````

Confirm that you have set the email address correctly in Git:

````
$ git config --global user.email
>finnpedersenfrance@gmail.com
````

## Help, I keep getting a 'Permission Denied (publickey)' error when I push!
https://gist.github.com/adamjohnson/5682757#help-i-keep-getting-a-permission-denied-publickey-error-when-i-push
