# lockheed

React to screen unlock events in Ubuntu Linux.

## Basic Usage

Every time the screen unlocks, echo `foo bar baz` to the standard output.

```sh
$ lockheed echo foo bar baz
```

After the next screen unlock, wait 5 seconds and then run a custom
script.

```sh
$ lockheed --once -c 'sleep 5 && ./myscript'
```

Get some help.

```sh
$ lockheed --help
```

## Installation

Copy the `lockheed` script to an appropriate place on your `PATH`, *e.g.*
`/usr/loca/bin`.

## Advanced Usage

To create a [systemd](https://www.freedesktop.org/wiki/Software/systemd/)
user service which does some useful actions when you unlock your
computer, you can create a service unit file such as
`my-unlock.service`:

```sh
[Unit]
Description=My Screen Unlock Actions

[Service]
ExecStart=lockheed -c 'myscript myarg1 myarg2'
Restart=on-failure
RestartSec=3s

[Install]
WantedBy=graphical-session.target
```

Copy `my-unlock.service` to an appropriate directory for systemd user
scripts on your system, for example `~/.config/systemd/user/` and
enable and start it in the usual way. Boom!

## Caveats

Tested and working on Ubuntu 20.04 running Gnome 3.36.8. If it does not
work on your distro, version, or desktop environment, please make it so
and submit a pull request!
