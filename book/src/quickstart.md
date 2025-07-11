# Quickstart

To easily get started, simply type the following command to generate a sample configuration:

Most commands support a set of global flags that affect output and behavior.
See [Global Flags](./global-flags.md) for details.

```bash
cutler init
```

By default, cutler stores your configuration in `~/.config/cutler/config.toml`.
But, it can also have other values depending on your setup:

- `$HOME/.config/cutler/config.toml`
- `$HOME/.config/cutler.toml`
- `cutler.toml` in the current directory

It respects your `$XDG_CONFIG_HOME`, so you don't have to worry about path issues.

The next section will describe how you can use this one configuration file to orchestrate between
or use all of cutler's capabilities.
