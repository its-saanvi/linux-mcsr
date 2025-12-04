# Boat Eye on X11

Setting up boat eye on X11 is not as easy as it is on Windows. You might see some  weird behaviour while using it just because X11 handles mouse movement much different than Windows. Make sure to follow instructions as closely as possible.

## Setting up mouse drivers

- Check online if your mouse has software supported on Linux.
  - For most Razer mice, install `openrazer` for the GUI as well as the driver.
  - If your mouse is in [this list of devices](https://github.com/libratbag/libratbag/tree/master/data/devices) install `piper` for the GUI and `libratbag` for the driver.
  - If you don't have mouse software, you can either:
    - switch back to Windows and set your DPI (and DPI toggle if you can/want) as necessary,
    - OR use software like [maccel](https://github.com/Gnarus-G/maccel?tab=readme-ov-file#install) instead.
      - Instead of inputting your mouse's DPI into the sens calculator in the next section, input **1**. The resulting New DPI is what you should use in the **Sens Multiplier** field in maccel.
    - OR skip changing your DPI and cursor speed entirely, and just change your Minecraft sensitivity.
      - Find the closest value to your current sensitivity in the first column of [this list](https://gist.github.com/ExeRSolver/cd8e89256a5f51ee4e32ba9df2db748f), and change it accordingly.
      - You can find your current sensitivity by right clicking your instance in Prism Launcher > Folder > minecraft > options.txt > searching for `mouseSensitivity`.
      - Remember to update your sensitivity in `minecraft/config/mcsr/standardsettings.json` if you're using StandardSettings, otherwise just change `minecraft/options.txt`.

## Finding your sens values

- If you're setting up boat eye for the first time, refer to this [sens calculator](https://priffin.github.io/Pixel-Perfect-Tools/calc.html) to figure out your boat eye cursor speed, DPI and sensitivity.
  - You can find your current options.txt sensitivity by right clicking your instance in Prism Launcher > Folder > minecraft > options.txt > searching for `mouseSensitivity`.
  - Leave cursor speed on 10 in the calculator, assuming you haven't changed pointer speed on Linux before (on Plasma, check if pointer speed is 0.00 in System Preferences > Mouse > select your mouse under the Device dropdown).
- To convert the Windows cursor speed from the sens calculator to the appropriate Linux speed, use the EPP off row in the table below.

| Windows Sens | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
|:-----------------|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| EPP off | -0.96875 | -0.9375 | -0.875 | -0.75 | -0.625 | -0.5 | -0.375 | -0.25 | -0.125 | 0.0 | 0.25 | 0.5 | 0.75 | 1.0 | 1.25 | 1.5 | 1.75 | 2.0 | 2.25 | 2.5 |
| EPP on  | -0.9 | -0.8 | -0.7 | -0.6 | -0.5 | -0.4 | -0.3 | -0.2 | -0.1 | 0.0 | 0.1 | 0.2 | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 | 0.8 | 0.9 | 1.0 |

- For example, if the calculator gave you a cursor speed of 3, the corresponding value in the table is **-0.875**.

## Setting your sens values

- Once you know your settings:
  - Set the DPI to the DPI that you took from the calculator in your mouse configuration application.
  - Set your Minecraft sensitivity in `minecraft/config/mcsr/standardsettings.json`, or `minecraft/options.txt` if you disabled/aren't using StandardSettings.
- Install `xinput` using your package manager, to set your cursor speed accurately in X11.
- Figure out the correct device ID for your mouse by running `xinput` in a terminal and analyzing the output.
- Pick the correct id corresponding to your mouse and note it down.
- Eg: `Logitech G102 LIGHTSYNC Gaming Mouse     id=11 [slave  pointer  (2)]` Here the device id would be `11`.
- Now set the cursor speed by executing the following command in a terminal:

```bash
xinput set-prop <device_id> "libinput Accel Speed" <speed>
```

- Here, replace `<device_id>` with the id and `<speed>` with the resulting speed you calculated from the table before.
- In our example, the command would be `xinput set-prop 11 "libinput Accel Speed" -0.875`.
- You should also disable mouse acceleration with the command:

```bash
xinput set-prop <device_id> "libinput Accel Profile Enabled" 0 1 0
```

- These settings will reset after rebooting your PC - if you're happy with how your mouse feels, save your configuration by creating and editing a libinput configuration file:

```bash
sudo touch /etc/X11/xorg.conf.d/99-libinput-custom-config.conf
sudo nano /etc/X11/xorg.conf.d/99-libinput-custom-config.conf
```

- Paste the following text into this file, replacing `<speed>` with your pointer speed calculated earlier and `<mousename>` with the name of your mouse as shown when running `xinput`.

```bash
Section "InputClass"
  Identifier "PointerSpeed"
  MatchDriver "libinput"
  MatchProduct "<mousename>"
  Option "AccelProfile" "flat"
  Option "AccelSpeed" "<speed>"
EndSection
```

## Window resizing with resetti

- If you haven't already, install [resetti](resetti.html) to handle window resizing.
- In your config, add an entry under your `alt_res` list with the dimensions `"384x16384+768,-7652"`.
  - The position (`768,-7652` in this case) may be incorrect depending on your monitor setup, change it as necessary to position the game in the center of your monitor.
    - Here's a simple rule for finding the proper position to center the game: `X = (monitor width / 2) - (resize width / 2)`, `Y = (monitor height / 2) - (resize height / 2)`.
- Then, add a hotkey to toggle this res at the bottom of your config using `ingame_toggle_res(n)`.
- Check that the resizing works by running resetti and pressing your hotkey ingame.
  - If your game doesn't become thin and tall, see the [Issues with certain WMs](https://its-saanvi.github.io/linux-mcsr/minecraft/x11/boat-eye.html#issues-with-certain-wms) section and double-check your config.

## Eye Measuring Projector

- There are two methods for displaying an eye measuring projector:
  - You can use [xEyeSee](https://github.com/qMaxXen/xEyeSee?tab=readme-ov-file#xeyesee) to display an eye measuring projector automatically when using Tall Macro. This method does not require OBS Studio.
  - The second method is to use OBS Studio. You can follow [this tutorial](https://youtu.be/_CXmCUYJbSk?si=2xyTiTuAnlpGdsDl) to setup an OBS projector.
    - Note that this projector won't automatically position itself beside your game unlike xEyeSee - you should instead place the window behind your game yourself.

## Issues with certain WMs

- There are some window managers that have trouble with out-of-bounds window resizing, or just window resizing in general:
  - kwin (KDE Plasma Desktop Environment)
  - muffin (Linux Mint/Cinnamon Desktop Environment)
  - xfwm (XFCE Desktop Environment)
  - mutter (Gnome Desktop Environment)
- Before switching desktop environments/window managers, check if initially resizing the game window out of monitor bounds works for you.
  - Set the `play_res` and each `alt_res` option in your resetti config to be 1 pixel larger than your monitor's bounds in either dimension.
  - Make sure to unmaximize/unfullscreen your game window (play in borderless if possible - on KDE, press Alt+F3 and disable window borders).
    - On i3 or other tiling window managers, make sure the game window is undocked (make the window floating).
  - After this, you may also be required to manually drag the game window partially offscreen before your resizing hotkeys work properly.

## i3

i3 is an X11 WM that has been tested a lot and it works very well with Fedora and all the tools. You can set it up in [this](i3.html) section of the guide.

## Finishing Up

- This covers all of the Linux-specific setup for boat eye - check out the following timestamps in osh's boat eye guide for the remaining setup:
  - [2:32](https://youtu.be/HcrrfsHrR_c?t=152) for Ninjabrain Bot settings.
  - [5:24](https://youtu.be/HcrrfsHrR_c?t=324) for actually performing a pixel perfect eye measurement.
    - Note that toggling raw input as shown may introduce issues - toggling your mouse to a lower DPI is preferred instead.
- A high polling rate on your mouse may also cause problems, such as lag when moving the ingame camera. Use your mouse software and decrease it if necessary - usually anything below 1000Hz is fine.
- Congratulations! We have successfully set up boat eye on Linux!
