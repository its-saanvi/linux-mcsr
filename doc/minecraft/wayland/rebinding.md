# Search crafting setup using waywall

This section goes over creating a keyboard layout for search crafting using waywall and xkb, similar to using Microsoft Keyboard Layout Creator on Windows.

## Creating a layout

- First, create the `~/.config/xkb/symbols` directory by running `mkdir -p ~/.config/xkb/symbols`.
- Create a file in this directory `touch ~/.config/xkb/symbols/mc`, and open it in a text editor `nano ~/.config/xkb/symbols/mc`.
- Paste the following example layout into this file:

```xkb
default partial alphanumeric_keys
xkb_symbols "basic" {
    name[Group1] = "Minecraft";
 
    key <TLDE> { [ plus, plus ] }; // ~ > +
    key <AE01> { [ 8, 8 ] }; // 1 > 8
    key <AE02> { [ 4, 4 ] }; // 2 > 4
    key <AE03> { [ Armenian_nu, Armenian_NU ] }; // 3 > ն
    key <AE04> { [ Armenian_gim, Armenian_GIM ] }; // 4 > գ
    key <AE05> { [ Armenian_tche, Armenian_TCHE ] }; // 5 > ճ

    key <AD01> { [ Armenian_yech, Armenian_YECH ] }; // q > ե
    key <AD02> { [ Armenian_tyun, Armenian_TYUN ] }; // w > տ
    key <AD03> { [ Armenian_pe, Armenian_PE ] }; // e > պ
    key <AD04> { [ Armenian_se, Armenian_SE ] }; // r > ս

    key <CAPS> { [ Armenian_vo, Armenian_VO ] }; // capslock > ո
    key <AC01> { [ Armenian_re, Armenian_RE ] }; // a > ր
    key <AC02> { [ Armenian_vyun, Armenian_VYUN ] }; // s > ւ
    key <AC03> { [ Armenian_hi, Armenian_HI ] }; // d > յ
    key <AC04> { [ Armenian_cha, Armenian_CHA ] }; // f > չ

    key <AB01> { [ Armenian_ini, Armenian_INI ] }; // z > ի
    key <AB02> { [ Armenian_ayb, Armenian_AYB ] }; // x > ա
    key <AB03> { [ Armenian_ken, Armenian_KEN ] }; // c > կ
    key <AB04> { [ Armenian_za, Armenian_ZA ] }; // v > զ

    key <LALT> { [ Armenian_dza, Armenian_DZA ] }; // alt > ձ
};
```

- Let's break down how the layout file works.
- The comment code on the right (the text after the `//`) shows which key is being mapped to what character.

```xkb
key <AD03> { [ Armenian_pe, Armenian_PE ] }; // e > պ
```

- This line remaps lowercase `e` to the `պ` character, and uppercase `E` to the `Պ` character.
  - `key <AD03>` refers to the `e` key.
    - Most of the common keys remapped for search crafting (i.e. keys close to the WASD cluster) are listed here, you can add keys further on the right by simply copying the key before it and increasing the number accordingly.
  - `Armenian_pe` refers to the `պ` character.
  - `Armenian_PE` refers to the `Պ` character.
  - [Here is the list of valid names for characters](https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap).
    - To find the matching name, first try searching for the character in the list with Ctrl+F, otherwise find a proper name for the character and attempt to search for that instead (for the Armenian layout above, the [Wikipedia page for the Armenian alphabet](https://en.wikipedia.org/wiki/Armenian_alphabet#Alphabet) was especially useful).

## Using the layout in waywall

- After creating your layout, open your waywall config file in a text editor (`nano ~/.config/waywall/init.lua`).
- Go to the `config.input` table and edit the `layout` option to "mc".
<img width="194" height="63" alt="image" src="https://github.com/user-attachments/assets/7ee9c1e6-e56f-4d89-95cb-bd67170d39d5" />

- Essentially, the `~/.config/xkb/symbols` folder is checked for a file named "mc", and switches to that layout if it's found.
- If you want to have multiple layouts to swap between easily, copy your existing layout file in `~/.config/xkb/symbols` and give it a distinct name, then edit init.lua accordingly.
