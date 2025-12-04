# Drag clicking

- By default, drag clicking will not work on Linux - it is set to ignore multiple successive fast clicks (similar to high debounce time).
- To fix this:
  - Create the configuration folder for `libinput`, which handles mouse input: `sudo mkdir -p /etc/libinput`.
  - Create a config file in this folder: `sudo touch /etc/libinput/local-overrides.quirks`.
  - Open this file in a text editor: `sudo nano /etc/libinput/local-overrides.quirks`.
  - Paste the following content and save the file:

```bash
[Never Debounce]
MatchUdevType=mouse
ModelBouncingKeys=1
```

- Finally, restart your system to bring the new config into effect.
