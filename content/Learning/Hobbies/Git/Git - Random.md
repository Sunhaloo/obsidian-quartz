---
id: Git - Random
aliases: Things That I Done In Git
tags:
  - git
  - GitHub
  - linux
author: S.Sunhaloo
date: 2025-09-25
status: HOLD
---

## List of Contents

- [[#Go Back To Previous Commit, Make Changes And Push]]

---

# Go Back To Previous Commit, Make Changes And Push

Given that I am currently working on the a commit in my 'University' repository's `main` branch.

Initially, I made some changes and pushed these changes to **remote**.

The commit that I made the **actual** change was:

```console
commit ba2cdaa74fc6cd63cbc47ca0506c268d8f217cd7
Author: Sunhaloo <username@gmail.com>
Date:   Thu Sep 25 13:56:53 2025 +0400

    Update: Going to test why we need to update to new path in `INSTALLED_APPS` list
```

> This is what I was trying to do: '[[Django Docs - Database Setup#But First I Want To Test Somethings]]'

Therefore, I just experimented my with my shit and I did also committed the following "*experiment*". Therefore my latest commit was:

```console
commit ef0d3f8d91e96359a03215ca327da651a2a576aa (HEAD -> main, origin/main, origin/HEAD)
Author: Sunhaloo <username@gmail.com>
Date:   Thu Sep 25 14:56:09 2025 +0400

    Update: This was the testing part... Going back to previous commit
```

> Now I want to go back to `ba2cdaa74fc6cd63cbc47ca0506c268d8f217cd7`!

I want to go back and continue there and make my changes there and when I push I want the changes for that commit be the the **latest** commit.

> This is with the help of [ChatGPT](https://chat.openai.com)

We can go to different **branches** using the `git switch` ( *or older deprecated `git checkout`* ) command... But we can also move to different **commits**!

```bash
git switch ba2cdaa74fc6cd63cbc47ca0506c268d8f217cd7
```

- But I get this as output:

```console
fatal: a branch is expected, got commit 'ba2cdaa74fc6cd63cbc47ca0506c268d8f217cd7'
hint: If you want to detach HEAD at the commit, try again with the --detach option.
```

---

- But using `checkout` ( *more dangerous* ):

```bash
git checkout ba2cdaa74fc6cd63cbc47ca0506c268d8f217cd7
```

- This is the output but we do move to that commit:

```console
Note: switching to 'ba2cdaa74fc6cd63cbc47ca0506c268d8f217cd7'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at ba2cdaa Update: Going to test why we need to update to new path in `INSTALLED_APPS` list
```

- Output of `git log --oneline --graph --all`:

```console
* ef0d3f8 (origin/main, origin/HEAD, main) Update: This was the testing part... Going back to previous commit
* ba2cdaa (HEAD) Update: Going to test why we need to update to new path in `INSTALLED_APPS` list
```

> [!BUG] But I Am NOT Going To Use `checkout`!
> So returning with `git switch main`...
>
> ```console
> Previous HEAD position was ba2cdaa Update: Going to test why we need to update to new path in `INSTALLED_APPS` list
> Switched to branch 'main'
> Your branch is up to date with 'origin/main'.
> ```

---

- Therefore, **detach** from the head to the *previous* commit

```bash
# actual detach the head to go to previous commit
git switch --detach ba2cdaa74fc6cd63cbc47ca0506c268d8f217cd7
```

- This is the output that I get and also output of `git --no-pager log --oneline --graph --all -2`

```console
HEAD is now at ba2cdaa Update: Going to test why we need to update to new path in `INSTALLED_APPS` list
```

```console
* ef0d3f8 (origin/main, origin/HEAD, main) Update: This was the testing part... Going back to previous commit
* ba2cdaa (HEAD) Update: Going to test why we need to update to new path in `INSTALLED_APPS` list
```

- Now I am going to make my changes, please see '[[Django Docs - Database Setup#Make The Migrations]]'

> Finished making the changes... Going to `add` and `commit`!

- After `add` and `commit` return the the `main` branch / *remote latest commit*:

```bash
# return to the latest commit
git switch main
```

- This outputs:

```console
Warning: you are leaving 1 commit behind, not connected to
any of your branches:

  1d4a8c6 Update: This is now going to be the latest commit

If you want to keep it by creating a new branch, this may be a good time
to do so with:

 git branch <new-branch-name> 1d4a8c6

Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

> [!WARNING] But We Don't Want To Create A New Branch ( *in this case* )!
> But should I?
>
> I think I should take its advice and create a that new branch

- Okay creation of **new branch**:

```bash
# create the new branch
git branch previous-temp-commit 1d4a8c6
```

- Running a little `git branch` I get this:

```console
  L1S1-09/09/25
  UTM-2024
* main
  previous-temp-commit
```

- Now we simply have to **merge**:

> [[Git - Merge]]

As we are going to take the contents **from** *that* branch to `main`... We need to **switch** to `main`.

> Which we already have!

- Therefore I am simply going to **merge** it with `main`!

```bash
# merge the new branch with `main` branch
git merge previous-temp-commit
```

- This is the output that I get:

```console
CONFLICT (add/add): Merge conflict in Current-Learning/DjangoLearning/FirstApp/migrations/0001_initial.py
warning: Cannot merge binary files: Current-Learning/DjangoLearning/db.sqlite3 (HEAD vs. previous-temp-commit)
Auto-merging Current-Learning/DjangoLearning/db.sqlite3
CONFLICT (content): Merge conflict in Current-Learning/DjangoLearning/db.sqlite3
Automatic merge failed; fix conflicts and then commit the result.
```

> Ahh A Merge Conflict - See [[Git - Merge#Comparing Latest Commits]]

- Running `git status`:

```console
On branch main
Your branch is up to date with 'origin/main'.

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file> ..." to mark resolution)
        both added:      FirstApp/migrations/0001_initial.py
        both modified:   db.sqlite3

no changes added to commit (use "git add" and/or "git commit -a")
```

- I am now going to open the `FirstApp/migrations/0001_initial.py` and going to remove all the contents from 'HEAD'!

- Now I am going to keep only the binary file from the `previous-temp-commit`:

```bash
# keep only the proper binary file
git restore --source=MERGE_HEAD --staged --worktree Current-Learning/DjangoLearning/db.sqlite3
```

> [!WARNING]
> Just copy and pasted this from ChatGPT!

> [!NOTE]
> We could have also done that for `0001_initial.py`!

- Now running `git status` we have the following:

```console
On branch main
Your branch is up to date with 'origin/main'.

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   FirstApp/migrations/0001_initial.py
        modified:   db.sqlite3
```

- **We are still in process of `merge`**... Therefore we can commit the merge:

```bash
# commit the merge --> message I will leave default
git commit
```

- Finally we can `git push`!

- This is what my graph using `git log --oneline --graph --all` looks like for **our** part:

```console
On branch main
Your branch is up to date with 'origin/main'.
*   2208362 (HEAD -> main, origin/main, origin/HEAD) Merge branch 'previous-temp-commit'
|\
| * 1d4a8c6 (previous-temp-commit) Update: This is now going to be the latest commit
* | ef0d3f8 Update: This was the testing part... Going back to previous commit
|/
* ba2cdaa Update: Going to test why we need to update to new path in `INSTALLED_APPS` list
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!