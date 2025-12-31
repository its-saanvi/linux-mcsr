# waywall

- **waywall** is a Wayland compositor designed to run inside your existing Wayland session. It provides various convenient features for speedrunning, including but not limited to:
  - Window resizing
  - Key remapping
  - Ninjabrain Bot support
  - Mirrors (i.e. magnifiers for eye measuring, F3, etc.) without using OBS
  - Lots of custom functionality.
- If you're using **X11**, please use [resetti](../x11/resetti.html) instead.

## Installation From Prebuilt Binaries

- To install waywall on Fedora:
 - Install the latest .rpm from the [waywall github](https://github.com/tesselslate/waywall/tags).
 - After installing the .rpm, you should be able to open it through your file manager, where you will then have an option to install it

- To Install waywall on Debian
 - Install the latest .deb from the [waywall github](https://github.com/tesselslate/waywall/tags).
 - After installing the .deb, you should be able to open it through your file manager, where you will then have an option to install it
  
- On Arch Linux, [you can install waywall through the AUR](https://aur.archlinux.org/packages/waywall-working-git).
 - You may also download the latest .tar.zst from the [waywall github](https://github.com/tesselslate/waywall/tags).

## Installation From Source

- To install waywall on Fedora:
  - First install the dependencies with the following terminal command:

    ```bash
    sudo dnf install libspng-devel cmake meson mesa-libEGL-devel luajit-devel libwayland-client libwayland-server libwayland-cursor libxkbcommon-devel xorg-x11-server-Xwayland-devel wayland-protocols-devel wayland-scanner wayland-devel libXcursor-devel libXi-devel libXinerama-devel libXrandr-devel
    ```

  - Then, run the commands on [this page of the waywall documentation](https://tesselslate.github.io/waywall/00_installation.html#compiling) to compile waywall from source.

- On Arch Linux, [you can install waywall through the AUR](https://aur.archlinux.org/packages/waywall-working-git).
- Users on Debian-based distros may have trouble building waywall manually due to certain dependencies being far out of date. If you're having trouble, join the [Linux MCSR Discord server](https://discord.gg/3tm4UpUQ8t).

- Run `waywall` in a terminal to check it's installed properly.
  - Use the absolute path to the waywall executable if this doesn't work (i.e. if you built waywall in `/home/username/waywall/build/waywall`, run `/home/username/waywall/build/waywall/waywall`).
  - The wrapper command for your instance in the next step should also use this path instead of `waywall`.
- Once waywall is installed properly, visit the [next page of the documentation](https://tesselslate.github.io/waywall/00_setup.html) to patch GLFW and set up your instance to launch within waywall.

- After this, move to the [next section](waywall-config.html) to install an example config and learn how to customize it to your liking.

## Troubleshooting

- On dual-GPU setups (i.e. laptops with integrated and dedicated graphics), waywall may not display mirrors correctly, specifically if the desired GPU is an NVIDIA one.
  - To fix this:
    - Arch users should check `nvidia-prime` is installed.
    - If you're on another distro (i.e. Fedora):
      - Run the below commands to create the prime-run script on your PATH:

        `mkdir ~/.local/bin`
        `cd ~/.local/bin`
        `touch prime-run`
        `nano prime-run`

      - Then, paste the following text, and save and exit the file with Ctrl+X:

        ```bash
          #!/bin/bash
          __NV_PRIME_RENDER_OFFLOAD=1 __VK_LAYER_NV_optimus=NVIDIA_only __GLX_VENDOR_LIBRARY_NAME=nvidia "$@"
        ```

      - Finally, make the script executable by running `sudo chmod +x prime-run`.

  - Then, modify your wrapper command in your instance's settings in Prism like so:

    ```bash
    sh -c "waywall wrap -- prime-run $INST_JAVA \"$@\""
    ```

  - Remember to replace `waywall` with the absolute path if you must.
  - Finally, uncheck "Use discrete GPU" in Prism Launcher settings if it was checked earlier when [setting up Minecraft](../mmc.html#Further-optimizations).
