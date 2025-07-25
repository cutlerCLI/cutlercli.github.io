# Remote Sync

cutler features a simple built-in remote sync logic. For example, if you want to apply a config from a given URL without placing it manually on your machine, simply use the following command:

```bash
cutler apply --url https://example.com/config.toml
```

cutler will then download and validate the config file, and if all looks good, it will be loaded to be applied.

You can also use this functionality on your "existing" configurations, by utilizing the `[remote]` table:

```toml
[remote]
url = "https://example.com/config.toml"
autosync = true
```

Here, the `autosync` flag will ensure that the next time you run any command except the [disabled commands](#disabled-commands), it will automatically fetch the config file beforehand from the provided remote.

Or, you can simply fetch from the config URL written in `[remote]` manually using the `fetch` command:

```bash
cutler fetch
```

In order to disable remote sync behavior while running any command, use the `--no-sync` global flag:

```bash
cutler status --no-sync
```

## Caveats

Important know-hows related to remote sync:

- If, for some reason, the remote config does not have a `[remote]` section, cutler will keep the current `[remote]` from the local config file and merge it into the remote configuration.

## Disabled Commands

Some commands will not respect `autosync = true` and therefore NOT synchronize the config automatically:

- `fetch`
- `self-update`
- `check-update`
- `init`
- `completion`
- `reset`
- the `config` group of subcommands
