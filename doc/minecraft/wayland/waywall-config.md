# Configuring waywall

After setting up [waywall](waywall.html), you must create a configuration file to run it and use its features.

waywall is configured in Lua, a lightweight and easy-to-learn scripting language. The config file for waywall is located at the following path `~/.config/waywall/init.lua` by default. If you make any changes in your config file and wish to reload your config, simply save `init.lua`.
Note that certain parts of your config require restarting your Minecraft instance to take effect, i.e. shaders.

## Using a pre-made config

It is recommended to use a pre-made config, with window resizing and magnifiers set up for you. Here are two templates by Gore (@goreay_12 on Discord):

- If you want to use a generic config with a bunch of features that you can customize out of the box, check out the [generic config](https://github.com/arjuncgore/waywall_generic_config). (Many users refer to this as the generic config or the Gore config.)
- If you would prefer to use a basic config that you can build from without anything fancy, check out the [barebones config](https://github.com/arjuncgore/waywall_barebones_config).

The Linux MCSR community also publishes their own configuration files in `#configuration-showcase` in the [Discord server](https://discord.gg/fwZA2VJh7k). Feel free to check those out, and ask any questions in the `#public-help` channel.

## Creating/editing your config file

If you wish to create a config file from scratch, you should read the [documentation](https://tesselslate.github.io/waywall/01_basics.html) for information on the different options, functions, and API references.
You may create a file in `~/.config/waywall/init.lua` and use this as a starting point:

```lua
local waywall = require("waywall")
local helpers = require("waywall.helpers")

local config = {
    input = {
        layout = "us",
        repeat_rate = 40,
        repeat_delay = 300,

        sensitivity = 1.0,
        confine_pointer = false,
    },
    theme = {
        background = "#303030ff",
    },
}

config.actions = {}

return config
```

Note that the next section regarding boat eye setup is only practical if you resize Minecraft to a tall resolution, and use a mirror to magnify the game further.
Please see an existing config for pointers on how you can set this up manually.

## Profiles

You can also load a config from any other Lua file in `~/.config/waywall/` by using the `--profile` argument in the wrapper command. This can be used if you want multiple configs for different instances. For example, setting your wrapper command to `waywall wrap --profile ranked --` reads a config from `~/.config/waywall/ranked.lua`.

If your config is valid, and you properly followed the setup steps in the previous section, launching your instance should result in the window title being "waywall" instead of the usual "Minecraft":
![image](https://github.com/user-attachments/assets/50549c81-dbbe-460d-a164-d116aa168531)
