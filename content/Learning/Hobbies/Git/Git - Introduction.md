---
id: Git - Introduction
aliases: An Introduction to Git Version Control System
tags:
  - git
  - GitHub
  - bootdev
  - linux
author: S.Sunhaloo
date: 2025-06-23
status: Completed
---

## List of Contents

- [[#What is Git?]]
- [[#The Setup]]
	- [[#The Setup]]
	- [[#Installing Git]]
- [[#Confusion, Confusion and Confusion!]]

---

# What is Git?

> [!INFO] Resources
> - https://en.wikipedia.org/wiki/Git
> - https://github.com/git/git
> - **Official Git Documentation**: https://git-scm.com/doc
> - **The Man Himself "Doing" It**: https://www.youtube.com/watch?v=rH3zE7VlIMs

Git is what we call a **Distributed Version Control System** ( VCS ) made by the [GOAT](https://www.urbandictionary.com/define.php?term=GOAT), [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds)! It is a program that is used to track **files** ( *and folders* ) and is mostly used by *programmer* to control the **versions** of *Source Code*.

> [!TIP]
> The story goes like this, Linus was pissed at most of the *version control* system like [BitKeeper]() at the time!
>
> Therefore, he took **2 weeks** off and created the core / main components of *Git* in just... **5 Fucking Days**!!!
>
> > [That's why he is the GOAT](https://www.youtube.com/watch?v=lPk_zyRKs1Q)!
>

---

# The Setup

> [!NOTE] Now, Hear Me Out!
> Now, this is **not** my first time using `git` and [GitHub](https://github.com/)!
Back in '09/12/2023', when I started *learning* and using `git` to track my programs and also my [Obsidian](https://obsidian.md) vault.
>
> I do have knowledge to *add*, *commit*, *push* and *pull*. But that's it!
>
> Hence, in this holiday ( *University Level 1 "completion" Holiday* ); instead of learning some "*new*" technology. I want to instead **focus on learning the fundamentals** of the **existing** technology that I already used.
>
> > [!INFO] [Boot.dev](https://boot.dev)
> > I personally **don't** really like these "*Course Type Websites*". But as this is recommended by another '*GOAT*', [ThePrimeagen](https://github.com/ThePrimeagen).
> > Therefore, I wanted to give it a try! Additionally, its not like you a simply watching a video and typing along.
> >
> > > ITs inTeraCtIVe!!!
> >
> > Hence, instead of *fucking around and finding out*. I will have a structure!

> Thank You [Mr Sathan](https://gavinsathan.blogspot.com/) for your inspiration!

## Requirements

- Terminal Emulator
	- [Windows People](https://www.youtube.com/watch?v=bKcgfVCFKZU): [Windows Terminal](https://github.com/microsoft/terminal)
	- Linux People: [Kitty](https://github.com/kovidgoyal/kitty) $\leftarrow$ My Personal Favourite!
- `git`
- [GitHub](https://github.com/Sunhaloo) Account

### Installing Git

The following code block below will show you how to install `git`.

> Just look for you specific Operating System!

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

> [!SUCCESS] Verify Installation of `git`
> To verify if you successfully install the package... You can simply run $\downarrow$:
>
> ```bash
> # check if git has been installed or already installed
> git
> ```
>
> > You should see that you get a long output!
>

> [!TIP] Starship / Oh My Posh
> I also suggest you to install a "*good-looking*" prompt!
>
> Here are the 2 that I used:
>
> - Starship: https://starship.rs/ ( my current one... Rust based )
> - Oh My Posh: https://ohmyposh.dev/
>
> The reason that I say this is it help you see differentiate between, different "*stages*" of `git`!
>
> For example here is my Git Configuration for Starship
>
> ```toml
> # -- Configure Git Status Module --
> [git_status]
> format = "[\\[[$ahead_behind](green)[$modified](dark_yellow)[$conflicted](red)[$renamed](dark_white)[$staged](dark_gray)[$untracked](gray)[$deleted](dark_red)\\]](dark_white)"
> conflicted = ''
> ahead = ''
> behind = ''
> diverged = ''
> # INFO: also known as 'ahead_behind'??!??
> up_to_date = ''
> untracked = ''
> stashed = '󰠔'
> modified = ''
> staged = '󰓍'
> renamed = ''
> deleted = ''
> ```

# Confusion, Confusion and Confusion!

<h2 align="center"> Git is <span style="color: red;"> NOT</span> GitHub!!!</h2>

Yes, most beginners confuse `git` as being GitHub. These are two different things!

> They are [same, same but different](https://www.youtube.com/watch?v=7tTfL-DtpXk)!

> [!INFO] My Shitty Analogy!
> Think of a world where every *Social Media Platform* like [Instagram](https://instagram.com), [YouTube](https://youtube.com), [Twitch](https://twitch.tv), [Reddit](https://reddit.com), and all of the others ( *Fuck TikTok* ) where made using [Rust](https://github.com/rust-lang/rust).
>
> Therefore, we "*can*" say that all need **rust** to be able to exists and keep on updating.
>
> We can say the same thing about [GitHub](https://github.com), [GitLab](https://gitlab.com), [Codeberg](https://codeberg.org/), [SVN](https://en.wikipedia.org/wiki/Apache_Subversion) whereby the all use `git`!
>

> Now, you see how important is `git`!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!