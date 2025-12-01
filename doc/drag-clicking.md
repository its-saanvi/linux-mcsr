# Drag clicking

- By default, drag clicking will not work on Linux - it is set to ignore multiple successive fast clicks (similar to high debounce time).
- To fix this, create a file with this content:

```bash
#!/bin/sh

sudo mkdir -p /etc/libinput
sudo tee /etc/libinput/local-overrides.quirks >/dev/null <<ENDHERE
[Never Debounce]
MatchUdevType=mouse
ModelBouncingKeys=1
ENDHERE
```

- Then, use `chmod +x <path/to/file>` to make the file executable (replace `<path/to/file>` with the actual path to the file).
- Finally, execute the file by typing the file path in the terminal, and restart your system.
