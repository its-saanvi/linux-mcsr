# OBS

- This section goes over installing and setting up OBS on your system.
- Open up a terminal and type in this command:

```bash
sudo dnf install obs-studio
```

- This should download and install OBS on your system.
- After downloading and installing it, you can open it and set it up as per usual.
  - On Wayland, you can capture specific windows or displays with the **Screen Capture (PipeWire)** source.
  - On X11, use the **Window Capture (Xcomposite)** source.
    - If you plan on using window resizing scripts on X11, it is recommended to set your Minecraft capture source to be centered. After adding Minecraft, select it and press Ctrl+E to open the transform settings - here, click "Reset", then set "Positional Alignment" to "Center". Finally, close the transform settings and press Ctrl+D.
- If you are using classic wall (i.e. multi-instancing on versions without SeedQueue), you might want to look at [these](https://github.com/tesselslate/resetti/blob/legacy-wall/doc/obs.md) docs to setup OBS to work with resetti.

## Splitting audio

- Read ahead to set up audio splitting (useful for removing music from your Twitch VODs to avoid copyright, or only capturing game audio in your recordings).
- As of right now, OBS on Linux does not support application-specific audio capture out of the box - we instead use an OBS plugin to achieve this.
- Download and install the plugin using the instructions [here](https://github.com/dimtpap/obs-pipewire-audio-capture?tab=readme-ov-file#installation).
- After installing the plugin and restarting OBS, check the list of sources. You should see the "Application Audio Capture (PipeWire)" source at the top - after adding it, select the app to capture audio from in the Applications dropdown.
- Make sure to mute/disable desktop audio afterwards.
