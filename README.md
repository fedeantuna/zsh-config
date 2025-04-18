# zsh config files

This configuration files are tested on Fedora 42. There are a few required (and recommended) dependencies for this setup.

## Dependencies

### Packages

```bash
sudo dnf install ctags fd-find fzf git jq ripgrep the_silver_searcher zsh
```

### Iosevka Font

**Site:** [https://typeof.net/Iosevka](https://typeof.net/Iosevka)

**Repo:** [https://github.com/be5invis/Iosevka](https://github.com/be5invis/Iosevka)

```bash
curl -L -o "$HOME/Downloads/Iosevka.zip" $(curl -s https://api.github.com/repos/be5invis/Iosevka/releases/latest | jq -r '.assets[] | select(.name | test("^SuperTTC-Iosevka-.*\\.zip$")) | .browser_download_url') && mkdir -p "$HOME/.local/share/fonts/Iosevka" && unzip "$HOME/Downloads/Iosevka.zip" -d "$HOME/.local/share/fonts/Iosevka" && rm "$HOME/Downloads/Iosevka.zip"
```

### Starship

**Site:** [https://starship.rs/](https://starship.rs/)

**Repo:** [https://github.com/starship/starship](https://github.com/starship/starship)

```bash
mkdir -p "$HOME/.local/bin" && curl -sS https://starship.rs/install.sh | sh -s -- --bin-dir "$HOME/.local/bin" && starship preset bracketed-segments -o "$HOME/.config/starship.toml"
```

## .zshrc

```zsh
# shellcheck shell=bash

# shellcheck source=/dev/null
[ -f "$HOME/.config/zsh/z-rc" ] && source "$HOME/.config/zsh/z-rc"

initialize_zsh_config

# starship
eval "$(starship init zsh)"

# fzf
try_add_path "/usr/share/zsh/site-functions/fzf"
try_add_path "/usr/share/fzf/shell/key-bindings.zsh"

# alias
alias upgrade-all='sudo dnf upgrade -y && sudo dnf autoremove -y && flatpak update -y && flatpak uninstall --unused -y && rustup update && update_all_zsh_plugins'

# brave
overwrite_chrome_executable "/usr/bin/brave-browser"

# rust
try_add_path "$HOME/.cargo/env"

# fnm
if try_add_path "$HOME/.local/share/fnm"; then
  eval "$(fnm env)"
fi

# jetbrains
try_add_path "$HOME/.local/share/JetBrains/Toolbox/apps"
try_add_path "$HOME/.local/share/JetBrains/Toolbox/scripts"
```

