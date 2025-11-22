# File permissions

File permissions in a UNIX system are distributed per user.

The only permission we really care about is the executable flag.
This flag tells the operating system that it can execute that file as a binary.

To set the executable flag on a file we use the `chmod` command.

```bash
touch bin
chmod +x bin
```

- Now edit the contents of `bin` with

```bash
nano bin
```

- Add these contents in it

```bash
#!/bin/bash
echo "Hello World"
```

- Here the echo command is used to print out text to the console.
- To execute this script, we use this command

```bash
./bin
```

- You would see the console output `Hello World`.
- There are other permissions too, but we mostly use `chmod +x` to set the executable flag on files.
- We can also remove the executable flag from a file by using `chmod -x`.

```
chmod -x bin
```

# Clearing out worlds

- Now that we know much about the Linux terminal, we can now make scripts to automate our filesystem tasks.
- We can declare variables in scripts using the syntax:

```bash
<variable_name>=<value>
```

- Here is a script to clear out saves in all your instances.

```bash
#!/bin/bash
instances=("Ranked" "SeedQueue" "Practice")
# DO NOT add a '/' at the end of launcher_prefix's value
launcher_prefix=~/.local/share/PrismLauncher/instances
for inst in ${instances[@]};
do
    rm -r $launcher_prefix/$inst/saves/Random*
    rm -r $launcher_prefix/$inst/saves/New*
done
```

- We use a list called `instances` to list the names of some instances we might have in Prism Launcher.
- Here in the `rm` commands, we use shorthand representation to expand every folder starting with `Random` and `New` in its name. Its matches would include names like `Random Speedrun #12345`, `New World (32)`, and so on.
- We also use `for` to loop over every instance and delete every matching world folder.

# Going ahead

We are now proficient with the Linux terminal and bash scripting!
