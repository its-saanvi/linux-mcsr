# Configuring Waywall

Waywall is configured in Lua, a lightweight and easy-to-learn scripting language. The config file for Waywall is located at the following path `~/.config/waywall/init.lua` by default. If you make any changes in your config file and wish to reload your config, simply save `init.lua` (This may not reload certain parts of your config; those may require restarting your Minecraft instance.).

## Using a premade config
If you are new to Lua or prefer to start with a ready-made configuration, Gore (@goreay_12 on Discord) has published two templates you can use immediately.

If you want to use a generic config Gore made with a bunch of features that you can customize out of the box, check this one out: [Waywall Generic Config](https://github.com/arjuncgore/waywall_generic_config). (Many users refer to this as the generic config or the Gore config.)

Otherwise, if you would prefer to use a basic config that you can build from, without anything fancy, consider this:
[Waywall Barebones Config](https://github.com/arjuncgore/waywall_barebones_config)

The community of speedrunners also publishes their own configuration files in `#configuration-showcase` in the Discord server. Feel free to check those out and ask any questions if you want to use any features from them.

## Profiles
You can also load a config from any other Lua file in `~/.config/waywall/` by using the `--profile` argument in the wrapper command. This can be used to have multiple configurations for different instances. For example, setting your wrapper command to `waywall wrap --profile ranked --` reads a config from `~/.config/waywall/ranked.lua`.

## Creating/Editing your config file
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
