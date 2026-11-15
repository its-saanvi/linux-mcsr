# Waywall on Steam Deck

The Valve Steam Deck ships with SteamOS, a custom Arch-based Linux distribution. It ships with a custom [microcompositor](https://wiki.archlinux.org/title/Gamescope) but fortunately Waywall works fine, as the desktop environment is essentially KDE/Wayland. There are a variety of peculiarities to SteamOS that serve to make the device better for the average user, that might get in the way of your speedrunning attempts.

## General Setup

If you've never used the desktop environment on your steam deck before, you will need to set a superuser password by running `passwd` from the terminal (Konsole).

For the most part, you should follow the usual wayland setup in this guide. It is recommended to download a JDK for local use (to store somewhere in your /home partition) as root-installing will quickly fill up the small SteamOS root partition. Similarly, you will likely want to download a Prism AppImage for actually running Minecraft.

## Waywall Setup

The same goes for installing and setting up Waywall. Building from source is **not recommended** as this will require installing a variety of tools and libraries that you may not even have space for on the root partition. Installing Waywall (through the usual process) is similarly not recommended. Instead, download and untar the latest waywall[version].pkg.tar.zst file [from the Releases page](https://github.com/tesselslate/waywall/releases).

This will give you a nested directory layout containing both the required GLFW shared object library and the waywall executable. Place these wherever you would like (although for the purpose of upgrading Waywall versions, it may be simpler to store the entire folder structure in somewhere like $HOME/mcsr/waywall).

Follow the ordinary Waywall/Linux setup guide for setting up Prism to correctly use this Waywall executable and GLFW library.

After attempting to launch, you may find that some libraries are missing (for example `libspng`). There are multiple ways to fix this. The "easy route" is to install `libspng` by disabling SteamOS readonly mode, which allows commands like `sudo pacman -S libspng`. As this library is small, there is no real downside to doing this.

However, if you would like to avoid modifying the root partition as much as possible (or if larger libraries are required in the future, or in your setup), you can also locally install libraries using e.g. `pacman -S --root $HOME/mcsr/deps/ libspng`. This will create a "root-like" folder structure in `$HOME/mcsr/deps/`. In order for libraries in here to be seen by Waywall, you can add a .conf file in `/etc/ld.so.conf.d`:

```bash
sudoedit /etc/ld.so.conf.d/mcsr.conf
(in editor: add the following) /home/deck/mcsr/deps/usr/lib/ # ensure that this is the correct library path, obviously
sudo ldconfig # required for ld to recognize the updated library locations
```

This will allow you to install arbitrary libraries without requiring space in your root partition.

## Additional Notes

Due to Minecraft tying input to framerate, it is recommended to set a high max framerate (e.g. 120fps) even if you are running on a lower framerate monitor.

**To fix issues with input lag:** Ensure you enable fullscreen with Waywall. Disable VSync in Standard Settings. Finally, in Waywall configuration, enable tearing ([current documentation for tearing settings](https://tesselslate.github.io/waywall/01_options_experimental.html)).
