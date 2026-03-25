# Sofle with Bongo Cat (Vial)

**Sofle rev1** firmware with **Vial**, starting from the Sofle Vial keymap in [vial-qmk](https://github.com/vial-kb/vial-qmk).

**OLED (USB side of the split):** The cat **taps when you press a key** and is **idle** when you are not typing. It also shows the **layer** you are on and your **WPM**.

## What’s inside

- `sofle/rev1/keymaps/vial/` — that Vial keymap, including the cat / layer / WPM OLED (`oled.c` and related files).

Upstream Sofle documentation and hardware notes still apply; see [`sofle/readme.md`](sofle/readme.md) for keyboard revision details and general build references.

## Prerequisites

Use the same environment as for any **QMK + Vial** keyboard:

1. [QMK build environment](https://docs.qmk.fm/#/getting_started_build_tools) (toolchain, QMK CLI).
2. A QMK tree that includes **Vial** support (for example a [vial-qmk](https://github.com/vial-kb/vial-qmk) checkout, or your own setup that matches how you normally flash Vial firmware).

Copy or merge the `sofle/` tree from this repo into your QMK firmware directory so `sofle/rev1/keymaps/vial` is available under your keyboard path, then build and flash from that tree.

## Flashing

Example commands for this keymap on **RP2040 CE** with the **UF2 split** bootloader. Flash **one half at a time**: connect the half you are flashing, enter the bootloader when QMK asks, then repeat for the other side.

**Left half:**

```bash
qmk flash -kb sofle/rev1 -km vial -e CONVERT_TO=rp2040_ce -bl uf2-split-left -j 31
```

**Right half:**

```bash
qmk flash -kb sofle/rev1 -km vial -e CONVERT_TO=rp2040_ce -bl uf2-split-right -j 31
```

`-j 31` tells the build to compile with **up to 31 parallel jobs** (same idea as `make -j31`). Use a number that fits your CPU (often number of cores, or cores × 2); lower it if the build runs out of memory or feels sluggish.

Adjust `-e CONVERT_TO=...`, `-bl`, and `-j` to match your controller and machine if they differ.
