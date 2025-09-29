# Quickstart

To easily get started, simply type the following command to generate a sample configuration:

Most commands support a set of global flags that affect output and behavior.
See [Global Flags](./global-flags.md) for details.

```sh
cutler init
```

Once you run this command, you will get a copy of [this starter template](https://github.com/cutlerCLI/cutler/blob/master/examples/complete.toml) in the
configuration path. The path defaults to `$HOME/.config/cutler/config.toml` but can
be set anywhere within these locations:

- `$HOME/.config/cutler/config.toml`
- `$HOME/.config/cutler.toml`
- `$XDG_CONFIG_HOME/cutler/config.toml`
- `$XDG_CONFIG_HOME/cutler.toml`

cutler uses TOML "tables" to put everything together it does; from setting up system
preferences to running commands and more. So, the config file you just created will be the
center point of usage.

The template is filled to the brim with examples. It is suggested that you read it thoroughly
for getting a hold of the structure. It may seem more familiar if you're already experienced
with the format.
