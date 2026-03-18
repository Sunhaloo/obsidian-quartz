---
id: Git - Branches
aliases: Branches in Git
tags:
  - git
  - GitHub
  - linux
author: S.Sunhaloo
date: 2025-07-31
status: Completed
---

## List of Contents

- [[#Git Branches]]
	- [[#Simple Git Branches Commands]]
	- [[#Renaming Branches]]
	- [[#Create New Branches]]
	- [[#Deleting Branches]]

---

# Git Branches

If you go ahead and [simply run our lovely](https://www.youtube.com/watch?v=OtjsHokKUgI&t=9s) little `git status` command, you are going to see this:

```console
On branch main
nothing to commit, working tree clean
```

You notice that its saying that we are "*On branch main*".

Now, let's say that you and your friend are working on the same project. But a dilemma happened. You guys don't really know what *data structure* is going to result in higher performance **for your specific project**.

Therefore, you guys decides to **split up** and work so as to find out what is the "*best*" data structure.

Now, you are also working on a **remote** repository! This means that if you try to make a change, your friend will also receive *that change*. How are you going to prevent that? How are you guys going to prevent conflicting with each other's "*separate*" codes?

Well, here comes **[Git Branches](https://git-scm.com/docs/git-branch)**. It will allow you to *diverge* from the `main` ( *or `master`* ) branch and therefore, the original code will still be **intact**!

Then when you guys finally figure out what is the best data structure for your program... Then you can simply [merge](https://git-scm.com/docs/git-merge) them!

## Simple Git Branches Commands

Go ahead and run the following command, right now, right here in your **local** repository:

```bash
# list all the branches in our local repository
git branch
```

```console
* main
```

As you can see we only have **one** *local* branch!

### Testing My Private Repository!

I have a **private** and **remote** repository whereby I keep all of my Obsidian Notes backup! Now for each *semester* or noticeable change, I **make** a new branch, switch to that branch and then do all of my "*backup*".

This private repository that I have, currently has 5 different branches... Therefore, running `git branch` should have 5 ( *or more* ) branches.

> I think you know where this is going!

```console
* main
```

> [!WARNING]
>
> > That is why one **needs** to *read* the fucking manual... "*RTFM Bro*!!!"
>
> Simply running the `git branch` command will **only** show all the *local* branches that are present. But it will <strong> <span style="color: red;"> not</span> </strong> show any **remote** branches!
>
> Therefore, to be able to show all the **remote branches** found; we need to pass in the `-a` flag!
>
> ```bash
> # show both local and remote repositories
> git branch -a
> ```
>
> ```console
> * main
>  remotes/origin/HEAD -> origin/main
>  remotes/origin/UOM_L1S1
>  remotes/origin/UOM_L1S2
>  remotes/origin/UOM_L1_COMPLETE
>  remotes/origin/UTM-2024
>  remotes/origin/main
> ```

> [!INFO] I Like To Think That `git branch` = `ls`!
> Yes, because if I do for example `ls` ( *I use [eza](https://github.com/eza-community/eza) BTW* ).
>
> ```console
>  Desktop    󰉍 Downloads   ly-session.log   Obsidian      󰉏 Pictures   Screenshots   Videos
> 󰲂 Documents   GitHub     󱍙 Music            'OBS Studio'   Public     Templates     Wallpapers
> ```
>
> But we all know that running `ls -la` will show everything!
>
> > I am not going to *paste* that here because there is a lot of hidden files / directories in my **home directory**!
>
> Therefore, you could say that `git branch` $=$ `ls` and `git branch -la` $=$ `ls -la`!
>
> Like running `git branch -la` will give us the output that you see above.

## Renaming Branches

So there are some times where one is going to have to **rename** his / her repository!

Hence, to show this; I am going to rename our `main` branch to `deeznuts`!

```bash
# rename our local 'main' branch to 'deeznuts'
git branch -m main deeznuts
```

Hence, running a simple `git status` or `git branch` command, we can see that our branch has changed from `main` to `deeznuts`.

- Running `git status`:

```console
On branch deeznuts
nothing to commit, working tree clean
```

- Running `git branch`:

```console
* deeznuts
```

## Create New Branches

> This is where its going to get interesting! Let's get straight into it ( *[that's what she said](https://www.youtube.com/watch?v=dBUGfs9rwms)* )!

Run the following command, to create a new, **local** branch named `the_goat`:

```bash
# create a new local branch called 'the_goat'
git branch the_goat
```

> [!NOTE]
> This is just for show! Please do use the correct **naming conventions** when using *naming* git branches!

But you will see that we are still in `deeznuts`... Therefore, we are going to have to **manually** switch to `the_goat`.

The switch, we just need to `switch`!

```bash
# switch the newly created local branch
git switch the_goat
```

Therefore, running `git status` or "*better*" `git branch` will show us that we are currently on the `the_goat` branch!

- Running `git status`:

```console
On branch the_goat
nothing to commit, working tree clean
```

- Running `git branch`:

```console
  deeznuts
* the_goat
```

> See how the position of the `*` character has changed...

> [!TIP]
> Normally when we are creating a new branch, we would like to **immediately** switch to the newly created branch.
>
> Therefore, we have a little **shortcut** for this!
>
> ```bash
> # create the new branch 'new-branch-name'
> # immediately switch to the newly created branch
> git switch -c new-branch-name
> ```

### Same Commits!

I am currently in the new `the_goat` branch! What do you think will appear if I go ahead and execute the `ls` command inside that branch?

> Will it be empty? Will it be different? Will it be the same? Will it be "*same, same but different*"?

```console
 joe_mama.txt   main.py  󰂺 README.md
```

As you can see the *contents* inside the *newly* created branch is the <strong> <span style="color: orange;"> same</span> </strong> as our `deeznuts` branch!

> [!INFO] The Reason...
> The reason as to why this happens, its because **creating** a *new branch* is "*commit-based*"
>
> What I am trying to say, its that creating a new commit still has **all** the *commits* made from the "*`main`*" branch.
>
> For example, I recently created `UOM_L1_COMPLETE`... But running a `git log`, I can still see all the *shit* that I have done before
>
> > This is actually so cool!
>
> But I am now going to show you the *commit message* for my **private** repository. Instead I am going to show you the number of lines when running the `git log` command
>
> ```bash
> # find the number of lines for 'git log'
> git log | wc -l
> ```
>
> > I don't know the appropriate Powershell command... *Sorry Not Sorry*! Switch to Linux You Fool!
>
> ```console
> 2941
> ```
>
> As you can see there are many, many commits even though, I just did **2** actual commits!

> [!TIP]
> Similar to what we did in '[[Git - Hashes]]'... We can also do the same thing here.
>
> But this time, instead of going to the `.git/objects/` directory, we are going to head over to `.git/refs/heads`
>
> The `heads` folder should contains all our branch's *commit hashes*!

## Deleting Branches

So we have looked at the *creation of branches* in Git; but what about their deletion?

> This is what we are going to learn now... Do you have a bit of patience? Why are you still reading this?

---

### Upstream

> [!INFO] Resources
> - https://stackoverflow.com/a/17122300
> - https://tms-outsource.com/blog/posts/what-is-upstream-in-git/

So their is something that we first need to understand first, before we go ahead an actually **delete** *branches* in our local repository.

This is more related to **remote** repositories but if you go and read the documentation, you are going to see that it says something along the lines of:

```console
The branch must be fully merged in its upstream branch, or in `HEAD`
if no upstream was set with `--track` or `--set-upstream-to`.
```

> This is the reason as to why I feel like I should **learn** this for myself!

> [!TIP] What Is This "*Upstream*"?
> > Definition By TMS
>
> *Upstream* in Git refers to the **remote** branch that your *local branch* **tracks**. It’s typically the branch you pull changes from and push changes to. The term helps manage *collaboration* by defining where updates come from and where your changes should go, usually set with `git push --set-upstream`.

So think of it like some sort of "*man-in-the-middle*" that is linking the information from the **local** repository to the **remote** repository!

Hence, to **delete** a branch in Git, we first need that all the *contents* currently inside that branch has been fully [[Git - Merge | merged]] or *synced* with the **upstream** branch.

---

Now, the command that we need to **delete** a branch from our repository is going to look like this:

```bash
# we are now going to delete the newly created 'the_goat' branch
git branch -d the_goat
```

> [!NOTE] Make Sure That You Are **NOT** Located In It
> > "*That's what she said*"
>
> You **cannot** delete a branch that is you are currently in!
>
> For example, I went into the `the_goat` branch and ran the above command and received this error message:
>
> ```console
> error: cannot delete branch 'the_goat' used by worktree
> at '/home/username/Desktop/learning_git/first_local_repo'
> ```

- Hence, we should see that we get a message that our desired branch was deleted:

```console
Deleted branch the_goat (was aea6060).
```

Now if we go ahead and run a simple `git --no-pager branch -la`, we should see that we have this:

```console
* deeznuts
```

> As you can see we only have **1**, beautifully named, branch!

### Delete "Remote Tracked" Branch On Local

> [!INFO] Resources
> - https://stackoverflow.com/a/23961231

I was "*casually*" reading the Git `branch` help page ( *like one does on a Week-End night* ) and saw this:

```console
git branch (-d|-D) [-r] <branch-name> ...
```

> I wondered to myself, `-r`? Recursive? WTF?

So `-r` actually stands for `--remotes`. For example, running `git branch` will **only** show the **local** branches but we add the `-r` flag like so: `git branch -r` so that we can **only** see all the remote branches...

If I go ahead and run *that* command in our repository, we should see that we get:

```console

```

Well... **Nothing**! This is true as we currently only have a **local** repository setup.

> But what if I try this inside my **remote** repository?

- Find out how many *remote branches* I have in my private repository

```bash
# list out all the remote branches in my private repository
git branch -r
```

- I currently have all of these *remote branches* setup!

```console
  origin/HEAD -> origin/main
  origin/UOM_L1S1
  origin/UOM_L1S2
  origin/UOM_L1_COMPLETE
  origin/UTM-2024
  origin/main
```

Let's say that we want to **delete** the `origin/UOM_L1S2` *remote* branch... Therefore, we are going to have to run the following command:

```bash
# delete the remote branch 'UOM_L1S2' that is found on remote repository
git push origin --delete UOM_L1S2
```

> [!NOTE]
> I am **not** going to run the above command as I need that branch.
>
> But I just ran that *template* command on another repository and it did **delete** the branch from *remote*!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!