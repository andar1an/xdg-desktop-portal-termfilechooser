# xdg-desktop-portal-termfilechooser

[xdg-desktop-portal] backend for choosing files with your favorite file
chooser.
By default, it will use the [yazi] file manager, but this is customizable.
Based on [xdg-desktop-portal-wlr] (xpdw).

## Building

```sh
meson build
ninja -C build
```

## Installing

### From Source - Original Content

```sh
ninja -C build install
```

### Manually - Doing this Until rewrite in Rust

```sh
doas cp build/xdg-desktop-portal-termfilechooser /usr/libexec/xdg-desktop-portal-termfilechooser
doas chown --reference=/usr/libexec/xdg-desktop-portal-gtk /usr/libexec/xdg-desktop-portal-termfilechooser
doas chmod --reference=/usr/libexec/xdg-desktop-portal-gtk /usr/libexec/xdg-desktop-portal-termfilechooser
doas cp build/org.freedesktop.impl.portal.desktop.termfilechooser.service /usr/share/dbus-1/services/org.freedesktop.impl.portal.desktop.termfilechooser
doas chown --reference=/usr/share/dbus-1/services/org.freedesktop.impl.portal.desktop.gtk.service /usr/share/dbus-1/services/org.freedesktop.impl.portal.desktop.termfilechooser
doas chmod --reference=/usr/share/dbus-1/services/org.freedesktop.impl.portal.desktop.gtk.service /usr/share/dbus-1/services/org.freedesktop.impl.portal.desktop.termfilechooser

echo "[Desktop Entry]
Type=Application
Name[be]=Партал
Name[ca]=Portal
Name[cs]=Portál
Name[da]=Portal
Name[de]=Portal
Name[en_GB]=Portal
Name[es]=Portal
Name[gl]=Portal
Name[he]=שער
Name[hi]=पोर्टल
Name[hr]=Portal
Name[hu]=Portál
Name[id]=Portal
Name[ie]=Portale
Name[it]=Portale
Name[ja]=ポータル
Name[ka]=პორტალი
Name[lt]=Portalas
Name[nl]=Portaal
Name[oc]=Portal
Name[pl]=Portal
Name[pt]=Portal
Name[pt_BR]=Portal
Name[ro]=Portal
Name[ru]=Портал
Name[sk]=Portál
Name[sl]=Portal
Name[sv]=Portal
Name[tr]=Kapı
Name[uk]=Портал
Name[zh_CN]=门户
Name[zh_TW]=入口
Name=Portal
# TRANSLATORS: Don't translate this text (this is icon name)
Icon=applications-system-symbolic
Exec=/usr/libexec/xdg-desktop-portal-termfilechooser
NoDisplay=true" | doas tee /usr/share/applications/xdg-desktop-portal-termfilechooser.desktop

doas chown --reference=/usr/share/applications/xdg-desktop-portal-gtk.desktop /usr/share/applications/xdg-desktop-portal-termfilechooser.desktop
doas chmod --reference=/usr/share/applications/xdg-desktop-portal-gtk.desktop /usr/share/applications/xdg-desktop-portal-termfilechooser.desktop

echo "[portal]
DBusName=org.freedesktop.impl.portal.desktop.termfilechooser
Interfaces=org.freedesktop.impl.portal.FileChooser;
UseIn=wlroots;niri;kde;gnome;Hyprland;Wayfire;river;phosh;i3" | doas tee /usr/share/xdg-desktop-portal/portals/termfilechooser.portal

doas chown --reference=/usr/share/xdg-desktop-portal/portals/gtk.portal /usr/share/xdg-desktop-portal/portals/termfilechooser.portal
doas chmod --reference=/usr/share/xdg-desktop-portal/portals/gtk.portal /usr/share/xdg-desktop-portal/portals/termfilechooser.portal

doas mkdir /etc/xdg/xdg-desktop-portal-termfilechooser
echo "[filechooser]
cmd=/usr/share/xdg-desktop-portal-termfilechooser/yazi-wrapper.sh
default_dir=/home/andar1an/Downloads" | doas tee /etc/xdg/xdg-desktop-portal-termfilechooser/config

doas chown --reference=/etc/xdg/xdg-desktop-portal-wlr/config /etc/xdg/xdg-desktop-portal-termfilechooser/config
doas chmod --reference=/etc/xdg/xdg-desktop-portal-wlr/config /etc/xdg/xdg-desktop-portal-termfilechooser/config
```

## Running - Original Docs

Make sure `XDG_CURRENT_DESKTOP` is set and imported into D-Bus.

When correctly installed, xdg-desktop-portal should automatically invoke
xdg-desktop-portal-termfilechooser when needed.

For example, to use this portal with Firefox, launch Firefox as such:
`GTK_USE_PORTAL=1 firefox`.

### Configuration - Original Docs

See `man 5 xdg-desktop-portal-termfilechooser`.

### Manual startup - Original Docs

At the moment, some command line flags are available for development and
testing. If you need to use one of these flags, you can start an instance of
xdpw using the following command:

```sh
xdg-desktop-portal-termfilechooser -r [OPTION...]
```

To list the available options, you can run `xdg-desktop-portal-termfilechooser
--help`.

## License

MIT

[xdg-desktop-portal]: https://github.com/flatpak/xdg-desktop-portal
[xdg-desktop-portal-wlr]: https://github.com/emersion/xdg-desktop-portal-wlr
[yazi]: https://yazi-rs.github.io
