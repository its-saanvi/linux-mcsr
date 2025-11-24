# Configuring waywall

waywall is configured in lua, a lightweight and easy-to-learn scripting language. The config file for waywall is located at the following path `~/.config/waywall/init.lua` by default. If you make any changes in your config file and wish to reload your config, simply save `init.lua` (This may not work for reloading certain parts of your config, which may require a restart of your minecraft instance to reload).

## Profiles
You can also load a config from any other lua file in `~/.config/waywall/` by using the `--profile` argument in the wrapper command. This can be used to have multiple configurations for different instances. For example, setting your wrapper command to `waywall wrap --profile ranked --` reads a config from `~/.config/waywall/ranked.lua`.

## Creating/Editing your config file
If you wish to create a config file from scratch, you should read documentation for information of the different options, functions, and API references.
You may create file in `~/.config/waywall/init.lua` and use this as a starting point:
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

## Using a premade config
If you don't know how to program or just want to get started right away, Gore (@goreay_12 on discord) made a couple waywall configurations for new users to setup and start running with immediately.

If you want to use a generic config Gore made with a bunch of features that you can customize out of the box, check this one out:
https://github.com/arjuncgore/waywall_generic_config

Otherwise, if you would prefer to use a basic config that you can build from, without anything fancy, consider this:
https://github.com/arjuncgore/waywall_barebones_config.

The community of speedrunners also publish their own configuration files in `#configuration-showcase` in the discord server. Feel free to check those out and ask any questions if you want to use any features from them.