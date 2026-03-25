# Sofle with Bongo Cat (Vial)

This repository holds a **Sofle** keyboard layout based on the **Vial** keymap from the [vial-qmk](https://github.com/vial-kb/vial-qmk) project. The main change is the **OLED**: Bongo Cat is shown on the primary display instead of the stock Vial OLED content.

## What’s inside

- `sofle/rev1/keymaps/vial/` — Vial keymap with the Bongo Cat OLED implementation (see `oled.c` and related config).

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
