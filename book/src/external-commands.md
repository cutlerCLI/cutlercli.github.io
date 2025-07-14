# External Commands

Running commands to spring up your environment is essential for any workflow. Luckily, cutler is made with most scenarios in mind, given that most people usually set their dotfiles up with shell scripts which require manual execution and intervention.

You can define external commands with simple syntax like this:

```toml
# ~/.config/cutler/config.toml

[command.greet]
run = "echo Hello World"

# This runs:
# echo Hello World
```

## Ideal Structure

```toml
# ~/.config/cutler/config.toml

[vars]
hostname = "darkstar"

[command.hostname]
run = """
#!/usr/bin/env bash
scutil --set LocalHostName $hostname
scutil --set HostName $hostname
scutil --set ComputerName $hostname
"""
sudo = true  # a more "annotated" sudo
```

## Notable Features

Some people would like to run their commands "before" other commands. But, cutler runs all commands in parallel, which might not be what you want. In that case, you can use the `ensure_first` key to run then in your desired serial. You can apply this to multiple commands.

```toml
# ~/.config/cutler/config.toml

[command.dotfiles]
run = "git clone repo && cd repo && stow . -t ~"
ensure_first = true
```

You may also want to "ensure" certain binaries/programs in `$PATH` before running them. You can do so with the `required` field, like this:

```toml
[command.dev-env]
run = "mise install && mise up"
required = ["mise"]  # won't run if mise is not in $PATH
```

## Running the Commands

External commands are run whenever you run `cutler apply` by default. However, if you'd like to _only_ run the commands and not apply defaults, run:

```bash
cutler exec
```

You can also run a specific external command by attaching a name parameter:

```bash
$ cutler exec hostname  # this runs the hostname command
```
