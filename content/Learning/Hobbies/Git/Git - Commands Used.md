---
id: Git - Commands Used
aliases: Git Commands Used When "Re-Learning" Git
tags:
  - git
  - GitHub
  - bootdev
  - linux
module: ICDT 1201Y
author: S.Sunhaloo
date: 2025-07-30
status: Completed
---

- [[Git - Introduction#Installing Git]]

```console
# windows users
winget install Git.Git

# macos users - see homebrew package manager or xcode-select
# sorry

# debian / debian based distribution
sudo apt-get install git

# I use Arch BTW
sudo pacman -S git

# fedora based distributions
sudo dnf install git
```

- [[Git - Getting Started#Reading The Friendly Manual]]

```bash
# Linux
man git
```

```powershell
# Windows
git help git
```

- [[Git - Getting Started#Setup `git`]]

```bash
# new command - setup username
git config set --global user.name "github_username"

# deprecated equivalent - setup username
git config --global user.name "github_username"

# new command - setup email
git config set --global user.email "github_email"

# deprecated equivalent - setup email
git config --global user.email "github_email"

# new command - change default branch
git config set --global init.defaultBranch main

# deprecated equivalent - change default branch
git config --global init.defaultBranch main

# new command - setup code editor
# NOTE: if you use VS C*de / Sumblime Text, you need to add the `--wait`
# so that git will stop doing / running other commands
# until you close the editor, i.e
git config set --global core.editor "code --wait"

# INFO: I use VIM BTW!!!
# WARNING: choose only one!
git config set --global core.editor "nvim"

# deprecated equivalent - setup code editor
git config --global core.editor "core-- wait"
```

- [[Git - Local Repositories#Initialisation of Local Repository]]

```bash
# create the following directories inside the `Desktop` folder
mkdir -p ~/Desktop/learning_git/first_local_repo

# go into that directory
cd ~/Desktop/learning_git/first_local_repo

# initialise the local repository
git init
```

- [[Git - Local Repositories#Creating Files]]

```bash
# check the states of the file in our repository
git status

# run the shorter version of `git status`
git status --short
```

- [[Git - Local Repositories#Adding Files To The Staging Area]]

```bash
# add our `README.md` file to the staging area
git add README.md

# add everything all at once
git add .
```

- [[Git - Local Repositories#Removing Files]]

```bash
# remove all files / folders in the staging area
git rm -r --cached .

# if you want to remove individual files
git rm --cached file_name.ext file_2_name.ext

# if you want to remove a combination of files and folders
# INFO: see how we are passing the '-r' flag here!
git rm -r --cached file_name.ext file_2_name.ext folder_name/

# if you want to remove individual files
git rm --cached file_name.ext file_2_name.ext

# if you want to remove a combination of files and folders
# INFO: see how we are passing the '-r' flag here!
git rm -r --cached file_name.ext file_2_name.ext folder_name/
```

- [[Git - Local Repositories#Committing and Commit Messages]]

```bash
# simply run the commit command
# our "configured" / default editor should show up
git commit
```

- [[Git - Local Repositories#Let's Go Committing]]

```bash
# remove the unwanted files
rm main.py joe_mama.txt

# or we could do something interesting like so
# WARNING: this should be run inside the repository
find . -type f -not -name "*.md" -delete

# run the status command
git status

# add everything that we want to commit
git add .
```

```bash
# commit without opening any editor
git commit -m "Second Commit Ever"

# optionally, we can run the command found below
git commit -m "Second Commit Ever" -m "In this version, we remove unwanted files"
```

- [[Git - Local Repositories#Fucking Up]]

```bash
# write a new / modify last commit message
git commit --amend

# change the second commit message with '-m' flag
git commit --amend -m "Completely New Commit Message" -m "Yes I have changed the commit message for the second commit"
```

- [[Git - Local Repositories#Git Log]]

```bash
# simple vanilla command
git log

# more information on the screen
git log --oneline

# another combination of the above
# the "graph" will show stuff like merging and others
git log --oneline --graph
```

```bash
# replicate 'less' on Windows
git log | more
```

```bash
# replicate windows
git log --no-pager
```

- [[Git - Local Repositories#Undo Last Commit But Keep Changes]]

```bash
# remove the latest commit but keep files staged
git reset --soft HEAD~1
```

- [[Git - Local Repositories#Undo Last Commit And Unstage Changes]]

```bash
# remove the latest commit
# also remove the files from the staged area
# place them into the working directory
git reset --mixed HEAD~1
```

- [[Git - Local Repositories#Undo Last Commit And Delete Changes!]]

```bash
# completely remove commit and associated changes
git reset --hard HEAD~1
```

- [[Git - Hashes#Git Cat-File]]

```bash
# view contents of a specific commit
git cat-file -p aea6060a504ed9dab225edbe3995553142f4df1e
```

- [[Git - Hashes#Get Content Of File From Hash]]

```bash
# get the output of our main commit "message" hash
git cat-file -p aea6060a504ed9dab225edbe3995553142f4df1e
```

```bash
# get the output of the git tree's hash for that commit hash
git cat-file -p ca5b09e0d5b1c827e03fe61264ab6fda00b0d35f
```

```bash
# get the actual contents found inside 'README.md'
git cat-file -p a6bdfb839192eeb2a841b7e76ed3541cc164deef
```

- [[Git - Branches#Simple Git Branches Commands]]

```bash
# list all the branches in our local repository
git branch
```

- [[Git - Branches#Testing My Private Repository!]]

```bash
# show both local and remote repositories
git branch -a
```

- [[Git - Branches#Renaming Branches]]

```bash
# rename our local 'main' branch to 'deeznuts'
git branch -m main deeznuts
```

- [[Git - Branches#Create New Branches]]

```bash
# create a new local branch called 'the_goat'
git branch the_goat
```

```bash
# switch the newly created local branch
git switch the_goat
```

```bash
# create the new branch 'new-branch-name'
# immediately switch to the newly created branch
git switch -c new-branch-name
```

- [[Git - Branches#Deleting Branches]]

```bash
# we are now going to delete the newly created 'the_goat' branch
git branch -d the_goat
```

- [[Git - Branches#Delete "Remote Tracked" Branch On Local]]

```bash
# list out all the remote branches in my private repository
git branch -r
```

- [[Git - Merge#Git Adding, Committing]]

```bash
# add all changes to the staging area all at once
git add .
```

```bash
# commit the changes by writing a simple message
git commit -m "Our Real Second Commit Ever"
```

- [[Git - Merge#Some More Changes]]

```bash
# add the 'README.md' file to the staging area
git add README.md

# write a simple commit message with the '-m' flag
# NOTE: again, this is just for "show" don't do this
git commit -m "Update: Added Things To 'README.md' File"
```

- [[Git - Merge#Creation Of Branch]]

```bash
# create new branch 'shit' and switch to it instantly
git switch -c shit
```

```bash
# create a new branch 'test' and immediately switch to it
# this branch will / should start from the first commit ever!
git switch -c test aea6060a504ed9dab225edbe3995553142f4df1e
```

```bash
# delete the temporary branch
git branch -d test
```

[[Git - Merge#Making Changes and Commits in New Branch]]

```bash
# add the 'README.md' file to the staging area
git add README.md

# write a little commit message directly in the terminal
git commit -m "A: Added Memes"
```

- [[Git - Merge#Make Some More Changes]]

```bash
# add the 'joe_mama.txt' file to the staging area
git add joe_mama.txt

# write a little commit message directly in the terminal
# WARNING: See how these commit messages does not have any meaning
# don't do that specially if you are working with people
git commit -m "A: Added More Memes"
```

- [[Git - Merge#Merging Branches]]

```bash
# switch to our 'deeznuts' branch
git switch deeznuts
```

```bash
# merge the 'shit' branch's content to 'deeznuts'
git merge shit
```

```bash
# check if we have "diagonal" lines in log graphs
git log --oneline --graph
```

```bash
# run the merge commit and explicitly mention NO fast-forwarding!
# INFO: again if you want 'shit' --> 'deeznuts'
#need to run command in 'deeznuts'
git merge --no-ff shit
```

- [[Git - Merge#Actually Merging Merging]]

```bash
# switch to our 'shit' branch for some shitty actions
git switch shit
```

```bash
# add the required file to the staging area
git add joe_mama.txt

# commit the changes without opening editor
git commit -m "A: Switch to Linux Line Added"
```

```bash
# add the required file to the staging area
git add main.py

# commit the changes without opening editor
git commit -m "A: Required Comments"
```

```bash
# switch to your lovely `deeznuts` branch
git switch deeznuts
```

```bash
# add the required files to the staging area
git add joe_mama.txt

# commit the changes made
git commit -m "A: YouTube Links"
```

```bash
# switch to our "main" 'deeznuts' branch
git switch deeznuts
```

```bash
# merge the contents of 'shit' with 'deeznuts'
git merge shit
```

>[!NOTE]
>Visit '[[Git - Merge#Actually Merging Merging]]' to see how to fix the conflicts!

- [[Git - Rebase#Preparing Repository For Rebasing]]

```bash
# add the 'README.md' file to the staging area
git add README.md

# commit the changes made
git commit -m "I Like Cars"
```

```bash
# add the required file to the lovely staging area
git add README.md

# commit the changes made
git commit -m "The RX-7 FD goes brap brap brap brap"
```

```bash
# create branch 'new_one'
# based on our "fifth" commit on 'deeznuts' ( hehe )
# immediately switch to that branch after creation
git switch -c new_one 7e3edc9360b6a4544ca7badcf57ceb72f0b657b7
```

- [[Git - Rebase#Let's Create Some Commits]]

```bash
# add the 'joe_mama.txt' file to the staging area
git add joe_mama.txt

# commit the changes that we made
git commit -m "I don't want conflict... Fingers Crossed"
```

```bash
# add the required file to the staging area
git add README.md

# commit the changes
git commit -m "Remove a line from Markdown File"
```

- [[Git - Rebase#Running The Commands]]

```bash
# switch to the 'new_one' branch
git switch new_one
```

```bash
# rebase against 'deeznuts' branch
git rebase deeznuts
```

- [[Git - Rebase#What If We Rebase Again "Main"]]

```bash
# switch to our "main" 'deeznuts' branch
git switch deeznuts

# check if we are actually inside the correct branch
# INFO: not a mistake... run the fucking command again
git switch deeznuts
```

```bash
# rebase against our "main" / 'deeznuts' branch
git rebase new_one
```

- [[Git - Rebase#Make A Change And Commit]]

```bash
# stage the required file
git add .

# commit the changes without opening the editor
git commit -m "We should be linear now boys... and girls"
```

- [[Git - Remote Repositories#Add Original Repository As Remote]]

```bash
# setup the "initial" git repository
git init
```

```bash
# track the remote repository 'first_local_repo'
# whereby the remote name is "origin"
# which points to local folder 'first_local_repo'
git remote add origin ../first_local_repo
```

- [[Git - Remote Repositories#The Solution To The Problem]]

```bash
# download the objects and references from another repository
git fetch
```

```bash
# check the remote commit logs for 'shit' branch
git log origin/shit
```

```bash
# merge the contents of 'origin/deeznuts' branch with 'main'
git merge origin/deeznuts
```

```bash
# count the number of items inside the 'objects' folder
ls -la | wc -l
```

- [[Git - Remote Repositories#Git - Push and Git - Pull#Making Some Changes]]

```bash
# add the new files to the staging area
git add main.js

# commit the changes made
git commit -m "Create New Javascript File"
```

- [[Git - Remote Repositories#Cloning Repository]]

```bash
# clone my dotfiles repository onto our local machine
git clone https://github.com/Sunhaloo/dotfiles.git
```

- [[Git - Remote Repositories#Creation of `first_local_repo` on GitHub]]

```bash
# link that local repository to our remote repository
git remote add origin git@github.com:Sunhaloo/first_local_repo.git
```

```bash
# push with the '-u' flag for the first time
# this will setup the upstream branch
git push -u origin main
```

- [[Git - Remote Repositories#Clone Repository Again]]

```bash
# clone the 'first_local_repo' inside 'Downloads' folder
# I am going to clone with SSH link
git clone git@github.com:Sunhaloo/first_local_repo.git ~/Downloads/first_local_repo
```

```bash
# add the required file to the staging area
git add main.js

# commit the change made to the LOCAL repository
git commit -m "Added A Single Line To JS File"
```

```bash
# push the changes made to the remote repository
git push
```

```bash
# pull the latest changes from the remote repository
git pull
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!