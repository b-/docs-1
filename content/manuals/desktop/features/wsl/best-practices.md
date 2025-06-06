---
title: Best practices
description: Best practices for using Docker Desktop with WSL 2
keywords: wsl, docker desktop, best practices
tags: [Best practices]
aliases:
- /desktop/wsl/best-practices/
---

- Always use the latest version of WSL. At a minimum you must use WSL version 2.1.5, otherwise Docker Desktop may not work as expected. Testing, development, and documentation is based on the newest kernel versions. Older versions of WSL can cause:
    - Docker Desktop to hang periodically or when upgrading
    - Deployment via SCCM to fail
    - The `vmmem.exe` to consume all memory 
    - Network filter policies to be applied globally, not to specific objects
    - GPU failures with containers

- To get the best out of the file system performance when bind-mounting files, it's recommended that you store source code and other data that is bind-mounted into Linux containers. For instance, use `docker run -v <host-path>:<container-path>` in the Linux file system, rather than the Windows file system. You can also refer to the [recommendation](https://learn.microsoft.com/en-us/windows/wsl/compare-versions) from Microsoft.
    - Linux containers only receive file change events, “inotify events”, if the original files are stored in the Linux filesystem. For example, some web development workflows rely on inotify events for automatic reloading when files have changed.
    - Performance is much higher when files are bind-mounted from the Linux filesystem, rather than remoted from the Windows host. Therefore avoid `docker run -v /mnt/c/users:/users,` where `/mnt/c` is mounted from Windows.
    - Instead, from a Linux shell use a command like `docker run -v ~/my-project:/sources <my-image>` where `~` is expanded by the Linux shell to `$HOME`.

- If you have concerns about the size of the `docker-desktop-data` distribution, take a look at the [WSL tooling built into Windows](https://learn.microsoft.com/en-us/windows/wsl/disk-space). 
    - Installations of Docker Desktop version 4.30 and later no longer rely on the `docker-desktop-data` distribution; instead Docker Desktop creates and manages its own virtual hard disk (VHDX) for storage. (note, however, that Docker Desktop keeps using the `docker-desktop-data` distribution if it was already created by an earlier version of the software).
    - Starting from version 4.34 and later, Docker Desktop automatically manages the size of the managed VHDX and returns unused space to the operating system.

- If you have concerns about CPU or memory usage, you can configure limits on the memory, CPU, and swap size allocated to the [WSL 2 utility VM](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#global-configuration-options-with-wslconfig).
