# Boat Eye on Wayland

Before setting up boat eye, first setup [waywall](waywall.html) for window resizing, magnifiers and sensitivity changes.

## What is Boat Eye?

Boat Eye is a method of measuring the size of an eye by using a boat to simulate the movement of the eye in the game. It is a way to get a more accurate measurement of the eye size.

## Benefits to Boat Eye on Waywall
- Lets you decrease your sensitivity automatically when you change to tall resolution, or manually with either a mouse button or keyboard key (not limited to mouse buttons like usual).
- Easily allows the use of a ["god sensitivity"](https://gist.github.com/ExeRSolver/c4e852bb2527069e08c1a5e0a9c47613) without changing how the mouse feels whatsoever.
  - With a god sens, the default boat mode in Ninjabrain Bot may be set to green boat, removing the need to get in a boat and F3+C to get green boat before measuring, assuming you haven't steered a boat at any point beforehand.

## 1: Sensitivity Settings

Do step 1.1 if you're transitioning from Windows and step 1.2 if you're setting up boat eye from scratch on Linux.

### 1.1: Transitioning from Windows
#### 1.1.1: Get Waywall Sensitivities
- Go to the [Waywall Boat Eye Utility](https://arjuncgore.github.io/waywall-boat-eye-calc/) Website.
- Input your DPI, Minecraft Sensitivity and Windows Sensitivity into "Waywall Sensitivities".
  - If you already setup your compositor sensitivity and are used to that, you may input your Linux Sensitivity instead of your old Windows Sensitivity.
- Note down the outputs.

### 1.1.2: Set your Compositor sensitivity

- Convert your Windows cursor speed to the corresponding Linux pointer speed using the following table:

| Windows Sens | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
|:-----------------|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| EPP off | -0.96875 | -0.9375 | -0.875 | -0.75 | -0.625 | -0.5 | -0.375 | -0.25 | -0.125 | 0.0 | 0.25 | 0.5 | 0.75 | 1.0 | 1.25 | 1.5 | 1.75 | 2.0 | 2.25 | 2.5 |
| EPP on  | -0.9 | -0.8 | -0.7 | -0.6 | -0.5 | -0.4 | -0.3 | -0.2 | -0.1 | 0.0 | 0.1 | 0.2 | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 | 0.8 | 0.9 | 1.0 |

- With the value from the table above, change your pointer speed in your compositor's configuration.
- Below are some examples for some common compositors.

<details>
<summary>KDE</summary>
<ul>
<li>Press <kbd>Alt</kbd>+<kbd>F2</kbd> to open KRunner, and search for “mouse settings”.</li>
<li>Set “Pointer speed” to your new sensitivity.</li>
</ul>
</details>


<details>
  <summary>Hyprland</summary>

  <ul>
    <li>Open the Hyprland config file in a text editor: <code>~/.config/hypr/hyprland.conf</code>.</li>
    <li>If you have not added your devices config yet, run <code>hyprctl devices</code> in your terminal and you will see an output like this:</li>
  </ul>

  <pre><code class="language-bash">$ hyprctl devices
...

Input Device: turtle-beach-burst-ii-air-mouse

...</code></pre>

  <ul>
    <li>Then add the following block of code to the config file, setting the name to what you got from the previous step, and sensitivity to your new sensitivity:</li>
  </ul>

  <pre><code class="language-ini"># eg: for a windows sensitivity of 3
device {
    name = turtle-beach-burst-ii-air-mouse
    accel_profile = flat
    sensitivity = -0.875
    natural_scroll = false
}</code></pre>

  <ul>
    <li>Save the file and reload your config with <code>hyprctl reload</code>.</li>
  </ul>
</details>


<details>
  <summary>Sway</summary>

  <ul>
    <li>Open your config file in a text editor: <code>~/.config/sway/config</code>.</li>
    <li>If you have not added your device config yet, run: <code>swaymsg -t get_inputs</code> in your terminal. You will see output like this:</li>
  </ul>

  <pre><code class="language-bash">$ swaymsg -t get_inputs
...
Input device:Turtle Beach Burst II Air Mouse
Type: pointer
Identifier: 4341:20482:Turtle_Beach_Burst_II_Air_Mouse
...</code></pre>

  <ul>
    <li>Add the following block to your config file, replacing the identifier and sensitivity value with your own:</li>
  </ul>

  <pre><code class="language-ini"># Example: Windows sensitivity 3
input "4341:20482:Turtle_Beach_Burst_II_Air_Mouse" {
    natural_scroll disabled
    accel_profile "flat"
    pointer_accel -0.875
}</code></pre>

  <ul>
    <li>Save the file and reload Sway with:
      <code>swaymsg reload</code>
    </li>
  </ul>

</details>


### 1.2: Setting up Boat eye from Scratch
- Go to the [Waywall Boat Eye Utility](https://arjuncgore.github.io/waywall-boat-eye-calc/) Website.
- Input your current Minecraft Sensitivity on the "Linux Boat Eye Calc".
- Note down the outputs.

## 2: Setup your waywall config

- **If you're using one of Gore's pre-made configs, see the section below.**
- If you're using your own config:
  - Set `config.input.sensitivity` to the "New normal sensitivity coefficient" given by mcsr-calcsens.
  - Use `waywall.set_sensitivity()` to change your sensitivity when moving to tall and back to normal.

### 2.1: Gore config setup

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

## 3: General boat eye setup

- Set your Minecraft sensitivity to `0.02291165`.
  - Remember to update your sensitivity in `minecraft/config/mcsr/standardsettings.json` if you're using StandardSettings, otherwise just change `minecraft/options.txt`.
- Complete the steps in [this boat eye setup video](https://youtu.be/FQiGzO-oCZo) to setup Ninjabrain Bot.
- Finally, **turn off raw input** ingame (change it in StandardSettings if you're using it) - the waywall sens will only take affect if you do this.
    - Note that you won't be able to toggle sens using raw input anymore, you will either need to use waywall sensitivities or a dpi switch if you prefer.


## 4: Measuring an eye

- After setting your sensitivity with the method above, watch the [boat eye setup video](https://youtu.be/l1Z2t9e6Qko?t=442) from 7:22 for an example boat eye measurement.
  - On either of Gore's pre-made configs, the default key for tall resizing & magnifying is **F4**.
  - Note that you can skip pressing F3+C when exiting the boat - the boat icon on Ninjabrain Bot should be green by default.
    - This is made possible by using the god sens in Minecraft and the specific waywall sensitivity values given by mcsr-calcsens.
  - You don't need to toggle your raw input while measuring either, going to the tall resolution should already lower your sensitivity to make it easier to measure an eye
