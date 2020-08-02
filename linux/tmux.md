# tmux - Terminal Multiplexer

## Run tmux

Run your terminal emulator with `<terminal> -e tmux` to autostart tmux

| Command                             	| Description                 	|
|-------------------------------------	|-----------------------------	|
| `tmux new -s myname`                	| start new with session name 	|
| `tmux a  #`  (or `at`, or `attach`) 	| attach                      	|
| `tmux a -t myname`                  	| attach to named             	|
| `tmux ls`                           	| list sessions               	|

## Session

| Command                  | Description                       |
|--------------------------|-----------------------------------|
| rename current session   | `$`                               |
| kill session by name     | `:kill-session -t <session-name>` |

## Window

| Command         | Description |
|-----------------|-------------|
| create window   | `c`         |
| list windows    | `w`         |
| next window     | `n`         |
| previous window | `p`         |
| find window     | `f`         |
| name window     | `,`         |
| kill window     | `&`         |

## Panes (splits)

| Command                             | Description |
|-------------------------------------|-------------|
| vertical split                      | `%`         |
| horizontal split                    | `"`         |
| Resize pane in direction of <arrow> | `C-<arrow>` |
| swap panes                          | `o`         |
| show pane numbers                   | `q`         |
| kill pane                           | `x`         |
| restore pane from window            | `-`         |
| space - toggle between layouts      | ` `         |
| Move the current pane left          | `{`         |
| Move the current pane right         | `}`         |
| toggle pane zoom                    | `z`         |

## Copy mode

To start `copy mode` press `<pfx> [`.
Move around the buffer using vim controls or arrow keys.
To start selection press `<space>` and copy with `<enter>`.
You can toggle block visual mode by pressing `C-v`.


## Mouse

You can use the mouse to move or scale panes.
Hold `<shift>` key to enable regular mouse usage like select-to-copy and paste.

## References

- [A guide to customizing your tmux conf/](https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf)
- [Navigate terminal output like a text file with vim keybinding](https://superuser.com/questions/1294618/how-can-i-navigate-terminal-output-like-a-text-file-with-vim-keybinding)
- [vi mode in tmux](https://sanctum.geek.nz/arabesque/vi-mode-in-tmux)
- [tmux themepack](https://github.com/jimeh/tmux-themepack)
- [vim+tmux navigation](https://github.com/christoomey/vim-tmux-navigato)
