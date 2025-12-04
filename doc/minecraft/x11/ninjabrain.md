# Ninjabrain Bot

- This section goes over installing Ninjabrain Bot on X11 and creating a **desktop entry** for it, so you can easily open it from the start menu/your app launcher.
  - On Wayland, please instead run Ninjabrain Bot through [waywall](../wayland/waywall.html) - this is done with the example config provided.
- Download the .jar for Ninjabrain Bot as per usual from [here](https://github.com/Ninjabrain1/Ninjabrain-Bot/releases/latest).
- **NOTE:** [NBTrackr](https://github.com/qMaxXen/NBTrackr?tab=readme-ov-file#installation) can be used to see Ninjabrain Bot information easily, especially for single-monitor users.
- To add it as an application to your list of applications, ensure the applications folder exists by running the following command:

```bash
mkdir -p ~/.local/share/applications/
```

- Then, create this file with the following contents under `~/.local/share/applications/NinjabrainBot.desktop`, replacing `<path/to/Ninjabrain-Bot-1.5.1.jar>` with the actual path to Ninjabrain Bot on your system.

```bash
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=NinjabrainBot
Icon=minecraft
Exec=java -jar <path/to/Ninjabrain-Bot-1.5.1.jar>
```

- Now you can launch Ninjabrain Bot from your applications menu! Note that if you move the Ninjabrain Bot .jar file, you will have to edit this file as well.
