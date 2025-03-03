---
id: fish
aliases: []
tags: []
---

# How to install and use Fish shell

- Friendly Interactive SHell

## Install

See what shell you're currently using

```sh
echo $0
```

Install using `Pacman`

```sh
sudo pacman -Sy fish
```

Check version

```sh
fish -v
```

Check path of fish shell with `which` command

and change the shell to fish

```sh
chsh -s /use/bin/fish
```

Now log out by pressing `Super + M` and log back in to apply changes

To turn off the welcome phrase by fish

open `~/.config/fish/config.fish` with editor of you choice and add the following code

- tl;dr
  - -g is for global range is current session
  - -U is for Universal range across all session

```sh
set -U fish_greeting
```

## Creating aliases

To create it run the following command at the terminal

```sh
alias --save {alias-name}="{command-to-run}"
```

which will create a file under `~/.config/fish/functions` that contains function for alias

### Separate file

Or create aliases.fish under `~/.config/fish`
then create a alias like this

```sh
alias {alias-name}="{command-to-run}"
```

Finally add the following line of code to source the `aliases.fish` when the `config.fish` is sourced

- In `~/.config/fish/functions/`

```sh
source ~/.config/fish/aliases.fish
```

-- Create a fish function to mkdir, touch and open it with nvim

`~/.config/fish/functions/mkdtn.fish`

```sh
function mkdtn
    mkdir -p $argv[1] && touch $argv[1]/$argv[2] && nvim $argv[1]/$argv[2]
end
```

Restart to take effect function

```sh
funcsave mkdtn
```

- Usage

```sh
mkdfn {path-and-dir-to-create} {name-of-file}
```

---

#### bat

- better version of cat
- file preview

```sh
sudo pacman -S bat
```

---

#### Sessionizer

- Dependency: Fzf

Copy the bash script from the github repo
and change the directories inside

- [github.com/tmux-sessionizer](https://github.com/edr3x/tmux-sessionizer)

Create directory, file and then open it with nvim

```sh
mkdir -p ~/.local/scripts/ && touch ~/.local/scripts/tmux-sessionizer && nvim ~/.local/scripts/tmux-sessionizer
```

Add PATH and macro inside config.fish file

```sh
set PATH "$PATH":"$HOME/.local/scripts/"

bind \cf "tmux-sessionizer"
```

and for .tmux.conf

```sh
bind-key -r f run-shell "tmux neww ~/.local/scripts/tmux-sessionizer"
```

Finally give tmux-sessionizer script a execution permission

```sh
chmod +x ~/.local/scripts/tmux-sessionizer
```

Additionally if you add the following script to `.tmux.conf`
you can open desired path without using the fzf with `prefix` + k

```sh
bind-key -r k run-shell "~/.local/scripts/tmux-sessionizer {path-to-desired-directory}"
```

---

### Happy Hacking 🎉
