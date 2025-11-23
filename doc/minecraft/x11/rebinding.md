# Rebinding Keys (for searchcrafting)

- Install `xdotool` and `xmodmap`

```bash
sudo dnf install xdotool xmodmap
```

- Now make a new file called `Rebinder.py` wherever you like and copy the following contents into it.

```python
import os

# Settings
window_filter = "Minecraft*"
rebinds = {
    25: "h",
    43: "w",
}
reset_rebinds = {
    43: "h",
    25: "w",
}


rebound_keys = False
while True:
    active_window = os.popen(
        "xdotool getactivewindow getwindowclassname").read()
    if window_filter in active_window and not rebound_keys:
        for (keycode, keysym) in rebinds.items():
            rebind_cmd = f"xmodmap -e 'keycode {keycode} = {keysym}'"
            os.system(rebind_cmd)
            print(f"Rebound Keycode: {keycode} to Keysym: {keysym}")
            rebound_keys = True
    elif window_filter not in active_window and rebound_keys:
        for (keycode, keysym) in reset_rebinds.items():
            reset_cmd = f"xmodmap -e 'keycode {keycode} = {keysym}'"
            process = os.popen(reset_cmd)
            os.system(reset_cmd)
            print(f"Rebound Keycode: {keycode} to Keysym: {keysym}")
            rebound_keys = False
```

- Here you can configure what keycodes can be rebound to what key symbols and how you can reset them to their original state (this happens when you are not focussed on a Minecraft instance).
  - This information can be obtained by running `xev` in a terminal and hitting the respective key. You need to look for the **Key Press** or **Key Release** event in the output which will state the keycode and keysym in the following lines after it. The examples are a good place to start. Hit `h` and `w` and see what the keycodes are. They should be `43` and `25` respectively. The example is a circular rebind from `h -> w` and `w -> h`.
- Names for characters that aren't on your native keyboard layout (for example, the `Ø` character found on Danish & Norwegian layouts) can be found [here](https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap).
  - To find the matching name, first try searching for the character in the list with Ctrl+F (in the case of `Ø`, the matching name is "oslash").
  - Otherwise, find a proper name for the character and attempt to search for that instead (for example, the [Wikipedia page for the Armenian alphabet](https://en.wikipedia.org/wiki/Armenian_alphabet#Alphabet) is especially useful).
- **NOTE** If you rebind keys using this method, you won't need to change any binds ingame. Minecraft will automatically detect the change in layout and adjust accordingly.
- Now running `python3 Rebinder.py` will rebind your keys if focussed on a Minecraft window.
  - Note that you need to run `python3 Rebinder.py` in a terminal each time before playing Minecraft.
