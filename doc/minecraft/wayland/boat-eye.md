# Boat Eye

For boat eye, Waywall users have 2 main methods to change your mouse's sensitivity.
- Waywall sensitivity
    - Uses [mcsr-calcsens](https://github.com/Esensats/mcsr-calcsens) (Thank you Esensats)
    - This lets you change your sensitivity automatically when you change to tall resolution
- Windows-like raw input/DPI toggle
    - This mirrors what you would do 
    - Quickest to setup if your mouse's DPI is already set

## Waywall sensitivity
Skip steps 1 and 2 if you've never setup boat eye before

### 1. Find DPI and Minecraft Sens for Windows sens of 10
- Go to qMaxXen's [Minecraft 360 Calculator](https://qmaxxen.github.io/mc-360-calc/)
- Input your DPI, Minecraft Sens and Windows Sensitivity.
- Note the outputted "Cursor Sensitivity" and "cm / 360"
- Change the DPI on the website to the "Cursor Sensitivity" you noted, and change Windows Sens to 10
- Note that the Cursor Sensitivity is the same as your original but "cm / 360" is different. You now need to manually change the "Minecraft Sens" to have the "cm / 360" match the original
    - Someone may make a calculator to do this for you, but you can just do this by trial and error for now
- Now note down the final "Minecraft Sens"

### 2. Configure your Mouse DPI
- Using your mouse's software, change your DPI to the "Cursor Sensitivity" you noted, or the closest value
    - If your mouse is in this [list of support devices](https://github.com/libratbag/libratbag/tree/master/data/devices) for libratbag, you can use either `piper` or `ratbagctl` to configure its DPI
    - If you have a Razer mouse, you can use `openrazer`
    - If your mouse doesn't have a linux driver, you will need to use Windows via your existing boot, a VM (if you're daring enough), or another device to configure its DPI

### 3. Get new Waywall and Boat Eye Sensitivities
- Go to this website made for Esensat's [mcsr-calcsens](https://arjuncgore.github.io/mcsr-calcsens/)
    - You could also use his original python program if you prefer
- Input your Minecraft Sens from step 1, or if you skipped it, from options.txt
- Set your Waywall Sensitivity to 1
- Note down the outputs

### 4. Setup your Config File (If you're using one of Gore's Configs, see below)
- Set `config.input.sensitivity` to the "New normal sensitivity coefficient"
- Use `waywall.set_sensitivity()` to change your sensitivity when moving to tall and back to normal based on your config

### 4.1. Gore config setup
- Generic Config
    - Find this line in `config.lua`  
    ```lua
    local sens_change = { enabled = false, normal = 1.0, tall = 0.1 }
    ```
    - Set enabled to true, and normal and tall to the normal and tall sensitivity coefficients from mcsr-calcsens
- Barebones Config
    - Find these lines in `init.lua`
    ```lua
    -- ==== SENSITIVITIES ====
    local normal_sens = 1
    local tall_sens = 0.1
    ```
    - Set normal_sens and tall_sens to the sensitivity coefficients from mcsr-calcsens

### 5. General Boat Eye Setup
- Complete the steps from 2:30 to 3:40 in [Osh's Boat Eye Setup Video](https://www.youtube.com/watch?v=HcrrfsHrR_c)
- Set the Default boat mode in Ninjabrain Bot to "Green boat (with boat angle of 0)" 

## Windows-like Setup

### 1. Convert Windows Sensitivity to Linux Sensitivity using the following table

| Windows Sens | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
|:-----------------|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| EPP off | -0.96875 | -0.9375 | -0.875 | -0.75 | -0.625 | -0.5 | -0.375 | -0.25 | -0.125 | 0.0 | 0.25 | 0.5 | 0.75 | 1.0 | 1.25 | 1.5 | 1.75 | 2.0 | 2.25 | 2.5 |
| EPP on  | -0.9 | -0.8 | -0.7 | -0.6 | -0.5 | -0.4 | -0.3 | -0.2 | -0.1 | 0.0 | 0.1 | 0.2 | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 | 0.8 | 0.9 | 1.0 |

### 2. Change sensitivity in your settings

#### KDE
- Search mouse settings in krunner
- Set "Pointer speed" to your new sensitivity

#### Hyprland
- Open your config file in a code editor (code, nano, vim)
`~/.config/hypr/hyprland.conf`
- If you haven't added your devices config yet, run `hyprctl devices` in your terminal and you'll see an output like this
    ```bash
    $ hyprctl devices
        ...

        Input Device: turtle-beach-burst-ii-air-mouse

        ...
    ```
- Then add the following block of code to the config file, setting the name to what you got from the previous step, and sensitivity to your new sensitivity
    ```ini
    # eg: for a windows sensitivity of 3
    device {
        name = turtle-beach-burst-ii-air-mouse
        accel_profile = flat
        sensitivity = -0.875
        natural_scroll = false
    }
    ```
- Save the file and reload your config with `hyprctl reload`

#### Sway
- Open your config file in a code editor (code, nano, vim)
`~/.config/sway/config`
- If you haven't added your devices config yet, run `swaymsg -t get_inputs` in your terminal and you'll see an output like this
    ```bash
    $ swaymsg -t get_inputs
        ...
        Input device:Turtle Beach Burst II Air Mouse
        Type: pointer
        Identifier: 4341:20482:Turtle_Beach_Burst_II_Air_Mouse
        ...
    ```
- Then add the following block of code to the config file, setting the input identifier to what you got from the previous step, and pointer_accel to your new sensitivity
    ```ini
    # eg: for a windows sensitivity of 3
    input "4341:20482:Turtle_Beach_Burst_II_Air_Mouse" {
        natural_scroll disabled
        accel_profile "flat"
        pointer_accel -0.875
    }
    ```
- Save the file and reload your config with `swaymsg reload`

### 3. General Boat Eye Setup
- Complete the steps from 2:30 to 3:40 in [Osh's Boat Eye Setup Video](https://www.youtube.com/watch?v=HcrrfsHrR_c)
- Set the Default boat mode in Ninjabrain Bot to "Green boat (with boat angle of 0)" 
