---
id: Arch Linux V2
aliases: The remaking of my Arch Linux setup ( Version 2 )
tags:
  - linux
author: S.Sunhaloo
date: 2025-12-13
status: In-Progress
---

## List of Contents

- [[#First Boot]]
	- [[#Installation Process]]
		- [[#Post Installation]]
- [[#Start of Customisation]]

---

# First Boot

> [!INFO] Resource(s)
> 
> - Denshi Installation Guide: https://www.youtube.com/watch?v=68z11VAYMS8
> - Tony Installation Guide: https://www.youtube.com/watch?v=oeDbo-HRaZo

## Installation Process

> [!TIP] Change the font
> 
> Because I find the original font... Shit! I am going to run the following command which is going to switch us to the 'Terminus' font with a size of '18'.
> 
> ```bash
> # change the font of the live ISO tty
> setfont ter-v18n
> ```
> 
> > [!TIP] Better Yet!
> > 
> > Refer to the following file / note '[[Practical Training - Labsheet 5#SSH Into Live ISO | Practical Training - Labsheet 5]]'
> > 
> > > If you want to `ssh` into the installation from the comfort of you own terminal!

- [ ] Test internet connection by pinging cloudfare's server
- [ ] Find ways to make the installation faster
	- Use `reflector`
	- Refresh all the packages found on the system
	- Find the best mirrors using `refresh-keys` command ( *see partitioning video* )
- [ ] Partition the actual "*drive*" / partition with `cfdisk`
- [ ] Run the `archinstall` script
	- Watch the video about how to use that custom partition
	- Install `pipewire` audio package instead of the other one ( *`alsa`  I think...* )
	- Try searching for and installing the `nvidia` / NVIDIA related packages ( *already* )
- [ ] Reboot the machine!

### Post Installation

- [ ] Change the `PARALLEL_DOWNLOADS` value from 5 to 10
- [ ] Hard refresh, update and upgrade all packages and **restart** the computer
- [ ] Clone ( *my* ) [archible](https://github.com/Sunhaloo/archible) script
	- Install `yay` 'AUR' helper
- [ ] Check 'Z-Shell' ( *github* ) documentation to check for any changes in installation
	- Check if shell script matches; if **so**, only run that function

---

# Start of Customisation

## Neovim Setup

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!