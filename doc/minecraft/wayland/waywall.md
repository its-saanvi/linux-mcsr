# waywall

- **waywall** is a Wayland compositor designed to run inside your existing Wayland session. It provides various convenient features for speedrunning, including but not limited to:
  - Window resizing
  - Key remapping
  - Ninjabrain Bot support
  - Mirrors (i.e. magnifiers for eye measuring, F3, etc.) without using OBS
  - Lots of custom functionality.
- If you're using **X11**, please use [resetti](../x11/resetti.html) instead.

## Installation
- To install waywall on **Fedora**:
  - **Fedora 42 onwards**, prebuilt binaries are available and is **recommended** way to install waywall. Please download `**.x86_64.rpm` package from [releases of waywall](https://github.com/tesselslate/waywall/releases). 
    - If you are using KDE Plasma(default with Desktop edition of Fedora), installation can be done by double clicking on .rpm file and installing it via Discover app.
    - In any other case you can use, `sudo rpm -i [path_to_rpm_file]` provide path to `.rpm` file. 
    
      Expample: `sudo dnf install ~/Downloads/waywall.x86_64.rpm`
    

  - **Fedora 41 and below** 
    - First install the dependencies with the following terminal command:

      ```bash
      sudo dnf install libspng-devel cmake meson mesa-libEGL-devel luajit-devel libwayland-client libwayland-server libwayland-cursor libxkbcommon-devel xorg-x11-server-Xwayland-devel wayland-protocols-devel wayland-scanner wayland-devel libXcursor-devel libXi-devel libXinerama-devel libXrandr-devel
      ```

    - Then, run the commands on [this page of the waywall documentation](https://tesselslate.github.io/waywall/00_installation.html#compiling) to compile waywall from source.
    

- On **Arch Linux**, [you can install waywall through the AUR](https://aur.archlinux.org/packages/waywall-working-git).
- On **Debian** , prebuilt binaries are available for waywall however they only work with **Debian 13 and up** as older versions do not have updated dependancies to run waywall. Please download `.deb` version from [releases of waywall](https://github.com/tesselslate/waywall/releases).  
  - Installtion of package can be done by double clicking on `.deb` and installing using default system install.
  - In any other case apt can be used to install .deb packages using following command.
  `sudo apt install locationTodebfile` eg. `sudo apt install ~/Downloads/waywall.deb`
- On **Ubuntu**/**Ubuntu based Distros (Linux Mint, MX Linux, Pop OS! etc)**, 
  
  - **Ubuntu 26.04** has been tested and verified  working with waywall using `.deb` package. Follow the same installations instruction as Debian.
  - **Linux Mint 22.3 and below/Any distro based on Ubuntu 24.04 or below** cannot run waywall due outdated dependancies and should switch to x11 and use [resetti](../x11/resetti.html) instead. 

## Verification of installation and next steps
- Run `waywall` in a terminal to check it's installed properly.
it should produce similar ouput:
  ```waywall

  Usage:
          waywall wrap -- CMD      Run the specified command in a new waywall instance

  Options:
          --profile PROFILE        Run waywall with the given configuration profile
          --allow-mc-x11           Allows Minecraft to run under X11. This will result
                                  in a degraded experience.
          --no-env-reexec          Disable re-executing waywall with the parent process'
                                  environment
  ```
- In case it doesn't or ouputs waywall command not found
  - If you have installed waywall from prebuilt binaries, verify that waywall exist in following path `/usr/bin/waywall` in case it doesn't please reinstall waywall.                           
  - In case you are building waywall from source
    - Use the absolute path to the waywall executable and verify it works (i.e. if you built waywall in `/home/username/waywall/build/waywall`, run `/home/username/waywall/build/waywall/waywall`).
    - The wrapper command for your instance in the next step should also reflect this path in your launcher .i.e instead of `waywall wrap --`, it should be path where waywall build is present i.e `/home/username/waywall/build/waywall/waywall wrap --`
- Once waywall is installed properly, visit the [next page of the documentation](https://tesselslate.github.io/waywall/00_setup.html) to patch GLFW and set up your instance to launch within waywall.

- After this, move on to the [next section](waywall-config.html) to install an example config and learn how to customize it to your liking.

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
