# James Mugford's Dotfiles

Dotfiles managed with chezmoi.

## Quick start

Base system handled by Omarchy.
Install core packages.

```sh
sudo pacman -S --needed chezmoi
```

Apply the dotfiles.

```sh
git clone https://github.com/jamesmugford/jmdotfiles.git .local/share/chezmoi
chezmoi apply
```

## Omarchy stuff

Set pacman parallel downloads to 1 to prevent timeout of Omarchy's Stable package mirror 
sudo perl -0pi -e 's/^ParallelDownloads = 5$/ParallelDownloads = 1/m' /etc/pacman.conf

## Optional packages

### Apps

```sh
yay -S --needed github-desktop-bin synology-drive sublime-text-4
```


### Nvidia

```sh
sudo pacman -S --needed nvidia-settings nvtop
```

## OpenTabletDriver

```sh
# May require more commands. See: https://opentabletdriver.net/Wiki/Install/Linux#aur-helper-method

yay -S opentabletdriver

systemctl --user enable opentabletdriver.service --now

sudo tee /etc/udev/rules.d/99-uinput-permissions.rules >/dev/null <<'EOF'
KERNEL=="uinput", GROUP="input", MODE="0660", TAG+="uaccess", OPTIONS+="static_node=uinput"
EOF
sudo udevadm control --reload
sudo udevadm trigger /dev/uinput
systemctl --user restart opentabletdriver

```

## Extras

[Secure boot with sbctl](https://wiki.cachyos.org/configuration/secure_boot_setup/)

### Talon

### JM Face Gestures

```sh
git clone <https://github.com/jamesmugford/jmfacegestures.git> ~/Projects
sudo firewall-cmd --permanent --add-port=11111/udp
sudo firewall-cmd --reload
```

### Notes

## Chezmoi Cheat Sheet

```sh
chezmoi init
chezmoi add ~/.bashrc
chezmoi edit ~/.bashrc
chezmoi diff
chezmoi -v apply
```

### Tmux Restore

Configured with `tmux-resurrect` and `tmux-continuum`.

* Save manually: `C-Space Ctrl-s`
* Restore manually: `C-Space Ctrl-r`
* Auto-save interval: 15 minutes
* Auto-restore runs when the tmux server starts
