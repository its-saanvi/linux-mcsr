# Boat Eye on Wayland

Before setting up boat eye, first setup [waywall](waywall.html) for window resizing and magnifiers.

For boat eye, Wayland users have 2 main methods to change your mouse's sensitivity:

- Waywall sensitivity
  - Uses [mcsr-calcsens](https://github.com/Esensats/mcsr-calcsens). (Thank you Esensats!)
  - Lets you decrease your sensitivity automatically when you change to tall resolution, or manually with either a mouse button or keyboard key (not limited to mouse buttons like usual).
  - Also easily allows the use of a ["god sensitivity"](https://gist.github.com/ExeRSolver/c4e852bb2527069e08c1a5e0a9c47613) without changing how the mouse feels whatsoever.
    - With a god sens, the default boat mode in Ninjabrain Bot may be set to green boat, removing the need to get in a boat and F3+C to get green boat before measuring, assuming you haven't steered a boat at any point beforehand.
- Windows-like setup + raw input/DPI toggle
  - This mirrors what you would do on Windows, which involves changing your mouse's DPI and your system's pointer speed to ensure things feel the same after changing your Minecraft sensitivity.
  - Quickest to setup if your mouse's DPI is already set accordingly, i.e. if you had boat eye set up on Windows beforehand.

## Method 1: Waywall sensitivity

Skip steps 1.1 and 1.2 if you've never setup boat eye before.

### 1.1: Find DPI and Minecraft sens for Windows sens of 10

- Go to qMaxXen's [Minecraft 360 Calculator](https://qmaxxen.github.io/mc-360-calc/).
- Input your DPI, Minecraft Sens and Windows Sensitivity.
- Note the outputted "Cursor Sensitivity" and "cm / 360".
- Change the DPI on the website to the "Cursor Sensitivity" you noted, and change Windows Sens to 10
- Note that the Cursor Sensitivity is the same as before, but "cm / 360" is different. Change the "Minecraft Sens" until the "cm / 360" matches the original.
- Note down the final DPI and Minecraft sens.

### 1.2: Configure your mouse DPI

- Using your mouse's software, change your DPI to the final DPI you noted in the previous section, or the closest possible value.
  - If your mouse is in [this list of devices](https://github.com/libratbag/libratbag/tree/master/data/devices), install and use either `piper` or `ratbagctl` to configure its DPI.
  - If you have a Razer mouse, install and use `openrazer`.
  - If your mouse doesn't have a Linux driver, you will need to boot back into Windows, use a Windows VM (if you're daring enough), or another device with Windows installed to configure its DPI.
    - OR use software like [maccel](https://github.com/Gnarus-G/maccel?tab=readme-ov-file#install) instead.
      - In the **Sens Multiplier** field in maccel, input the new DPI you found in the previous section divided by your current DPI.
  - Note that not using the exact DPI will not affect the accuracy of your eye measurements.

### 1.3: Get new waywall and boat eye sensitivities

- Go to [this website made for Esensat's mcsr-calcsens](https://arjuncgore.github.io/mcsr-calcsens/).
  - You could also use the [original Python program](https://github.com/Esensats/mcsr-calcsens) if you prefer.
- Set Waywall Sensitivity to 1.
- Input the new Minecraft sens you got from step 1.1.
  - If you skipped step 1.1, instead input your current Minecraft sens from options.txt.
    - You can find your current options.txt sensitivity by right clicking your instance in Prism Launcher > Folder > minecraft > options.txt > searching for `mouseSensitivity`.
- Note down the outputs.

### 1.4: Setup your waywall config

- **If you're using one of Gore's pre-made configs, see the section below.**
- If you're using your own config:
  - Set `config.input.sensitivity` to the "New normal sensitivity coefficient" given by mcsr-calcsens.
  - Use `waywall.set_sensitivity()` to change your sensitivity when moving to tall and back to normal.

### 1.4.1: Gore config setup

- Generic Config
  - Find this line in `config.lua`:

    ```lua
    local sens_change = { enabled = false, normal = 1.0, tall = 0.1 }
    ```

  - Set enabled to true, and normal and tall to the normal and tall sensitivity coefficients from mcsr-calcsens.
- Barebones Config
  - Find these lines in `init.lua`:

    ```lua
    -- ==== SENSITIVITIES ====
    local normal_sens = 1
    local tall_sens = 0.1
    ```

  - Set normal_sens and tall_sens to the sensitivity coefficients from mcsr-calcsens.

### 1.5: General boat eye setup

- Set your Minecraft sensitivity to what was given by mcsr-calcsens.
  - Remember to update your sensitivity in `minecraft/config/mcsr/standardsettings.json` if you're using StandardSettings, otherwise just change `minecraft/options.txt`.
- Complete the steps from 2:30 to 3:40 in [osh's boat eye setup video](https://youtu.be/HcrrfsHrR_c?t=150).
- In Ninjabrain Bot options > Optional Features > Boat Measurements, set the Default boat mode to "Green boat (with boat angle of 0)".

## Method 2: Windows-like setup

### 2.1: Converting Windows sensitivity

- Convert your Windows cursor speed to the corresponding Linux pointer speed using the following table:

| Windows Sens | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
|:-----------------|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| EPP off | -0.96875 | -0.9375 | -0.875 | -0.75 | -0.625 | -0.5 | -0.375 | -0.25 | -0.125 | 0.0 | 0.25 | 0.5 | 0.75 | 1.0 | 1.25 | 1.5 | 1.75 | 2.0 | 2.25 | 2.5 |
| EPP on  | -0.9 | -0.8 | -0.7 | -0.6 | -0.5 | -0.4 | -0.3 | -0.2 | -0.1 | 0.0 | 0.1 | 0.2 | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 | 0.8 | 0.9 | 1.0 |

### 2.2: Change sensitivity in your settings

- With the value from the table above, change your pointer speed in your compositor's configuration.
- Below are some examples for some common compositors.

#### KDE

- Press Alt+F2 to open KRunner, and search for "mouse settings".
- Set "Pointer speed" to your new sensitivity.

#### Hyprland

- Open the Hyprland config file in a text editor: `~/.config/hypr/hyprland.conf`.
- If you haven't added your devices config yet, run `hyprctl devices` in your terminal and you'll see an output like this:

    ```bash
    $ hyprctl devices
        ...

        Input Device: turtle-beach-burst-ii-air-mouse

        ...
    ```

- Then add the following block of code to the config file, setting the name to what you got from the previous step, and sensitivity to your new sensitivity:

    ```ini
    # eg: for a windows sensitivity of 3
    device {
        name = turtle-beach-burst-ii-air-mouse
        accel_profile = flat
        sensitivity = -0.875
        natural_scroll = false
    }
    ```

- Save the file and reload your config with `hyprctl reload`.

#### Sway

- Open your config file in a text editor: `~/.config/sway/config`.
- If you haven't added your devices config yet, run `swaymsg -t get_inputs` in your terminal and you'll see an output like this:

    ```bash
    $ swaymsg -t get_inputs
        ...
        Input device:Turtle Beach Burst II Air Mouse
        Type: pointer
        Identifier: 4341:20482:Turtle_Beach_Burst_II_Air_Mouse
        ...
    ```

- Then add the following block of code to the config file, setting the input identifier to what you got from the previous step, and pointer_accel to your new sensitivity:

    ```ini
    # eg: for a windows sensitivity of 3
    input "4341:20482:Turtle_Beach_Burst_II_Air_Mouse" {
        natural_scroll disabled
        accel_profile "flat"
        pointer_accel -0.875
    }
    ```

- Save the file and reload your config with `swaymsg reload`.

### 2.3: General boat eye setup

- Complete the steps from 2:30 to 3:40 in [osh's boat eye setup video](https://youtu.be/HcrrfsHrR_c?t=150).

## Measuring an eye

- After setting your sensitivity with one of the methods above, watch [osh's video](https://youtu.be/HcrrfsHrR_c?t=324) from 5:24 for an example boat eye measurement.
  - On either of Gore's template configs, the default key for tall resizing & magnifying is **F4**.
  - Note that you can skip pressing F3+C when exiting the boat - the boat icon on Ninjabrain Bot should be green by default.
    - This is made possible by using the god sens in Minecraft and the specific waywall sensitivity values given by mcsr-calcsens.
