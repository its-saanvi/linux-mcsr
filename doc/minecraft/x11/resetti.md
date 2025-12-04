# resetti

- **resetti** is an X11 app mainly used for **resizing the Minecraft window**.
  - If you're using **Wayland**, please use [waywall](../wayland/waywall.html) instead.
- Go to [this](https://github.com/tesselslate/resetti/releases/latest) link to download the latest version of resetti.
  - On Fedora, download and run the `.rpm` file to install resetti. Once installed, check that it's working by opening a terminal and running `resetti version`.
  - If you are unsure what to download, simply pick the binary file (just named "resetti"). Once downloaded, check that it's working by opening a terminal and running `<path/to/resetti> version`, replacing <path/to/resetti> with the path to the resetti binary file you just downloaded. Run the following commands using the binary path as well.
- Run `resetti new <profile_name>` to create a new config, replacing the `<profile_name>` with a name for the config.
  Eg: `resetti new seedqueue1`.
- Go to `~/.config/resetti` to find your config files, and open the one you've created with a text editor (done in the terminal with `nano ~/.config/resetti/<profile_name>.toml`). Here, you can add custom resolutions and hotkeys to toggle them.
- Hooks are essentially terminal commands that run when pressing one of your resetti hotkeys. Further information regarding hooks and the resetti config can be found [here](https://github.com/tesselslate/resetti/blob/main/doc/configuration.md).
- You can now run resetti with `resetti <profile_name>` in a terminal to run the macro :D.
- **Some things to note:**
  - Resizing will only work if the game is **unfullscreened** (as mentioned earlier, windowed/borderless will perform the same as fullscreen - on Plasma, you can make a window borderless by pressing Alt+F3 and disabling window borders).
  - Quirks with out of bounds resizing are addressed in the [Boat Eye for X11](boat-eye.html) section.

## Using classic wall with resetti

- If you would like to run resetti with its Wall features still, you can look [here](https://github.com/tesselslate/resetti/releases/tag/v0.6.1) to download the binary for the last stable wall release of resetti.
- After downloading, do the same steps as listed above under the `Using SeedQueue with resetti` section.
- On top of the options listed in the above section, you must also perform more additional setup as listed [here](https://github.com/tesselslate/resetti/blob/main/doc/README.md).
