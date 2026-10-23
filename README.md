# My dotfiles

Configure linux workstation using Ansible.

Terminal tools are mostly inspired by [ this article ](https://remysharp.com/2018/08/23/cli-improved).

### System

- [ fzf ](https://github.com/junegunn/fzf) - It's an interactive Unix filter for command-line that can be used with any list; files, command history, processes, hostnames, bookmarks, git commits, etc.
- [ fd ](https://github.com/sharkdp/fd) - fd is a program to find entries in your filesystem. It is a simple, fast and user-friendly alternative to find
- git
- [ oh-my-zsh ](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) - Oh-My-Zsh is a framework for Zsh, the Z shell

### Packages

- snap
  - VS code
  - spotify
- apt
  - redis 
  - [ ansible ](https://github.com/ansible/ansible)
  - build-essential
  - [ curl ](https://github.com/curl/curl) - Curl is a command-line tool for transferring data specified with URL syntax.
  - [ htop ](https://htop.dev/)
  - [ jq ](https://github.com/stedolan/jq) - is a lightweight and flexible command-line JSON processor
  - make
  - wget
  - zip
  - [ vim ](https://github.com/vim/vim)
  - [ xclip ](https://github.com/astrand/xclip) - xclip is a command line utility that is designed to run on any system with an
X11 implementation. It provides an interface to X selections ("the clipboard")
from the command line.
  - [ silversearcher-ag ](https://github.com/ggreer/the_silver_searcher) - A code searching tool similar to ack, with a focus on speed.
  - git-flow
  - [ gh ](https://cli.github.com/) - GitHub CLI, used by the `issues` and `url` git aliases
  - [ fd-find ](https://github.com/sharkdp/fd)
  - [ bat ](https://github.com/sharkdp/bat)
  - [ fastfetch ](https://github.com/fastfetch-cli/fastfetch) - system info (`sys-info` alias)
  - tree
  - tmux
- npm
    - [ tldr ](https://github.com/tldr-pages/tldr) - The tldr pages are a community effort to simplify man pages with practical examples.
- custom installation
    - [ diff-so-fancy ](https://github.com/so-fancy/diff-so-fancy) - strives to make your diffs human readable instead of machine readable. This helps improve code quality and helps you spot defects faster.

  # GUI
  - chromium-browser
  - [ regolith ](https://regolith-desktop.com/) - Regolith is a modern desktop environment designed to let you work faster by reducing unnecessary clutter and ceremony. Built on top of Ubuntu, GNOME, and i3.

### Regolith

Regolith itself is installed manually (see the [install guide](https://regolith-desktop.com/docs/using-regolith/install/)). The playbook only links the custom config, which targets Regolith 3:

- `roles/apt/files/Xresources` → `~/.config/regolith3/Xresources` (apply with `regolith-look refresh`)
- `roles/apt/files/config` → `~/.config/regolith3/i3/config.d/90_custom` (loaded after Regolith's default partials)

## Bootstrap

First setup installation run the dot-bootstrap command.

```
$ ./bin/dot-bootstrap
```

After that you can run any scripts defined in the `$DOTFILES_PATH/bin`

```
$ dot-bootstrap
```

To dry-run the script run or check syntax use
```
$ dot-bootstrap dry-run

$ dot-bootstrap syntax-check
```

### Ubuntu 25.10+ and sudo-rs

Ubuntu 25.10 replaced `sudo` with `sudo-rs`, and Ansible's sudo plugin doesn't recognise its password prompt ("Timed out waiting for become success"). Classic sudo is still installed as `/usr/bin/sudo.ws`, so `group_vars/local` sets `ansible_become_exe` to use it when it exists and plain `sudo` otherwise. Your system's default `sudo` is unchanged.