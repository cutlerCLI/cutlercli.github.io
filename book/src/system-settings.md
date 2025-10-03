# Basics & System Settings

## Configuration Syntax

cutler can do a number of things if you use it right. Here's a basic example of a TOML configuration for cutler:

```toml
# ~/.config/cutler/config.toml

[set.dock]
tilesize = 46

[set.menuextra.clock]
FlashDateSeparators = true
```

macOS heavily relies on preference files (in `.plist` format) stored in certain ways to save the state of your Mac's apps and settings. cutler takes advantage of this mechanism to automatically put your desired system settings in place by following the config file you wrote. It's a "declarative" way to set your settings without even touching the app itself.

Ideally, the block above would look something like this if you were to manually call the `defaults` CLI tool which is used to modify these values on macOS:

```sh
$ defaults write com.apple.dock "tilesize" -int "46"
$ defaults write com.apple.menuextra.clock "FlashDateSeparators" -bool true
```

You can also configure global preferences like this:

```toml
# ~/.config/cutler/config.toml

[set.NSGlobalDomain]
InitialKeyRepeat = 15
ApplePressAndHoldEnabled = true
"com.apple.mouse.linear" = true

# or, for the third entry, alternate structure:
#
# [set.NSGlobalDomain.com.apple.mouse]
# linear = true
```

Again, if you were to use `defaults`, it would look something like this:

```sh
$ defaults write NSGlobalDomain "ApplePressAndHoldEnabled" -bool true
$ defaults write NSGlobalDomain com.apple.mouse.linear -bool true
```

## Applying & Undoing

Once you're ready, run this command to apply everything:

```sh
cutler apply
```

The `apply` command has multiple functionalities which happen alongside of applying the preferences. You may execute `cutler apply -h` or append the `--help` flag to see all the different options, or just read the cookbook.

To compare your system with your configuration and see what needs to be done, run:

```sh
cutler status
```

Unapplying everything is also as easy. Run the command below and cutler will restore your preferences to the exact previous state:

```sh
cutler unapply
```

## Action Hints

The fun part about using cutler is, it will mostly tell you to take certain actions based on what command you are using, without you having to think about it. This is due to cutler's immense synchronization between commands.

Say, for example, if my dock should automatically hide based on cutler's configuration, and if it does not right now, cutler will show this when running `cutler status`:

```sh
$ cutler status
WARN  com.apple.dock
WARN    autohide: should be true (now: false)
WARN  Preferences diverged. Run `cutler apply` to apply the config onto the system.
🍎 Homebrew status on sync.
$
```

As you can see, it suggests me to run `cutler apply`. Running the suggested command will only affect the changed portion of the preferences, and cutler will skip the rest.

## Risky Operations

If you would like to write non-existent domains (create them) using cutler, use the `--no-check` flag:

```sh
cutler apply --no-check
```

This will disable the "Domain does not exist" error which happens when cutler's backend does not recognize a domain.
