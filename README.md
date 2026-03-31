# config_installer

Clone your Debian desktop + terminal setup onto a fresh machine.

Packs and installs: **Zsh** (Oh My Zsh + Powerlevel10k), **Micro** editor (Dracula theme), **Fastfetch**, modern CLI tools (lsd, bat, fd, ranger, fzf, zoxide, thefuck), **XFCE4** desktop config (panels, shortcuts, window manager), GTK themes, icon packs, cursors, fonts, LightDM greeter, APT sources/keys, sudoers, sysctl, and wallpapers.

## Quick start

### One-liner download

```bash
curl -fsSL https://raw.githubusercontent.com/ilPez00/config_installer/master/get | bash
```

This downloads the repo to `~/config_installer` and tells you what to do next.

### Full workflow

**On your machine** (source):
```bash
git clone https://github.com/ilPez00/config_installer.git
cd config_installer
bash pack_configs
```

**Copy to USB** (or any transfer method):
```bash
cp -r . /media/your-drive/config_installer/
```

**On the target machine**:
```bash
cd /media/.../config_installer
bash install_configs
```

Or if both machines have internet, transfer configs directly without USB:
```bash
# Source machine: pack and push configs to a private place
bash pack_configs
tar czf configs.tar.gz configs/
# Transfer configs.tar.gz to target via scp, cloud, etc.

# Target machine:
curl -fsSL https://raw.githubusercontent.com/ilPez00/config_installer/master/get | bash
cd ~/config_installer
# Place your configs.tar.gz here, then:
tar xzf configs.tar.gz
bash install_configs
```

## What gets packed

| Category | Source | Details |
|---|---|---|
| Shell | `~/.zshrc`, `~/.p10k.zsh`, `~/.bashrc` | Aliases, functions, prompt config |
| Editor | `~/.config/micro/` | Settings, keybindings, colorscheme |
| Fastfetch | `~/.config/fastfetch/` | System info display layout |
| XFCE4 | `~/.config/xfce4/` | Panels, keyboard shortcuts, window manager, desktop |
| Thunar | `~/.config/Thunar/` | File manager preferences |
| Autostart | `~/.config/autostart/` | Startup applications |
| GTK | `~/.config/gtk-3.0/`, `gtk-4.0/` | Theme, font, icon settings |
| Themes | `~/.themes/` | GTK themes (directories only, skips .tar.xz) |
| Icons | `~/.icons/`, `~/.local/share/icons/` | Icon packs, cursors |
| Fonts | `~/.local/share/fonts/` | User-installed fonts |
| LightDM | `/etc/lightdm/` | Display manager greeter config |
| APT sources | `/etc/apt/sources.list`, `sources.list.d/` | Repositories, mirrors, preferences |
| APT keys | `/etc/apt/trusted.gpg.d/`, `/usr/share/keyrings/` | GPG keys for repos |
| Package list | `apt-mark showmanual` | Reference list of manually installed packages |
| Sudoers | `/etc/sudoers.d/` | Custom sudo rules (syntax-checked before install) |
| Sysctl | `/etc/sysctl.conf`, `/etc/sysctl.d/` | Kernel parameters |
| Environment | `/etc/environment`, `/etc/profile`, `/etc/profile.d/` | System-wide env vars and shell configs |
| Systemd | `~/.config/systemd/user/` | User-level systemd units |
| Wallpapers | `~/Pictures/Wallpapers/` | Up to 20 images |
| Git | `~/.gitconfig` | Git settings (remember to update name/email!) |

## Packages installed

`git` `curl` `wget` `unzip` `rsync` `zsh` `zsh-autosuggestions` `zsh-syntax-highlighting` `micro` `fastfetch` `neofetch` `htop` `btop` `lsd` `bat` `fd-find` `ranger` `fzf` `zoxide` `thefuck` `direnv` `yt-dlp` `papirus-icon-theme`

## Notes

- Existing dotfiles are backed up as `<file>.backup.<date>` before overwriting
- The `configs/` folder is `.gitignore`d since it contains machine-specific data
- APT sources are restored **before** `apt update` so third-party repos are available
- Sudoers rules are validated with `visudo -c` before install (broken rules = locked out)
- Mirror URLs in `sources.list` may need editing if the target is in a different region
- `sysctl` params are applied immediately after copy
- LightDM and system configs require sudo
- After install, log out and back in for all changes to take effect
