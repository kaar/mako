# mako

A lightweight notification daemon for Wayland. Works on Sway.

<p align="center">
  <img src="https://github.com/user-attachments/assets/25582bd6-bd3b-4bb3-b248-87fa7f88e967" alt="mako screenshot">
</p>

mako implements the [FreeDesktop Notifications Specification][spec].

Feel free to join the IRC channel: [#emersion on irc.libera.chat][irc].

## Running


`mako` will run automatically when a notification is emitted. This happens via
D-Bus activation, so you don't really need to explicitly start it up (this also
allows delaying its startup time and speed up system startup).

If you have several notification daemons installed though, you might want to
explicitly start this one. Some ways of achieving this is:

- If you're using Sway you can start mako on launch by putting `exec mako` in
  your configuration file.

- If you are not using systemd, you might need to manually start a dbus user
  session: `dbus-daemon --session --address=unix:path=$XDG_RUNTIME_DIR/bus`

## Configuration

`mako` can be extensively configured and customized - feel free to read more
using the command `man 5 mako`

For control of mako during runtime, `makoctl` can be used; see `man makoctl`

## Building

Install dependencies:

* meson (build-time dependency)
* wayland
* wayland-protocols
* pango
* cairo
* systemd, elogind or [basu] (for the sd-bus library)
* gdk-pixbuf (optional, for icons support)
* dbus (runtime dependency, user-session support is required)
* scdoc (optional, for man pages)

Then run:

```shell
meson setup build
ninja -C build
build/mako
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/4b32fef6-61d9-4ad1-8820-d4e5a245a76c" width="512" alt="mako">
</p>

## Usage

### Sway
If you are using Sway, you can add the following to your `~/.config/sway/config`:

```ini
exec mako
```

### Config
You can configure mako by creating a `~/.config/mako/config` file. Here is an example:

```ini
sort=-time
layer=overlay
# RGBA: last two hex chars set opacity (80 = ~50% opacity)
background-color=#2e344080
width=300
height=110
border-size=0
border-color=#88c0d0
border-radius=15
icons=0
max-icon-size=64
default-timeout=5000
ignore-timeout=1
font=monospace 14

[urgency=low]
border-color=#cccccc

[urgency=normal]
border-color=#d08770

[urgency=high]
border-color=#bf616a
default-timeout=0

[category=mpd]
default-timeout=2000
group-by=category
```

## I have a question!

See the [faq section in the wiki](https://github.com/emersion/mako/wiki/Frequently-asked-questions).

## License

MIT

[irc]: https://web.libera.chat/gamja/#emersion
[spec]: https://specifications.freedesktop.org/notification-spec/latest/
[basu]: https://github.com/emersion/basu
