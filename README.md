# evmk tools

evmk is a alpha stage tool under development.

evmk is developed to learn actual keyboard behavior differences among keyboards
to investigate ways to enable QMK-like home row mod and multilayer keyboard
behavior on normal keyboards connected to the Linux system.  It uses Python for
ease of coding. C/C++/go re-implementation for speed and size is desirable.

## evmk

evmk is a Linux evdev signal filter and logging script used with the
**interception-tools**. 

### Supported features of evmk

* Key code remapping
* Key code logging
* Dual-Function keys (DFK) for tap and hold
  * Support tap behavior for short press to emit a key code.
  * Support hold behavior for long press to change keyboard mode
    * layer change to emit a different key code
    * additional mod keys to be emitted together with the original key code of keys pressed
  * Support classical hold behavior of repeat by tap -> short-gap -> hold
  * Support time independent hold detection mechanism in addition to the normal time based one
  * Release key code based on the last press code result
  * Layer keys (up to 8 layers) as DFK
  * Mod keys (8 mod keys: [LEFT|RIGHT][SHIFT|CONTROL|ALT|META]) as DFK
* Support pass through after consecutive 100 * ESCs

### Usage of evmk

```
usage: evmk [-h] [-t] [-d] [-v [u|a|o]] [-g] [-m] [-s SECTION] [-l LOG]

A collection of python scripts to play with evdev events. version: 0.1
copyright 2022 Osamu Aoki <osamu@debian.org> license: GPL 2.0+ See See
https://github.com/osamuaoki/evmk

options:
  -h, --help            show this help message and exit
  -t, --timestamp       with timestamp
  -d, --delta           time as delta
  -v [u|a|o], --value [u|a|o]
                        key state value for log (default=u for ↑ ↓ →)
  -g, --group           group by event grp ending with SYN
  -m, --monitor         monitor only (no stdout)
  -s SECTION, --section SECTION
                        section to activate log: [1|2|3|4|5|9]
  -l LOG, --log LOG     set logging level (default=WARNING)
```

## `genmap`

`genmap` creates keyboard remapping table in the simple CSV format.

Currently, remapping is supported for all TKL-key positions.

## TODO

I see some shortcomings.

* evmk currently focuses on US TKL-key positions.  But it can handle all full
  size key positions.

* evmk acts as mere pass-through for unsupported events such as mouse,
  joystick, ... .  

* evmk doesn't trap native LED signals for CapsLock nor generate one for
  remap-generated CapsLock KEY events.  NumLock situation should be similar.

## LICENSE

GPL2+ or MIT whichever you like

## Prerequisite: interception by Francisco Lopes

For evmk tools to be useful, interception-tools by Francisco Lopes is needed.

* For Linux: https://gitlab.com/interception/linux/tools (This is what I target)

* For Windows: https://github.com/oblitum/Interception
  * Blog: http://www.oblita.com/interception

Osamu Aoki <osamu@debian.org> 2022-08-14
