# Setting up Minecraft

This section goes over how to best set up Minecraft itself for speedrunning.

## Launcher

- Here, we will be installing a fork of MultiMC called [Prism Launcher](https://prismlauncher.org).
- On Fedora, install Prism by opening a terminal and running these commands:

```bash
sudo dnf copr enable g3tchoo/prismlauncher
sudo dnf install prismlauncher
```

- This should install Prism Launcher - open the start menu and search for it.
- Users on other distros should locate their distro on the [Prism download page](https://prismlauncher.org/download/?from=button#official-packages) and follow the instructions.
  - **Avoid using Flatpak (Flathub)** where possible - you may run into issues running [waywall](wayland/waywall.html) later.

## Instance Setup

- You can watch this [Windows setup guide](https://www.youtube.com/watch?v=RSLv7FfQZKY) to get your Minecraft instance set up. The instructions should be largely the same on Linux, with the exception of:
  - Running Java apps (i.e. ModCheck), as explained in the [Java](../post_install/java.html) section earlier, can be done in the terminal with `java -jar <path/to/jarfile.jar>`, replacing `<path/to/jarfile.jar>` with the actual path to the .jar file.
  - Ninjabrain Bot will not work out of the box on Wayland - we will setup an app called [waywall](./wayland/waywall.html) later to address this.
  - Jingle is a Windows-only application - we will set up alternatives later for either Wayland or X11.

## Further optimizations

- The default version of GLFW included in LWJGL for Minecraft version 1.16.1 **may cause crashes** when tabbing out of the game, and tends to have worse performance.
  - Update LWJGL by right clicking your instance in Prism > Edit > Version > Right click **LWJGL 3** > Change Version > Select **3.3.3** (newer versions have their own share of issues).
- Using **jemalloc** may greatly improve memory performance for Minecraft on Linux.
  - To install jemalloc on Fedora, open up a terminal and run `sudo dnf install jemalloc-devel`.
  - To find where jemalloc installed to, run `jemalloc-config --libdir`. This is usually `/usr/lib`, which means the full path to jemalloc would be `/usr/lib/libjemalloc.so`.
  - To ensure Minecraft runs with jemalloc, go to Prism > Settings > Environment Variables. Add a new environment variable with the name `LD_PRELOAD`. Under "Value", enter the path to jemalloc we found earlier.
- **NVIDIA users** should add another environment variable named `__GL_THREADED_OPTIMIZATIONS` and set its value to 0. With driver versions greater than 525, not having this variable set may cause crashes, or make preemptive navigation very inconsistent because of a driver-side optimization to the Minecraft renderer (colloquially known as "preemptive bug").
- Your environment variables should look something like this:
  ![image](https://github.com/user-attachments/assets/bbfeb4ab-2201-41d1-bc94-9eb3aa2f7088)
- Finally, users on dual-GPU setups (i.e. laptops with integrated and dedicated graphics) should ensure Minecraft runs with dedicated graphics.
  - In Prism, go to Settings > Minecraft > Tweaks > Check **Use discrete GPU**.

## Moving forward

Move to [the next section](wayland.html) to continue setup.
