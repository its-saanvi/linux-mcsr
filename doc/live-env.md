# Live Environment

The instructions given below will be the setup step to start installing Fedora on your hard drive.

# Booting into the Live USB

- After going through and installing the ISO onto your USB stick, it is now time to install Fedora on your system.
- Plug in your USB drive and restart your PC. Before it boots into Windows, it'll tell you what key to press to enter UEFI setup - usually it's Delete, Escape or one of the function keys (i.e. F2).
- Once you're in the BIOS, make sure to have Secure Boot disabled and make sure to have CSM/BIOS mode disabled. These are usually under the menu labeled "Boot".
- Now, look for an option labeled **Boot Override** or **Boot Options**, usually under the "Boot" or "Exit" menus.
  Under here, select the USB you just installed Fedora on and the boot should continue from there and drop you into a live environment of Fedora.
- If you can't find **Boot Options** then changing the **Boot Order** is an alternative. Under here, reorder the options to have the USB stick at the top. Now, select Exit & save changes, and it should automatically reboot into a live environment of Fedora.
- You will be greeted with a boot screen listing some boot options initially, just hit enter on the first option to boot into Live USB mode.

# Testing the Live Environment

- Now that you have the Live Environment running, you can test out the OS partially here.
- Linux, given its versatility, doesn't require you to install the system on your physical hardware in order to test it, so whatever you do on here will not affect what you have already on your system. Feel free to mess around!
- When you are done, you can proceed with the [installation](installation.html) procedure.
