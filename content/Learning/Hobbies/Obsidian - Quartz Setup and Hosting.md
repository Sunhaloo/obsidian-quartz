---
id: Obsidian - Quartz Setup and Hosting
alias: Hosting Obsidian Notes with Quartz Tool
tags:
  - HTML
  - GitHub
  - react
author: S.Sunhaloo
date: 2026-03-17
status: In-Progress
---

## List of Contents

- [[#Installation and Setup]]
	- [[#Cloning Original Quartz Repository]]
	- [[#Writing Your Content]]
		- [[#Content Folder]]
		- [[#Build Quartz To Preview]]

---

> [!INFO] Resource(s)
> - Quartz Documentation: https://quartz.jzhao.xyz/
> - Preact: https://preactjs.com/

# Installation and Setup

## Cloning Original Quartz Repository

Following the official documentation, it tells us to clone the actual [quartz](https://github.com/jackyzha0/quartz) repository and then basically setup everything from there!

```bash
# clone the 'quartz' git repository and head inside it
git clone https://github.com/jackyzha0/quartz.git && cd quartz

# install all the required note dependencies
npm i

# run the command to very first time setup!!!
# NOTE: running this command give you and interactive prompt
# for the Obsidian link setting; simply leave it to `default`
npx quartz create
```

> [!INFO]
> Quartz is based on Preact which is simply a **lightweight** version of React!
> 
> That is why the commands like `npm i` and others feel kind-of similar its because its literally a stripped down version of React!

## Writing Your Content

Now that you have cloned the repository; you should see that you have a `quartz` directory and therefore inside that quartz directory; you should see something like this:

```console
 quartz
├──  CODE_OF_CONDUCT.md
├──  content
├──  Dockerfile
├──  docs
├──  globals.d.ts
├──  index.d.ts
├──  LICENSE.txt
├──  package-lock.json
├──  package.json
├──  quartz
├──  quartz.config.ts
├──  quartz.layout.ts
├── 󰂺 README.md
└──  tsconfig.json
```

Therefore, what we are currently interested right now is the `content` folder whereby its the *place* that all of our "*notes*" / **markdown** files are going to be stored.

### Content Folder

Head inside the content folder and you should see that we have a lonely `index.md` file!

```console
 .
└──  index.md
```

Think of that `index.md` file as our **root**... This markdown file is going to be our **homepage** and when someone is going to go on the website. It should redirect to that page.

> Hence, let's go ahead and write something inside of it!

- I updated my `index.md` file to this:

```md
---
title: Quartz Homepage
---

# Obsidian Notes

This is the homepage for our Obsidian _markdown_ notes!

> [!SUCCESS]
> This is actually very nice and we have nothing to lose as its **free**!
```

### Build Quartz To Preview

Well, the main thing about this quartz thing is to be able to render our markdown files on the internet right?

> So how do we actually do that?

Well, simply run the following command below to be able to preview your "*website*":

```bash
# preview the website on localhost / your machine
npx quartz build --serve
```

> [!NOTE]
> If you are not a developer or not in the realm of computers. Let me explain the above command in simple terms.
> 
> The above command is going to **fetch** all the *contents* that is found in the actual `content` folder.
> 
> Then, when it see these folders and markdown files; its going to **convert** them into their respective `.html` files.
> 
> > The thing about markdown is that is really similar to [HTML](https://en.wikipedia.org/wiki/HTML)!
> 
> Now, each time you add **new** notes; this means that its going to have to *convert* these new notes into their respective `.html` files ( *for the first time* ).
> 
> This means that it might take a while depending on the number of markdown files that you add!
> 
> > [!WARNING]
> > Additionally, if you are previewing using the above command; you need to let the command **run** else, the ( *local* ) website is just going to "*die*".
> > 
> > Then, when you are finished... You can simply close your terminal like a peasant or press `Ctrl + C` to close the *server*.

> [!SUCCESS]
> Therefore, if you head over to [http://localhost:8080](http://localhost:8080); you should see that the quartz website whereby you are redirected to the `index.md` homepage!

> [!TIP]
> If you head over to the `quartz/public` folder; you should see that the **equivalent** `index.html` files is found there!

### Keep Writing!

> [!INFO]
> Go ahead and take your time to write all the notes or even copy some notes from your **private** obsidian folder / vault.
> 
> Simply add everything that you want people to see and then you can continue this!

> [!BUG]
> We all know the reason that you are making this right?
> 
> > To be bit of a show-off and flex your notes while still being helpful to others!
> 
> Well, there is something that **breaks** the beautiful Obsidian Graph that quartz give us!
> 
> > **Images**!
> 
> Yes, if you are like me and already have a **private** Obsidian vault with *many* notes... Then, if your notes **does** have *images*; the Obsidian graph on the website will kind-of break!
> 
> > [!TIP] Fixing It!
> > 
> > Given that I have a `Media` folder at the root of my Obsidian vault whereby inside that `Media` folder is looks something like this:
> > 
> > ```console
> >  Media
> > ├──  Images
> > ├──  Templates
> > └──  Videos
> > ```
> > 
> > Simply add all your images inside the `content` folder!
> > 
> > Therefore for me, is going to be placing the `Media` folder inside the `quartz/content` folder!

---

# Socials

- **GitHub**: https://www.github.com/Sunhaloo
- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo

---

S.Sunhaloo
Thank You!
