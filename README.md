# .zshrc on ~/

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
