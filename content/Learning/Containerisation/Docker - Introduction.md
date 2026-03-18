---
id: Docker - Introduction
aliases: An Introduction to Docker Containerisation System
tags:
  - containerisation
  - docker
author: S.Sunhaloo
date: 2025-11-25
status: Completed
---

## List of Contents

- [[#Virtualisation V/S Containerisation]]
- [[#Installing Docker]]
	- [[#Testing Docker Installation]]

---

> [!INFO] Resource(s)
> - https://www.docker.com/
> - https://docs.docker.com/
> - https://www.youtube.com/watch?v=Ud7Npgi6x8E

# Virtualisation V/S Containerisation 

## Virtualisation

![[Virtual Machine.png | 280]]

## Containerisation

![[Docker Containerisation.png | 280]]

> [!INFO] Difference Between **Virtualisation** and **Containerisation**?
> As compared to the *regular* **virtualisation**; *containers* are much, much **lighter** than *virtual machines*.
>
> We are talking about **seconds** or **milliseconds** in *start time* and **megabytes** instead of gigabytes.
>
> It runs as a "*process*"; whereby a '*process*' can be simply considered as an application like 'Ghostty' or 'Neovim'.
>
> Additionally, for a Virtual Machine to work, we **need** to *allocate* a "**set**" number of resources to it! Well, that's not the case here as again, its simply runs as a **process** whereby it takes whatever amounts it needs to!
>
> > [!WARNING] Long Running and Expensive Process
> > Nevertheless, there might be times whereby you are going to have a process ( *running inside the container* ) that is taking up all the *resources* of your actual **host** computer.
> >
> > Therefore, we can setup **limits** so that it does not take up all our resources!
> >
>
> > Basically think of a *Virtual Machine* as a **reservation at a hotel** whereby you **have** to pay even when you are gone sight seeing. While think of *Containers* as a **taxi** whereby you *pay* when you are actually using it!
>

> [!NOTE]
> One of the "*main*" reasons that they are so efficient its because its based on the Linux Kernel ( *technologies* ) and filesystems.
>
> This is one of the reason that you see commands like `docker -ps` which is basically a copy of the "*original*" `ps` command found on Linux.

# Installing Docker

> [!INFO] Resource(s)
> - https://docs.docker.com/engine/install/

> I am not writing documentation just my learning experience and path here!

- Install the docker **engine**:

```bash
# install the 'docker' package
sudo pacman -S docker
```

> Therefore, this should go ahead and install the docker engine on your Arch / Arch-based systems!

> [!INFO]
> From the [roadmap.sh](https://roadmap.sh/docker) 'Docker' roadmap; I see that for the installation part; it divided it into two.
>
> There it says that the **Docker Engine** ( *only* ) can only be installed in Linux.
>
> For other operating systems like 'Windows' and 'MacOS'; you are going to have to install the 'Docker Desktop' package instead.
>
> > But I think that's bullshit; you should be able to use a package manager like `winget` or home`brew` to be able to install it!
>

- Run the 'Hello World' of docker:

```bash
# run 'hello-world' image
docker run hello-world
```

> [!WARNING] Ohh... A Service!
> Running the above command; I get the following as output:
>
> ```console
> docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
>
> Run 'docker run --help' for more information
> ```
>
> Yes, you are going to have to `systemctl start` docker to be able to use it!

- Start the docker service / daemon:

```bash
# start the docker service
sudo systemctl start docker.service
```

- This is the output that I get after running `sudo systemctl status docker.service`:

```console
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; preset: disabled)
     Active: active (running) since Wed 2025-11-26 09:10:26 +04; 1s ago
 Invocation: 426e24b1d13f489da717d63ac3e0f966
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 4805 (dockerd)
      Tasks: 10
     Memory: 24.6M (peak: 28.1M)
        CPU: 219ms
     CGroup: /system.slice/docker.service
             └─4805 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```

> [!NOTE] Enabling On Boot!
> If you are not a fucking 'ADHD' piece of shit like me; then you can simply *start* docker whenever you **boot** up your computer.
>
> - Run the following command if you want docker to start on boot:
>
> ```bash
> # allow docker to start on boot + start service right away!
> sudo systemctl enable --now docker.service
> ```

> [!TIP] Stop Running `sudo` each time...
> [Claude](https://claude.ai) told me to run the following command:
>
> ```bash
> # add docker to the user group
> sudo usermod -aG docker $USER
> ```
>
> This means that we won't need to run `sudo` each time for some of the docker commands that does require *higher privileges*.
>
> > I am going to run it!
>

## Testing Docker Installation

Hence, run the 'hello-world' image to test if docker is working correctly on our system:

```bash
# run the 'hello-world' image
docker run hello-world
```

- Therefore this is the output that I get:

```console
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete 
Digest: sha256:f7931603f70e13dbd844253370742c4fc4202d290c80442b2e68706d8f33ce26
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

> [!INFO] List out all the images
> - Run the following command to list out all the images on your system:
>
> ```bash
> # list out al the images found on locally
> docker images
> ```
>
> - Therefore this is how the output should look like:
>
> ```console
> REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
> hello-world   latest    1b44b5a3e06a   3 months ago   10.1kB
> ```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!