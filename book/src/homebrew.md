# Homebrew Backups

If you're a person who struggles to keep tabs on all the installed formulae or apps using [Homebrew](https://brew.sh), then cutler could be a great choice for you!

You can back up your formula/cask names into your existng config file (or a new one), using this command:

```bash
cutler brew backup

# or, only backup the ones which are not a dependency:
#
# cutler brew backup --no-deps
```

Now, when you want to install from the file, simply run:

```bash
cutler brew install
```

You can also invoke the command's functionalty from within `cutler apply`:

```bash
cutler apply --with-brew
```

This will install every formula/cask _alongside_ applying preferences and running external commands.

The structure of the `brew` table inside cutler's configuration is like such:

```toml
# ~/.config/cutler/config.toml

[brew]
taps = ["hitblast/tap"]
casks = ["zed", "zulu@21", "android-studio"]
formulae = ["rust", "python3"]

# Ensure dependencies aren't accounted for.
# This is auto-set if --no-deps is used in `brew backup`.
no_deps = true
```

While running this command, cutler will also notify you about any extra software which is untracked by it. Then, you can run `cutler brew backup` again to sync.

## Backend Prerequisites

Obviously, running Homebrew on a Mac requires the **Xcode Command-Line Tools** to be installed, let it be through Xcode itself or through
the preincluded utility in macOS. By default, cutler will try to ensure that it is there, before executing any of the subprocesses.

If you want to manually install it, you can do so by running:

```bash
xcode-select --install
```
