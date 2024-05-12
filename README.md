# Config

## Fedora

### Dependencies

```zsh
sudo dnf install fzf fd-find the_silver_searcher ripgrep ctags
```

### Nerd Font (FiraCode)

```zsh
curl -L https://github.com/ryanoasis/nerd-fonts/releases/latest/download/FiraCode.tar.xz > ~/Downloads/FiraCode.tar.xz
mkdir -p ~/.local/share/fonts/FiraCode
tar -xJvf ~/Downloads/FiraCode.tar.xz -C ~/.local/share/fonts/FiraCode
rm ~/Downloads/FiraCode.tar.xz
```

### Starship

[Project Site](https://starship.rs/)

```zsh
mkdir -p ~/.local/bin
curl -sS https://starship.rs/install.sh | sh -s -- --bin-dir ~/.local/bin
starship preset bracketed-segments -o ~/.config/starship.toml
```

### ~/.zshrc

```zsh
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc

# ssh-agent
if [ -z "$SSH_AUTH_SOCK" ]; then
   # Check for a currently running instance of the agent
   RUNNING_AGENT="`ps -ax | grep 'ssh-agent -s' | grep -v grep | wc -l | tr -d '[:space:]'`"
   if [ "$RUNNING_AGENT" = "0" ]; then
        # Launch a new instance of the agent
        ssh-agent -s &> $HOME/.ssh/ssh-agent
   fi
   eval `cat $HOME/.ssh/ssh-agent`
fi

# alias
alias upgrade-all='sudo dnf upgrade -y && sudo dnf autoremove -y && flatpak update -y && flatpak uninstall --unused -y'

# brave
export CHROME_EXECUTABLE="/usr/bin/brave-browser"

# jetbrains
export PATH="$HOME/.local/share/JetBrains/Toolbox/scripts:$PATH"

# starship
eval "$(starship init zsh)"
```

### ~/.zshrc (VFIO NVIDIA GPU)

```zsh
...

alias nvidia-attach-host="sudo virsh nodedev-reattach pci_0000_01_00_0 && sudo virsh nodedev-reattach pci_0000_01_00_1 && sudo rmmod vfio_pci vfio_pci_core vfio_iommu_type1 && sudo modprobe -i nvidia_modeset nvidia_uvm nvidia"
alias nvidia-attach-vfio="sudo rmmod nvidia_modeset nvidia_uvm nvidia && sudo modprobe -i vfio_pci vfio_pci_core vfio_iommu_type1 && sudo virsh nodedev-detach pci_0000_01_00_0 && sudo virsh nodedev-detach pci_0000_01_00_1"
```

### ~/.fzf.zsh

```zsh
# Auto-completion
# ---------------
[ -f /usr/share/zsh/site-functions/fzf ] && source /usr/share/zsh/site-functions/fzf

# Key bindings
# ------------
[ -f /usr/share/fzf/shell/key-bindings.zsh ] && source /usr/share/fzf/shell/key-bindings.zsh
```

## OpenSUSE Tumbleweed (WSL)

### Dependencies

```zsh
sudo zypper install fzf fzf-zsh-completion fd fd-zsh-completion the_silver_searcher ripgrep ripgrep-zsh-completion ctags
```

### ~/.zshrc

```zsh
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc

# ssh-agent
if [ -z "$SSH_AUTH_SOCK" ]; then
   # Check for a currently running instance of the agent
   RUNNING_AGENT="`ps -ax | grep 'ssh-agent -s' | grep -v grep | wc -l | tr -d '[:space:]'`"
   if [ "$RUNNING_AGENT" = "0" ]; then
        # Launch a new instance of the agent
        ssh-agent -s &> $HOME/.ssh/ssh-agent
   fi
   eval `cat $HOME/.ssh/ssh-agent`
fi

# alias
alias upgrade-all='sudo zypper cc -a && sudo zypper ref && sudo zypper dup --allow-vendor-change && flatpak update -y && flatpak uninstall --unused -y'

# brave
export CHROME_EXECUTABLE="/usr/bin/brave-browser"

# gpg
export GPG_TTY=$(tty)
```

### ~/.fzf.zsh

```zsh
# Auto-completion
# ---------------
[ -f /usr/share/zsh/site-functions/_fzf ] && source /usr/share/zsh/site-functions/_fzf

# Key bindings
# ------------
[ -f /etc/zsh_completion.d/fzf-key-bindings ] && source /etc/zsh_completion.d/fzf-key-bindings
```

## MacOS (OUTDATED)

### Dependencies (recommended)

```zsh
brew install fzf fd the_silver_searcher ripgrep ctags
```

### ~/.zshrc

```zsh
[ -f "$HOME/.config/zsh/z-rc" ] && source $HOME/.config/zsh/z-rc

# brave
export CHROME_EXECUTABLE="/usr/bin/brave-browser"
```

### ~/.fzf.zsh

```zsh
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
