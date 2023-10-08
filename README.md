# Config

All my systems have fnm (https://github.com/Schniz/fnm) and pyenv (https://github.com/pyenv/pyenv) installed. For the shell prompt I use Oh My Posh (https://ohmyposh.dev/) with Mistro theme (https://gist.github.com/fedeantuna/d89fbeac16b3227fc53cc30c9539607f)

## Fedora

### Dependencies (recommended)

```
sudo dnf install fzf fd-find the_silver_searcher ripgrep ctags
```

### ~/.zshrc

```
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc

# alias
alias upgrade-all='sudo dnf upgrade -y && sudo dnf autoremove -y && curl -fsSL https://fnm.vercel.app/install | bash -s -- --skip-shell && pyenv update && flatpak update -y && flatpak uninstall --unused -y'

# fnm
export PATH="$HOME/.local/share/fnm:$PATH"
eval "`fnm env`"

# pyenv
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

# oh-my-posh
eval "$(oh-my-posh init zsh --config $HOME/.posh_themes/custom/mistro.omp.json)"

# jetbrains
export PATH="$HOME/.local/share/JetBrains/Toolbox/scripts:$PATH"
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

## OpenSUSE Tumbleweed (WSL)

### Dependencies

```
sudo zypper install fzf fzf-zsh-completion fd fd-zsh-completion the_silver_searcher ripgrep ripgrep-zsh-completion ctags
```

### ~/.zshrc

```
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc

# alias
alias upgrade-all='sudo zypper cc -a && sudo zypper ref && sudo zypper dup --allow-vendor-change && curl -fsSL https://fnm.vercel.app/install | bash -s -- --skip-shell && pyenv update'

# fnm
export PATH="$HOME/.local/share/fnm:$PATH"
eval "`fnm env`"

# pyenv
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

# oh-my-posh
eval "$(oh-my-posh init zsh --config $HOME/.posh_themes/custom/mistro.omp.json)"

# gpg
export GPG_TTY=$(tty)
```

### ~/.fzf.zsh

```
# Auto-completion
# ---------------
[ -f /usr/share/zsh/site-functions/_fzf ] && source /usr/share/zsh/site-functions/_fzf

# Key bindings
# ------------
[ -f /etc/zsh_completion.d/fzf-key-bindings ] && source /etc/zsh_completion.d/fzf-key-bindings
```

## MacOS (OUTDATED)

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
