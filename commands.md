---
layout: reference
permalink: /commands/
---

## List of commands used

`cd`
change directory (defaults to home, eg `/home/tom` on Mac/Linux, `C:\Users\tom` on Windows)

`mkdir planets`
create a new folder (directory) in the current directory

`cd planets`
change directory into planets

`ls`
list files and directories in the current directory

`ls -a`
list files and directories, including hidden

`git config --global user.name "J Smith"`
configure git to use your name

`git config --global user.email "j.smith@ed.ac.uk"`
configure git to use your email

`git config --global color.ui "auto"`
configure git to give coloured output

`git config --global core.editor "notepad"`
configure git to use notepad for commit messages

`git config --list`
list the settings in your git configuration

`git --help`
help for the `git` command

`git config --help`
help for the `git config` command

`git init`
create a new git repository in the current directory

`cat mars.txt`
echo the contents of mars.txt

`git status`
check the status of the git repository in the current directory

`git diff`
show the difference between the last commit and the working directory

`git add mars.txt`
add `mars.txt` to the staging area

`git diff --staged`
show the difference between the last commit and the staging area

`git commit`
commit changes from the staging area (you will be prompted to add a message
using the editor configure above)

`git commit -m "Start notes on Mars as a base"`
commit changes with a short message

`git log`
show commit logs

`git log -1`
show the latest commit message

`git log --oneline`
show commit logs, just the commit id and the first line of the message

`git diff HEAD mars.txt`
show the difference between the last commit and the working directory

`git diff HEAD~1 mars.txt`
show the difference between the last-but-one commit and the working directory

`git diff f22b25e mars.txt`
show the difference between the commit with id `f22b25e...` and the working directory

`git checkout HEAD mars.txt`
replace mars.txt with the version from the latest commit

`git checkout -- mars.txt`
replace mars.txt with the version from the latest commit

`git checkout f22b25e mars.txt`
replace mars.txt with the version from the commit with id `f22b25e...`

`git log --patch mars.txt`
show commit logs, along with the changes made to `mars.txt` at each step

`git log --patch HEAD~3 HEAD~1 *.txt`
show commit logs, along with the changes made to `mars.txt` at each step

`git add -f a.dat`
add `a.dat` to the staging area, even though it would normally be ignored by
git because of rules in the `.gitignore` file

`git remote add origin https://github.com/vlad/planets.git`
add a reference to a remote repository at `https://github.com/vlad/planets.git`,
calling it `origin`

`git remote -v`
list all references to remotes in this repository

`git push origin master`
push commits from the local `master` branch to the remote at `origin`

`git pull origin master`
pull commits from the remote at `origin` to the local `master` branch

`git remote add broken_example https://github.com/this/url/is/wrong`
add a reference to a remote repository at `https://github.com/this/url/is/wrong`,
calling it `broken_example`

`git remote set-url broken_example https://github.com/this/url/should/fix/it`
set the URL of the `broken_example` remote to `https://github.com/this/url/should/fix/it`

`git remote remove broken_example`
remote the reference to the `broken_example` remote

`git clone https://github.com/nismod/workshop`
clones the remote repository from `https://github.com/nismod/workshop` into a
new folder `workshop`

`git branch new_feature`
creates a new branch called `new_feature`

`git checkout new_feature`
checks out the `new_feature` branch to the working directory

`git checkout master`
checks out the `master` branch to the working directory

`git merge new_feature`
merges the commits from the `new_feature` branch into `master`

`git branch -d new_feature`
delete the `new_feature` branch
