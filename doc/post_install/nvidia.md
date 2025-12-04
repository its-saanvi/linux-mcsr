# NVIDIA Drivers

- Before we setup Minecraft we need to first install the NVIDIA Drivers. If you are not on an NVIDIA GPU you can skip to the [Java](java.html) section.
- Open up a terminal and then type in these commands.

```bash
sudo dnf install kernel-devel kernel-headers gcc make dkms acpid libglvnd-glx libglvnd-opengl libglvnd-devel pkgconfig
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf makecache
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
```

- This should install NVIDIA drivers on your system. Restart your system and you should have GPU acceleration.
- Remember! Do **NOT** install NVIDIA drivers from NVIDIA's official website. It creates some irreversible changes to the system that the package manager of Fedora cannot detect and might bloat your install with unnecessary packages. Moreover, everytime you need to update the driver, you would have to run through that process again. Whereas with the package manager, the driver updates will be rolled out after testing along with your normal upgrades. Learn more [here](https://forums.developer.nvidia.com/t/stop-asking-simple-users-to-install-the-unfriendly-run-file/48586).

After rebooting, move ahead to [downloading and installing Java](java.html).
