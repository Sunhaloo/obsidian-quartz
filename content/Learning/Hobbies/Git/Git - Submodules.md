---
id: Git - Submodules
aliases: Adding Git Repositories Inside Of Git Repositories
tags:
  - git
  - GitHub
  - linux
author: S.Sunhaloo
date: 2026-07-14
status: Completed
---

## List of Contents

- [[#Git Submodules]]
- [[#What You Want To Do But Cannot]]
- [[#Using Git Submodules]]
	- [[#Add Git Repository As Submodule]]
- [[#Cloning Project with Submodules]]

---

# Git Submodules

> [!INFO]
> - Git Help: `git help submodule`
> - Atlassian: https://www.atlassian.com/git/tutorials/git-submodule
> - GitHub Gist: https://gist.github.com/gitaarik/8735255

Basically a Git Repository, with its own `.git` folder **inside** another Git Repository.

Well, I am going to speak in my use-case and what I currently know about it.

> Please read further more about it if you want to learn more about the `submodule` command!

While following and learning about making a 3D-model-viewer by [Coding with Sphere](https://www.youtube.com/watch?v=GCnipL4T0Ho). We needed to use [Sokol](https://github.com/floooh/sokol) and [CGLM](https://github.com/recp/cglm).

Therefore, he recommended that we clone the entire `sokol` and `cglm` repository as its a much easier way to get and use them.

Well, this is where the `submodule` commands comes into play! This allows us to *add* these repositories into our own *working* repository and still being able to do our usual versioning.

## What You Want To Do But Cannot

So let's say that we have the current project structure ( *already initialise as local git repository* ):

```console
 .
├──  .git
├── 󰊢 .gitignore
├── 󱧼 build
├──  dependencies
├──  Makefile
└── 󰣞 src
    └──  main.c
```

- Now let's try to add `sokol` for example as a dependency inside our project and inside our `dependencies` folder:

```bash
# add sokol as a dependency to our project
git clone https://github.com/floooh/sokol.git dependencies/sokol
```

- Then, if we try to **commit** out *addition* and *changes*; we get the following error:

```console
warning: adding embedded git repository: dependencies/sokol
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint:
hint: 	git submodule add <url> dependencies/sokol
hint:
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint:
hint: 	git rm --cached dependencies/sokol
hint:
hint: See "git help submodule" for more information.
hint: Disable this message with "git config set advice.addEmbeddedRepo false"
```

> Therefore, as the *hint* says, we need to use `submodule` sub-command!

> [!INFO]
> Just learned that git does provide a `--git-dir` flag but we are not going to talk about that right now.

## Using Git Submodules

> I am just going to be using the above project structure but now add dependencies using `submodule`!

### Add Git Repository As Submodule

- Instead of using the *usual* `clone` command, use the following instead:

```bash
# add sokol as a dependency to our project as a submodule
git submodule add https://github.com/floooh/sokol dependencies/sokol
```

- Check the status of the submodule(s):

```bash
# check the status of submodule present in the repository
git submodule status
```

- This is the output after running the above `submodule status` command:

```console
3743ea681fce95afd7bee41511cbe51480a046e5 dependencies/sokol (gles2-2352-g3743ea6)
```

> [!INFO]
> This is basically the **latest** commit of sokol as of 15th July 2026.
> 
> So the `status` shows the commit hash and the directory where that *submodule* is found!

> [!SUCCESS]
> Then if we go ahead and add everything to the staging area using `git add .`; we should see that we don't have an errors!

## Cloning Project with Submodules

Now, if a project has / have submodule(s) involved... Then our usual `git clone` command would **not** work and that's because it does **not** clone the *dependencies* repositories.

> Hence, we are going to have to use an updated `clone` command!

- Clone repository with the following command:

```bash
# if using simply 'https'
git clone --recurse-submodules https://github.com/username/project.git

# if using simply 'ssh'
git clone --recurse-submodules git@github.com:username/project.git
```

> [!SUCCESS]
> In the case of `sokol` repository acting our tutorial dependency; we should see something like this in our *log*:
> 
> ```console
> Submodule 'dependencies/sokol' (https://github.com/floooh/sokol) registered for path 'dependencies/sokol'
> ```

> [!TIP]
> But what if you already cloned the repository with the usual way ( *i.e without the `--recurse-submodules` flag* )?
> 
> Then you can use the following command to fetch the contents for the submodule(s)!
> 
> ```bash
> # populate the submodule(s) found in the project
> git submodule update --init
> ```
> 
> - Then again, you should see something like this ( *in our case we have sokol* ):
> 
> ```console
> Submodule 'dependencies/sokol' (https://github.com/floooh/sokol) registered for path 'dependencies/sokol'
> ```


---

# Socials

- **GitHub**: https://www.github.com/Sunhaloo
- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo

---

S.Sunhaloo
Thank You!