# waywall

- **waywall** is a Wayland compositor designed to run inside your existing Wayland session. It provides various convenient features for speedrunning, including but not limited to:
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
- Users on Debian-based distros may have trouble building waywall manually due to certain dependencies being far out of date. If you're having trouble, join the [Linux MCSR Discord server](https://discord.gg/3tm4UpUQ8t).

- Run `waywall` in a terminal to check it's installed properly.
  - Use the absolute path to the waywall executable if this doesn't work (i.e. if you built waywall in `/home/username/waywall/build/waywall`, run `/home/username/waywall/build/waywall/waywall`).
  - The wrapper command for your instance in the next step should also use this path instead of `waywall`.
- Afterwards, visit the [next page of the documentation](https://tesselslate.github.io/waywall/00_setup.html) to patch GLFW and set up your instance to launch within waywall.

- After this, move to the [next section](waywall_config.html) to install an example config and learn how to customize it to your liking.

## Troubleshooting

- On dual-GPU setups (i.e. laptops with integrated and dedicated graphics), waywall may not display mirrors correctly, specifically if the desired GPU is an NVIDIA one.
  - To fix this:
    - Fedora users should check `akmod-nvidia` is installed.
    - Arch users should check `nvidia-prime` is installed.
  - Then, modify your wrapper command in your instance's settings in Prism like so:

    ```bash
    sh -c "waywall wrap -- prime-run $INST_JAVA \"$@\""
    ```

  - Remember to replace `waywall` with the absolute path if you must.
