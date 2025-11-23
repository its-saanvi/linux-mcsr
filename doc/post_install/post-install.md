# Post Install

The following chapters will go through the first things you should do after installing Linux.

## Basic Terminal usage

- The primary method of downloading and installing software on Linux is using the **package manager** in the terminal. In Plasma, you can open a terminal window with `Ctrl+Alt+T`, or open the start menu and search for **Konsole**.
- The terminal command for installing most things is `sudo dnf install`, followed by a list of apps or things you want to install.
- To update your system, and anything else you’ve installed with dnf, simply run `sudo dnf update`.
  - **Run this now** to ensure everything is up to date. It's a good idea to update things somewhat frequently.
- You can use `sudo dnf search` to check if something you want to install can be installed with dnf.
- There are a couple other useful things dnf can do to help you with installing things, which you will learn to use with time. Generally, running something with the `--help` option tells you how to use it properly (i.e. `sudo dnf --help`).
- The rest of this guide will be followable without much further terminal knowledge, but if you want to learn more about the terminal, check out the [terminal](terminal.html) page.

## Software Manager

- The **Discover** app in Plasma is like an app store - it's a simple place for you to search and install packages and apps.
- Plasma will let you know when it finds any updates for apps you've installed through Discover.

After updating your system with `dnf`, NVIDIA users should [install the proper graphics drivers](nvidia.html). Drivers for other GPUs are pre-installed - if you aren't using an NVIDIA graphics card, jump ahead to [downloading and installing Java](java.html).
