# Config

All my systems have fnm (https://github.com/Schniz/fnm) and pyenv (https://github.com/pyenv/pyenv) installed

## Fedora

### Dependencies (recommended)

```
sudo dnf install fzf fd-find the_silver_searcher ripgrep ctags
```

### ~/.zshrc

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

### ~/.fzf.zsh

```
# Auto-completion
# ---------------
[ -f /usr/share/zsh/site-functions/fzf ] && source /usr/share/zsh/site-functions/fzf

# Key bindings
# ------------
[ -f /usr/share/fzf/shell/key-bindings.zsh ] && source /usr/share/fzf/shell/key-bindings.zsh
```

## Debian 9 (WSL)

### Dependencies

```
sudo apt install silversearcher-ag exuberant-ctags

```

For fzf, follow https://github.com/junegunn/fzf#using-git
For ripgrep, follow https://github.com/BurntSushi/ripgrep#installation
For fd-find, follow https://github.com/sharkdp/fd#installation

### ~/.zshrc

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

# gpg
export GPG_TTY=$(tty)
```

### ~/.fzf.zsh

```
# Setup fzf
# ---------
if [[ ! "$PATH" == *$HOME/.fzf/bin* ]]; then
    export PATH="${PATH:+${PATH}:}$HOME/.fzf/bin"
fi

# Auto-completion
# ---------------
[[ $- == *i* ]] && source "$HOME/.fzf/shell/completion.zsh" 2> /dev/null

# Key bindings
# ------------
source "$HOME/.fzf/shell/key-bindings.zsh"
```

## MacOS

### Dependencies (recommended)

```
brew install fzf fd the_silver_searcher ripgrep ctags
```

### ~/.zshrc

```
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc

export EDITOR="nvim"
```

### ~/.fzf.zsh

```
# Setup fzf
# ---------
if [[ ! "$PATH" == */opt/homebrew/opt/fzf/bin* ]]; then
    export PATH="${PATH:+${PATH}:}/opt/homebrew/opt/fzf/bin"
fi

# Auto-completion
# ---------------
[[ $- == *i* ]] && source "/opt/homebrew/opt/fzf/shell/completion.zsh" 2> /dev/null

# Key bindings
# ------------
source "/opt/homebrew/opt/fzf/shell/key-bindings.zsh"
```
