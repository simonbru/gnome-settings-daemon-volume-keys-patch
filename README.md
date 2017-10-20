# gnome-settings-daemon-volume-step-patch
Archlinux PKGBUILD for gnome-settings-daemon with additional settings for volume keys

## Details
gnome-settings-daemon 3.26 added the ability to increase of decrase the volume
in finer steps by pressing **Shift + Volume up/down key** instead of the volume keys alone.
These new shortcuts are hardcoded, so this PKGBUILD includes a patch to make these shortcuts
configurable.

## Usage
After installing this package, change the settings `volume-up-precise` and `volume-down-precise`
in `org.gnome.settings-daemon.plugins.media-keys` using dconf-editor or gsettings.

### Example
To lower the volume using **Shift + Super + Numpad minus key**:
```
gsettings set org.gnome.settings-daemon.plugins.media-keys volume-down-precise '<Shift><Super>KP_Subtract'
```
