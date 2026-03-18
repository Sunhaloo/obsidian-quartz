---
id: Git - Hashes
aliases: Git Commit Hashes
tags:
  - git
  - GitHub
  - bootdev
  - linux
author: S.Sunhaloo
date: 2025-07-31
status: Completed
---

## List of Contents

- [[#General "Introduction"]]
- [[#How Does SHA-1 Apply To Git]]
- [[#Find Our Commit Hash]]

---

# General "Introduction"

> [!INFO] Resources
> For more information about Hashes, Hash Maps and Hash Tables, please do check out the resources found below:
>
> - https://en.wikipedia.org/wiki/Hash_function
> - https://www.youtube.com/watch?v=y11XNXi9dgs
> - https://www.youtube.com/watch?v=FsfRsGFHuv4
> - https://stackoverflow.com/questions/1736614/what-is-hash-exactly

> Again, I recommend that you go and have a look at the above resources as I don't really understand it very well myself!

I have to tell you something... I have been hiding something from you...

Check this out:

- What I have been writing in '[[Git - Local Repositories]]'

```console
Author: Username <username@email.com>
Date:   Wed Jul 30 17:46:00 2025 +0400

    Initial commit

    This is our very first commit which contains the following files:

    - README.txt
    - joe_mama.txt
    - main.py

    Peace out!
```

- Compared to the full output of `git log`

```console
commit aea6060a504ed9dab225edbe3995553142f4df1e (HEAD -> main)
Author: Username <username@email.com>
Date:   Wed Jul 30 17:46:00 2025 +0400

    Initial commit

    This is our very first commit which contains the following files:

    - README.txt
    - joe_mama.txt
    - main.py

    Peace out!
```

> [!INFO]
> To be honest, I don't really know why I was hiding this!

Now every *commit* will have its own, **unique** *hash*. Git uses **Hash Functions** and if you want to get specific; the [SHA-1](https://en.wikipedia.org/wiki/SHA-1) and optionally [SHA-256](https://en.wikipedia.org/wiki/SHA-2) ( *in some of the newer versions* ) hash function.

Now, if you have downloaded a Linux ISO before... You know that people usually ask for the 'sha256sums'.

For example, for 'sha256sums.txt' for Arch Linux on the '2025-07-01 21:36' was:

```console
0dbac20eddeef67d3b3e9c109a51b77140cf4ee33cc0b408181454f6c41d0a91
0dbac20eddeef67d3b3e9c109a51b77140cf4ee33cc0b408181454f6c41d0a91
bc943f1d3d25d9350a23574b7eacdd8e00badd8f546ce05929d233b404bfd155
bc943f1d3d25d9350a23574b7eacdd8e00badd8f546ce05929d233b404bfd155
```

> You could say that is some sort of fingerprint!

# How Does SHA-1 Apply To Git

Git uses *this* hash function to computer a **unique** hash of *40-characters string*.

These function is applied to:

- Files ( blobs )
- Directories ( trees )
- Commits
- Tags

> Therefore, the *hash* becomes the **ID** of the object!

## Commits

While commit hashes are *derived* from their **content changes**. There are some other *stuff* that also affects the **end** of the hash and they might be:

- Commit Message
- Author's Name and Email
- Date and Time
- Parent ( Previous ) Commit Hashes

### Try It Out!

You can try generating a "*commit hash*" in your terminal like so:

```bash
󰘧 echo "Hello" | git hash-object --stdin
```

This will **always** output this number:

```console
e965047ad7c57865823c7d992b1d046ea66edf78
```

But let's try changing 'Hello' to 'Hello World'... Hence, we get and output like so:

```console
557db03de997c86a4a028e1ebd3a1ceb225be238
```

> [!WARNING] It Should Be Different!
> Even if you do the things like add the same data to a file, same commit messages... The *commit hashes* would still be **different**.

# Find Our Commit Hash

So from **my** `git log`, I can see that my commit message *hash* was:

```console
aea6060a504ed9dab225edbe3995553142f4df1e
```

Let me try to find it inside the `.git` folders!

> Bare with me for a second! If you are on Linux / Mac OS, follow me! Else try to use `Get-ChildItem` and use AI or something to replicate what I am about to do below.

- Remove the first 2 characters from the *commit hash*, therefore, it simply becomes:

> Go ahead and do this for your specific *commit hash*!

```console
a6060a504ed9dab225edbe3995553142f4df1e
```

Now, try to run this command inside the **root** of your repository:

```bash
# find the specific commit hash
find .git/objects/ae -type f -name "a6060a504ed9dab225edbe3995553142f4df1e"
```

The command above will try to find the contents of the `.git/objects/ae` directory and try to find the file that has the **same** name as our *commit hash*.

> [!NOTE]
> This means that you are going that have to remember the first 2 *characters* that you removed from **your** specific *commit hash*.

But as you can see most of these *hashes* ( *if not all of them* ) are stored under the `.git/objects` directory!

## Content of Commit Hash

Go ahead and `cat` out the contents for your specific *commit hash*.

```bash
# output the contents of my commit has with 'cat'
cat .git/objects/ae/a6060a504ed9dab225edbe3995553142f4df1e
```

In my case, the contents for the above *commit hash* is as follows:

```console
xK,Q0d()JMUHN4M2L5H1M2L02O50NK53423IL2KKI40H2H16MJ,-/.HWIML345400vHMKS04750643P6010XYJf.ϼ̒)\\!

E
eE
iE%Pi
     bTt̜b+..] WG_W.]D(7713O+ 519U!D
                                   > az%
```

> [!INFO] Pretty Much Unreadable!
> This is because the *contents* has been compressed to **raw bytes**!
>
> Now, let's try to use another program that will output the contents of the file in **HEX** format!
>
> > [!NOTE]
> > You might **not** have this program / command available on your system. At least, I did **not** have it!
> >
> > This program is called [`xxd`](https://linux.die.net/man/1/xxd)! Now there are no packages called `xxd`... But when I search using pacman for `xxd` like so:
> >
> > ```bash
> > sudo pacman -Ss xxd
> > ```
> >
> > I get the following output ( *this is not the full output but you get the idea* )!
> >
> > ```console
> > extra/gvim 9.1.1552-1
> > extra/tinyxxd 1.3.7-1
> > extra/vim 9.1.1552-1 [installed]
> > ```
> >
> > Well to install `xxd`, you are going to have to install [VIM]()!
> >
> > > Again, cementing that VIM is the greatest editor of all time!
> >
>

Let's us now go ahead and do the *same* thing but this time using `xxd`!

```bash
# output the contents of my commit has with 'xxd'
xxd .git/objects/ae/a6060a504ed9dab225edbe3995553142f4df1e
```

Hence, in this case, we do get some "*meaningful*" output:

```console
00000000: 7801 4bce cfcd cd2c 5130 b2b4 6428 294a  x.K....,Q0..d()J
00000010: 4d55 484e 344d 32b0 4c35 4831 4d32 4cb6  MUHN4M2.L5H1M2L.
00000020: 3032 4f35 304e 4b35 3334 3233 494c 324b  02O50NK53423IL2K
00000030: 4b49 3430 4832 4831 364d e34a 2c2d c9c8  KI40H2H16M.J,-..
00000040: 2f52 082e cdcb 48cc c9cf 57b0 49ac ca4d  /R....H...W.I..M
00000050: 4ccc 3334 3534 3030 7648 cf4d cccc d14b  L.345400vH.M...K
00000060: cecf b553 3034 3735 b6b0 3036 3433 50d0  ...S0475..0643P.
00000070: 3630 3130 e082 5859 924a 9666 2ecf bccc  6010..XY.J.f....
00000080: 92cc c41c 0588 295c 5c21 1999 c50a 99c5  ......)\\!......
00000090: 0af9 a545 0a65 a945 950a 6999 45c5 2550  ...E.e.E..i.E.%P
000000a0: 6985 f28c cce4 0c85 e4fc bc92 c4cc bc62  i..............b
000000b0: 8592 8c54 85b4 fc9c 9cfc f2cc bc74 85b4  ...T.........t..
000000c0: cc9c d462 2b2e 2e5d 8520 5747 175f 57bd  ...b+..]. WG._W.
000000d0: 928a 122e 5d85 acfc d4f8 dcc4 dc44 2837  ....]........D(7
000000e0: 3731 334f afa0 928b 2b20 3531 3955 21bf  713O....+ 519U!.
000000f0: b444 910b 003e ce61 7a                   .D...> .az
```

# Git Cat-File

So instead of fiddling around the `.git/` directory... `git` provides the `cat-file` command whereby we can use *that* command to *view* the **contents** of our last commit...

> [!INFO]
> The `cat-file` command is part of the "**[[Git - Getting Started#Git Commands | plumbing]]**" commands.
>
> This means that you usually don't really use them that often...

> Now, my question is why would someone do use that while we have `git log`? Nevertheless...

```bash
# view contents of a specific commit
git cat-file -p aea6060a504ed9dab225edbe3995553142f4df1e
```

In my case, I get the following output:

```console
tree ca5b09e0d5b1c827e03fe61264ab6fda00b0d35f
author Username <username@email.com> 1753883160 +0400
committer Username <username@email.com> 1753883160 +0400

Initial commit

This is our very first commit which contains the following files:

- README.txt
- joe_mama.txt
- main.py

Peace out!
```

> [!INFO]
> The `-p` *flag* just "**prettify**" the output!
>
> > What is "*beautiful*" anyways? An [RX-7 FD](https://www.youtube.com/watch?v=pzrAZeu1hr4) Obviously!!!
>

## Get Content Of File From Hash

> Again, why would someone do that? When you have things like `cat` and `ls` and `checkout` ( *don't worry mate...* ).

We are now going to try to get the contents of `README.md`.

- First we are going to `cat-file` our *commit hash*

```bash
# get the output of our main commit "message" hash
git cat-file -p aea6060a504ed9dab225edbe3995553142f4df1e
```

```console
tree ca5b09e0d5b1c827e03fe61264ab6fda00b0d35f
author Username <username@email.com> 1753883160 +0400
committer Username <username@email.com> 1753883160 +0400

Initial commit

This is our very first commit which contains the following files:

- README.txt
- joe_mama.txt
- main.py

Peace out!
```

- `cat-file` the *commit hash* for the work **git tree**

```bash
# get the output of the git tree's hash for that commit hash
git cat-file -p ca5b09e0d5b1c827e03fe61264ab6fda00b0d35f
```

```console
100644 blob a6bdfb839192eeb2a841b7e76ed3541cc164deef    README.md
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    joe_mama.txt
100644 blob 491f8ff66c653abd81614b8ac20c2b422d1e7586    main.py
```

- As we want to get the contents of our `README.md` file... We are going take its **blob** *hash*

```bash
# get the actual contents found inside 'README.md'
git cat-file -p a6bdfb839192eeb2a841b7e76ed3541cc164deef
```

Therefore, the final output should look like so:

```console
# First Local Repository

This is my NOT my first local repository!!!
```

> [!TIP]
> Just `cat` out the file for fuck sake!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!