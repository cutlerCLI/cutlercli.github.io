# Shell Integrations

## Completions

cutler supports built-in shell completion for your ease of access for a variety of system shells, including
`bash`, `zsh`, `powershell`, etc. Below you will find instructions for each of them.

> If you have installed cutler using Homebrew, the shell completion will automatically be
> installed. Just restart your shell after initial installation.


## Direct init

Use these commands to enable completions for your current shell session only. This is useful for temporary usage or testing.

<details>
<summary>Bash</summary>

```bash
eval "$(cutler completion bash)"
```
</details>

<details>
<summary>Zsh</summary>

```zsh
autoload -U compinit && compinit
eval "$(cutler completion zsh)"
```
</details>

<details>
<summary>Fish</summary>

```fish
cutler completion fish | source
```
</details>

<details>
<summary>Elvish</summary>

```elvish
eval (cutler completion elvish)
```
</details>

<details>
<summary>PowerShell</summary>

```powershell
cutler completion powershell | Invoke-Expression
```
</details>

## Persistent Completions

To enable completions automatically for every new shell session, follow the steps below for your shell.

<details>
<summary>Bash</summary>

Add the following line to your `~/.bashrc` or `~/.bash_profile`:

```bash
eval "$(cutler completion bash)"
```
Then restart your shell or run:
```bash
source ~/.bashrc
```
</details>

<details>
<summary>Zsh</summary>

1. Create a directory for custom completions (if it doesn't exist):

    ```sh
    mkdir -p ~/.zfunc
    ```

2. Generate the completion script and move it:

    ```sh
    cutler completion zsh > ~/.zfunc/_cutler
    ```

3. Add the following to your `~/.zshrc`:

    ```sh
    fpath=(~/.zfunc $fpath)
    autoload -U compinit && compinit
    ```

4. Restart your shell or run:

    ```sh
    source ~/.zshrc
    ```
</details>

<details>
<summary>Fish</summary>

Add the completion script to your fish configuration directory:

```fish
cutler completion fish > ~/.config/fish/completions/cutler.fish
```
Restart your shell or open a new fish session.
</details>

<details>
<summary>Elvish</summary>

Add the following to your Elvish configuration file (usually `~/.elvish/rc.elv`):

```elvish
eval (cutler completion elvish)
```
Restart your shell or source your config file.
</details>

<details>
<summary>PowerShell</summary>

Add the following to your PowerShell profile (you can find your profile path with `$PROFILE`):

```powershell
cutler completion powershell | Out-String | Invoke-Expression
```
Restart your shell or run:

```powershell
. $PROFILE
```
</details>
