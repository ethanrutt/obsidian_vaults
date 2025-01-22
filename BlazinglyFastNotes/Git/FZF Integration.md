
# Ref
- copied from [fzf-git.sh](https://github.com/junegunn/fzf-git.sh)
# List of bindings

- `C-g C-f` for \[F\]iles
- `C-g C-b` for \[B\]ranches
- `C-g C-t` for \[T\]ags
- `C-g C-r` for \[R\]emotes
- `C-g C-h` for commit \[H\]ashes
- `C-g C-s` for \[S\]tashes
- `C-g C-l` for ref\[L\]ogs
- `C-g C-w` for \[W\]orktrees
- `C-g C-e` for \[E\]ref (`git for-each-ref`)


> [!WARNING] Warning
> You may have issues with these bindings in the following cases:
> 	- `C-b` is tmux prefix
> 	- flow control is enabled. This means that doing `C-s` will freeze the terminal. It is    recommended to add `stty -ixon` to your `.bashrc` to prevent this, or just run in your terminal session to disable.
> 	- To work around, you can also use `C-g <key>` instead of `C-g C-<key>`


## Inside fzf

- `Tab`  or `Shift-Tab` to select multiple objects
- `C-/` to change preview window layout
- `C-o` to open object in the web browser (github url scheme)

# Customization

-  Redefine this function to change the options
```sh
_fzf_git_fzf() {
  fzf --height=50% --tmux 90%,70% \
    --layout=reverse --multi --min-height=20 --border \
    --border-label-pos=2 \
    --color='header:italic:underline,label:blue' \
    --preview-window='right,50%,border-left' \
    --bind='ctrl-/:change-preview-window(down,50%,border-top|hidden|)' "$@"
}
```

## Defining shortcut commands

- Each binding is backed by _fzf_git_* function so you can do something like this in your shell configuration file.

```sh
gco() {
  _fzf_git_each_ref --no-multi | xargs git checkout
}
```

```sh
gswt() {
  cd "$(_fzf_git_worktrees --no-multi)"
}
```

# Environment Variables

| Variable                | Description                                              | Default                                         |
| ----------------------- | -------------------------------------------------------- | ----------------------------------------------- |
| `BAT_STYLE`             | Specifies the style for displaying files using `bat`     | `full`                                          |
| `FZF_GIT_CAT`           | Defines the preview command used for displaying the file | `bat --style=$BAT_STYLE --color=$FZF_GIT_COLOR` |
| `FZF_GIT_COLOR`         | Set to `never` to suppress colors in the list            | `always`                                        |
| `FZF_GIT_PAGER`         | Specifies the pager command for the preview window       | `$(git config --get core.pager)`                |
| `FZF_GIT_PREVIEW_COLOR` | Set to `never` to suppress colors in the preview window  | `always`                                        |
