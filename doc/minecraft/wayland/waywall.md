# waywall

- **waywall** is a Wayland compositor designed to run inside your existing Wayland session. It provides various convenient features for speedrunning, including but not limited to:
  - Window resizing
  - Key remapping
  - Ninjabrain Bot support
  - Mirrors (i.e. magnifiers for eye measuring, F3, etc.) without using OBS
  - Lots of custom functionality.
- If you're using **X11**, please use [resetti](../x11/resetti.html) instead.

# Installation

- There are a few ways to install waywall.
  - [Lingle](https://github.com/Flammable-Bunny/Lingle/releases), a Java application, can build and install waywall and the patched GLFW required to run it on most popular distros. It can also edit your Prism Launcher instance to run waywall and use the patched GLFW.
  - On Arch Linux, [you can install waywall through the AUR](https://aur.archlinux.org/packages/waywall-working-git) - note that Minecraft must run with a patched GLFW and your Prism instance must be configured as instructed in the [waywall documentation](https://tesselslate.github.io/waywall/00_setup.html).
  - [You can build waywall and the patched GLFW manually.](https://tesselslate.github.io/waywall/00_installation.html)
    - On Fedora, install the dependencies with the following terminal command, then follow the steps in the above link:

```bash
dnf install -y libspng-devel cmake meson mesa-libEGL-devel luajit-devel libwayland-client libwayland-server libwayland-cursor libxkbcommon-devel xorg-x11-server-Xwayland-devel wayland-protocols-devel wayland-scanner
```

    - Users on Debian-based distros may have trouble building waywall manually due to certain dependencies being far out of date. If you're having trouble, join the [Linux MCSR Discord server](https://discord.gg/fwZA2VJh7k).

- After installing waywall and editing your instance to run it with the patched GLFW, move to the [next section](waywall_config.html) to install an example config and learn how to customize it to your liking.
