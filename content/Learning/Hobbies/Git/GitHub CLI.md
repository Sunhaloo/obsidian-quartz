---
id: GitHub CLI
aliases: Create and Manage GitHub Repositories In Terminal
tags:
  - git
  - GitHub
  - linux
author: S.Sunhaloo
date: 2025-08-03
status: HOLD
---

## List of Contents

- [[#GitHub In Terminal]]
	- [[#Installing GitHub CLI]]
- [[#Setting Up GitHub CLI]]
- [[#GitHub CLI Commands]]
	- [[#Create New Repository]]
	- [[#Delete Repository]]

---

> [!INFO] Resources
> - https://cli.github.com/manual/ $\Rightarrow$ Official Documentation / Manual

# GitHub In Terminal

So the first time that I came across this tool was when [Sylvan Franklin](https://www.youtube.com/@sylvanfranklin) was making a [Neovim Plugin](https://github.com/search?q=Neovim%20Plugins&type=repositories) whereby he used it to create his [pear](https://github.com/SylvanFranklin/pear) repository.

> Here is a link to the video: https://www.youtube.com/watch?v=MhlDm8WGbhM&t=341s

I think that this is so fucking cool and I wanted to learn it '*ASAP*' ( *as "slow" as possible* )!.

## Installing GitHub CLI

See the following code block below on how to install `gh`:

```console
# windows users
winget install GitHub.cli 

# again macos users - see homebrew package manager or xcode-select
# sorry not sorry

# debian - see documentation
# man you guys really need to switch to rolling release or use 'unstable'
# https://github.com/cli/cli/blob/trunk/docs/install_linux.md
# fuck... even termux have it! you guys really need to step up

# I use Arch BTW
sudo pacman -S github-cli

# fedora - also see the link above
```

> [!SUCCESS] Verify Installation of `gh`
> To verify if you successfully install the package... You can simply run $\downarrow$:
>
> ```bash
> # check if github-cli has been installed or already installed
> gh --version
> ```

---

# Setting Up GitHub CLI

## Authentication - Login

So because this is actually related to [GitHub](https://github.com/); we are going need to **login**!

- Run the following command to be able to login:

```bash
# authenticate and login to github-cli
gh auth login
```

> This should go ahead and run the **interactive** setup!

These are the following setting / options that I chose!

- Where do you use GitHub? **GitHub.com**
- What is your preferred protocol for Git operations on this host? **SSH**
- Upload your SSH public key to your GitHub account? *The default public GitHub SSH key*
- Title for your SSH key: **[Stop It... Get Some Help](https://www.youtube.com/watch?v=abXakjfuuRQ)**

- This this what message that I get after logging in:

```console
✓ Authentication complete.
- gh config set -h github.com git_protocol ssh
✓ Configured git protocol
✓ SSH key already existed on your GitHub account: /home/username/.ssh/id_ed25519.pub
✓ Logged in as Username
```

---

# GitHub CLI Commands

## Create New Repository

> [!INFO] Resource(s)
> - https://cli.github.com/manual/gh_repo_create

Let's go an create a little, **empty** GitHub repository called `test`

Now there are "*ways*" that we can do this running the command below will give you the **interactive** version!

```bash
# interactive version
gh repo create
```

> [!NOTE]
> I am going to try the interactive version first and then tell you want options / settings that I chose!

These are the following options that I chose:

- What would you like to do? **Create new repository on github.com from scratch**
- Repository name: **test**
- Description: **This is a testing repository made using github-cli**
- Visibility: **Public**
- Would you like to add a README file? **y**
- Would you like to add a .gitignore file? **N**
- Would you like to add a license? **N**
- This will create "test" as a public repository on github.com. Continue? **Y**
- Clone the new repository locally? **Yes**!!! *Why fucking not*!

### Create GitHub Repository ( Non-Interactive Way )

Instead of creating GitHub repository the "*interactive*" way... I am going to attempt to **create** a public repository called `testing`.

```bash
# create the 'testing' repository
# with the same settings as above
gh repo create "testing" --description "This is another testing repo" --public --add-readme --clone
```

> Let me try to run this shit!

> [!SUCCESS]
> This is what I got after running the above command!
>
> ```console
> ✓ Created repository Username/testing on github.com
>  https://github.com/Username/testing
> Cloning into 'testing'...
> ```

## Delete Repository

> [!INFO] Resource(s)
> - https://cli.github.com/manual/gh_repo_delete

So I am now going to try to learn how to **delete**, like "*nuke*" the repository that I just created.

### Deletion of `test` Repository

- Run the following command to **delete** our little `test` repository:

```bash
# delete our GitHub repository
gh repo delete test
```

> [!BUG] Oh Fuck!
> So this is error that I got after running the following command:
>
> ```console
> ? Type Username/test to confirm deletion: Username/test
> HTTP 403: Must have admin rights to Repository. (https://api.github.com/repos/Sunhaloo/test)
> This API operation needs the "delete_repo" scope.
> To request it, run:  gh auth refresh -h github.com -s delete_repo
> ```
>
> > [!INFO]
> > So the above `repo delete` command that we just ran is also **interative**!
>
> So as you can see to fix it, it tell us to run the following command:
>
> ```bash
> gh auth refresh -h github.com -s delete_repo
> ```
>
> > [!NOTE]
> > If I would have **read** the *fucking* manual! I would have seen it!

Therefore, running the same `gh repo delete test` "*interactive*" command again, we should see that is going to be successful!

> [!SUCCESS]
> Well, we succeeded in "*nuking*" the `test` directory!
>
> ```bash
> ? Type Username/test to confirm deletion: Username/test
> ✓ Deleted repository Username/test
> ```

### Deletion of `testing` Repository

Now, we are going to also **delete** the `testing` repository but this time **without** any *confirmation*!

> This means that we will **not** need to type `Username/repo_name`

```bash
# delete 'testing' repository without any confirmation
gh repo delete testing --yes
```

> [!SUCCESS]
> Well, well, well!
>
> ```bash
> ✓ Deleted repository Username/testing
> ```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!