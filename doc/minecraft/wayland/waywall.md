# waywall

- **waywall** is a Wayland compositor created by tesselslate designed to run inside your existing Wayland session. It provides various convenient features for speedrunning, including but not limited to:
  - Window resizing
  - Key remapping
  - Ninjabrain Bot support
  - Mirrors (i.e. magnifiers for eye measuring, F3, etc.) without using OBS
  - Lots of custom functionality.
- If you're using **X11**, please use [resetti](../x11/resetti.html) instead.

## Installation

- To install waywall on Fedora, first install the dependencies with the following terminal command:

```bash
sudo dnf install libspng-devel cmake meson mesa-libEGL-devel luajit-devel libwayland-client libwayland-server libwayland-cursor libxkbcommon-devel xorg-x11-server-Xwayland-devel wayland-protocols-devel wayland-scanner
```

- Then, run the commands on this page of the [waywall documentation](https://tesselslate.github.io/waywall/00_installation.html#compiling).

- On Arch Linux, [you can install waywall through the AUR](https://aur.archlinux.org/packages/waywall-working-git).
- Users on Debian-based distros may have trouble building waywall manually due to certain dependencies being far out of date. If you're having trouble, join the [Linux MCSR Discord server](https://discord.gg/fwZA2VJh7k).

- Run `waywall` in a terminal to check it's installed properly.
- Afterwards, visit the [next page of the documentation](https://tesselslate.github.io/waywall/00_setup.html) to patch GLFW and set up your instance to launch within waywall.

- After this, move to the [next section](waywall_config.html) to install an example config and learn how to customize it to your liking.
