# Introduction

This section explains why using Linux for Minecraft speedrunning is ideal, choosing a Linux distro and desktop environment, and creating bootable media.
If you're already using Linux, skip ahead to the [post-installation](post_install/post-install.html) section.

## Why Linux?

If you're not already using Linux, you’re probably asking - why would you use Linux for speedrunning, or for anything at all?

- Minecraft runs excellently on Linux, even better than on Windows.
- On Windows, it's recommended to play in fullscreen to avoid input lag. This makes window resizing scripts slow and distracting, and makes other windows such as Ninjabrain Bot invisible unless you turn off fullscreen/resize the game. On Linux, however, you can use windowed or borderless windowed without any input lag, so you have the best of both worlds.
- Resize macros, magnifiers/projectors, keyboard layouts for search crafting, rebinding and the like are very clean when using [waywall](minecraft/wayland/waywall.html).

While this sounds nice, you should have more of a reason other than speedrunning to make the switch.
- Outside of Minecraft, Windows is quickly turning into a less favourable option for more and more things, with Windows 11 being bloated with unnecessary AI features and more invasive data collection, and is becoming more and more unstable as time goes on [¹](https://x.com/WindowsLatest/status/1979635547921646058) [²](https://www.youtube.com/watch?v=mlY2QjP_-9s).
- Linux, with more support from developers and with things like Proton, is catching up to Windows for gamers, creatives, developers, and your average computer user.
- If there’s something you still need Windows for though (notably Valorant/Fortnite/Adobe software), don’t worry - this guide will also go over dual-booting, so you can use both Windows and Linux interchangeably.

## Distributions & Desktop Environments

- Linux, being a **free and open source operating system**, comes in several different flavours a.k.a distributions a.k.a distros.
- Some of the popular distributions are **Ubuntu**, **Fedora**, **Arch Linux(btw)**, etc.
- For MCSR, we recommend a distribution based on **RHEL** called **Fedora**, which balances stability with frequent updates.
- The next choice you should make is what **desktop environment** or **DE** to use - this includes the general visuals, window behaviour and management, pre-installed apps, things like that.
- The Fedora team provides [many versions](https://fedoraproject.org/spins/), or “spins”, with different DEs pre-installed. Some spins just provide a standalone **window manager** without many pre-installed apps or much of anything, for a clean, efficient albeit less beginner-friendly experience.
- We will first attempt to use a **Wayland-based** DE (a.k.a. a Wayland **compositor**), which are newer but sometimes less stable than DEs using the older **X11** backend, especially for NVIDIA users.
- The great thing about Linux is that you can use whichever DE or spin that you want, swap between them easily, and customize your setup endlessly. Speedrunning works just fine on most popular DEs.
- This guide will use the official **KDE Plasma** version of Fedora. The Plasma DE will feel very familiar if you’re coming from Windows, and tends to work well for NVIDIA users when using Wayland.
- Go [here](https://fedoraproject.org/kde/download) and download the latest Live ISO for Fedora KDE Plasma, under **For Intel and AMD x86_64 systems**.
- You can learn more about **Linux Distributions** [here](https://en.wikipedia.org/wiki/Linux_distribution).

## Creating Fedora installation media

- After downloading the ISO from the official Fedora Project website, pick up a USB stick of at least 5GB space or above.
- **NOTE: The USB stick will be formatted during the install process and all data on it will be erased.**
- To install the ISO into the USB stick, use **Balena Etcher** from [here](https://www.balena.io/etcher#download-etcher).
- Plug in the USB stick to your PC and open Balena Etcher. **Back up any data before proceeding.**
- Under **Select Image**, locate wherever you downloaded the Fedora ISO from before and select it.
- Under **Select Drive**, select the USB device name. It should be auto-selected for you, just make sure its the right USB.
- Then click **Flash** to start creating your Bootable USB!
- Wait for it to finish **Flashing** and **Verifying** as well. Don't quit Balena until all of it is done.
- Congratulations! You've just created a bootable Fedora USB. If you don't plan on dual-booting Windows and Linux, move to the [live environment](live-env.html) section to install Fedora, otherwise keep reading.

## Dual-booting

- Before rebooting your computer and beginning to install Fedora, you should make space on your hard drive for Fedora to install to.
- Press Windows+R, and type `diskmgmt.msc`. Here, you should see all of your disks - ideally you have a separate disk to install Fedora to, but usually we install it alongside Windows on the `C:/` disk.
- If using the `C:/` disk, right click the main (largest) partition on the disk and select **Shrink Volume**.
- If you can spare around **50 GB** (around 50000 MB) for Fedora, then do so. If you're sure you have the free space on the disk but it isn't letting you shrink it enough, consider using a third-party app like [MiniDisk Partition Wizard](https://www.partitionwizard.com/free-partition-manager.html) to shrink the volume instead.
- You can shrink the volume further after installing Fedora if you need more space - for now, shrink it as much as possible, then move to the [live environment](live-env.html) section to finally install Fedora.
