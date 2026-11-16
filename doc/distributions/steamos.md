# Waywall on Steam Deck

The Valve Steam Deck ships with SteamOS, a custom Arch-based Linux distribution. It ships with a custom [microcompositor](https://wiki.archlinux.org/title/Gamescope) but fortunately Waywall works fine, as the desktop environment is essentially KDE/Wayland. There are a variety of peculiarities to SteamOS that serve to make the device better for the average user, that might get in the way of your speedrunning attempts. For installing Waywall, see the [Waywall Installation page](../minecraft/waywall/waywall.md#Installation) (subheading SteamOS).

# Additional SteamOS Notes

- It is recommended to download a JDK for local use (as opposed to installing a package) as root-installing will quickly fill up the small SteamOS root partition.
    - Generally speaking, it is not recommended to install any package on SteamOS if you can avoid it.
- Due to Minecraft tying input to framerate, it is recommended to set a high max framerate (e.g. 120fps) even if you are running on a lower framerate monitor.
- **To fix issues with input lag:** Ensure you enable fullscreen with Waywall. Disable VSync in Standard Settings. Finally, in Waywall configuration, enable tearing ([current documentation for tearing settings](https://tesselslate.github.io/waywall/01_options_experimental.html)).
