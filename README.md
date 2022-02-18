# Config

The content of this repository goes into ~/.config/zsh/.zshrc

## Fedora

```
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc

export EDITOR="nvim"
export TERMINAL="alacritty"
export BROWSER="brave"

# fnm
export PATH=$HOME/.fnm:$PATH
eval "`fnm env`"

# pyenv
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"
```

## Debian (WSL)

```
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc

export EDITOR="nvim"

# fnm
export PATH=$HOME/.fnm:$PATH
eval "`fnm env`"

# pyenv
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"

export GPG_TTY=$(tty)
```

## MacOS

```
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc
```
