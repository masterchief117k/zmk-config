# ZMK config: Ferris Sweep (Cradio)

Wireless firmware configuration for my **34-key Ferris Sweep** split keyboard (Cradio shield on two
**nice!nano v2** controllers), built with [ZMK](https://zmk.dev). GitHub Actions compiles the firmware
on every push, so there's no local toolchain to install.

![ZMK](https://img.shields.io/badge/firmware-ZMK-1F6FEB?style=flat-square)
![Board](https://img.shields.io/badge/board-nice!nano%20v2-555555?style=flat-square)
![Keys](https://img.shields.io/badge/keys-34-2EA043?style=flat-square)

## Layout ideas

- **Seven letters live on combos.** R, Y, J, C, B, Z and `.` are typed by pressing two neighbouring keys
  together (50 ms window), so everyday typing uses only 27 of the 34 keys and fingers travel less.
- **Home-row modifiers.** Holding A / S / D / F gives Shift / Alt / Ctrl / GUI, with Ctrl / Alt / Shift mirrored on K / L / `'`.
  They use a tap-preferred hold-tap (200 ms tapping term, 150 ms prior-idle) to avoid misfires while typing fast.
- **Thumb layer keys.** Tab and Backspace double as layer keys when held.
- **Automatic third layer.** Holding both layer keys opens a system layer: Bluetooth profiles, reset and bootloader.

| Layer | Purpose | How to reach it |
| :-- | :-- | :-- |
| 0 · Base | Letters with home-row modifiers | default |
| 1 · Navigation & numbers | Arrows, Home/End, Page Up/Down, digits, Caps Word | hold Backspace |
| 2 · Symbols | Brackets, operators and punctuation | hold Tab |
| 3 · System | Bluetooth profile 0/1, reset, bootloader, plus the combo letters | hold both layer keys |
| 4 · Gaming | Plain keys with no hold-tap delays; Ctrl, Space and Enter on the thumbs | combo: Q + W |
| 5 · Numpad | Numpad on the right hand | combo: W + E |

## Build and flash

1. Edit `config/cradio.keymap` and push. The **Build ZMK firmware** workflow runs automatically.
2. Open the latest run in the **Actions** tab and download the `firmware` artifact.
3. Double-tap reset on a half to mount it as a USB drive, then drop `cradio_left` or `cradio_right`
   `.uf2` onto the matching half.

## Files

| Path | Purpose |
| :-- | :-- |
| `config/cradio.keymap` | Layers, combos and hold-tap behaviour |
| `config/cradio.conf` | Firmware options (ZMK defaults for now) |
| `config/west.yml` | Pins the ZMK version to build against |
| `build.yaml` | Which board and shield pairs to compile |
| `.github/workflows/build.yml` | CI build using ZMK's reusable workflow |
