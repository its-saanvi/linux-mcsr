# Boat Eye on X11

Setting up boat eye on X11 is not as easy as it is on Windows. You might see some  weird behaviour while using it just because X11 handles mouse movement much different than Windows. Make sure to follow instructions as closely as possible.

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

## i3

i3 is an X11 WM that has been tested a lot and it works very well with Fedora and all the tools. You can set it up in [this](i3.html) section of the guide.

## Setting up mouse drivers

- Check online if your mouse has software supported on Linux.
  - For most Razer mice, install `openrazer` for the GUI as well as the driver.
  - For most Logitech mice, install `piper` for the GUI and `libratbag` for the driver.
  - If you don't have mouse software, you can either:
    - switch back to Windows and set your DPI (and DPI toggle if you can/want) as necessary,
    - OR use software like [maccel](https://github.com/Gnarus-G/maccel?tab=readme-ov-file#install) instead.
      - Instead of inputting your mouse's DPI into Priffie's calculator in the next section, input **1**. The resulting New DPI is what you should use in the **Sens Multiplier** field in maccel.
- After setting up your mouse drivers, make sure to open the GUI for setting up your mouse and check that your mouse is showing up on it.

## Finding your sens values

- If you're setting up boat eye for the first time, refer to [Priffie's calculator](https://www.desmos.com/calculator/uld5u8glky) to figure out your boat eye cursor speed, DPI and sensitivity.
  - You can get to options.txt by right clicking your instance in Prism Launcher > Folder > minecraft > options.txt.
  - Leave cursor speed on 10 in the calculator, assuming you haven't changed pointer speed on Linux before (on Plasma, check if pointer speed is 0.00 in System Preferences > Mouse > select your mouse under the Device dropdown).
  ![image](https://github.com/its-saanvi/linux-mcsr/assets/94102031/08041a38-7909-495f-b90f-b453b14152ce)
- To convert the Windows cursor speed from Priffie's calculator to the appropriate Linux speed use the EPP off row in the table above.
  - To get your resulting speed, take your value from the table above and subtract 1.
    - For example, if the calculator gave you a cursor speed of 3, the corresponding value in the table is 1/8 (0.125), and your resulting speed would be 0.125 - 1 = **-0.875**.

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
- Then, add a hotkey to toggle this res using `ingame_toggle_res(n)`.
- Check that the resizing works by running your resetti profile and pressing your hotkey ingame.
  - If your game doesn't become thin and tall, see the [Issues with certain WMs](https://its-saanvi.github.io/linux-mcsr/boat-eye.html#issues-with-certain-wms) section and double-check your config.

## Eye Measuring Projector

- There are two methods for displaying an eye measuring projector:
  - You can use [xEyeSee by qMaxXen](https://github.com/qMaxXen/xEyeSee?tab=readme-ov-file#xeyesee) to display an eye measuring projector automatically when using Tall Macro. This method does not require OBS Studio.
  - The second method is to use OBS Studio. You can follow [Priffie's YouTube tutorial](https://youtu.be/_CXmCUYJbSk?si=2xyTiTuAnlpGdsDl) to setup an OBS projector.
    - Note that this projector won't automatically position itself beside your game unlike xEyeSee - you should instead drag the window behind your game manually.

## Polling Rate

- Setting the polling rate to a lower value is nicer just because having a higher polling rate can affect how Minecraft and/or X11 behaves in response to specific cursor speeds.
- Open your mouse configuration GUI and search for the tab that configures the polling rate of your mouse. Make sure to set it to a low value (such as 250Hz).
- This is not a de-facto standard for all cursor speeds and it doesn't fix issues for all mice.

## Finishing Up

- This covers all of the Linux-specific setup for boat eye - check out the following timestamps in osh's boat eye guide for the remaining setup:
  - [2:32](https://youtu.be/HcrrfsHrR_c?t=152) for Ninjabrain Bot settings.
  - [5:24](https://youtu.be/HcrrfsHrR_c?t=324) for actually performing a pixel perfect eye measurement.
    - Note that toggling raw input as shown may introduce issues - toggling your mouse to a lower DPI is preferred instead.
- Congratulations! We have successfully set up boat eye on Linux!
