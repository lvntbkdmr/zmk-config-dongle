# ⌨️ ZMK Config for Corne with Dongle Support

This is my personal [ZMK](https://zmk.dev) configuration for my corne keyboard.
The configuration supports using the two halves as is or additionally use a
USB dongle.

![Corne Keyboard with Dongle](/setup.jpg)

## 🤔 Why a Dongle?

For me, the most selling benefit of using a dongle is the keyboard availability
before entering an OS. This means, via the dongle you could, e.g., do the
following:

- Choose your OS in a bootloader
- Configure your UEFI

Other benefits, including a much longer battery life for the "pre-master" half
can be found [here](https://www.slicemk.com/pages/split-dongle).

## 🚀 Usage

Clone or fork this repository and trigger a new GitHub action. If you do not know
what that means check [this](https://docs.github.com/en/actions) out.
Download the generated UF2 files from the workflow artifact.

### Without Dongle

When using the firmware without a dongle you have to declare a master half that
communicates with your operating system. Flash your left half of your split
keyboard with the `corne_left*.uf2` file. Your right half has to be flashed
with the `corne_right*.uf2` file.

### With Dongle

Flash your dongle with the `corne_dongle*.uf2` file to use it as a master that
communicates over USB with your OS. Now, your left half does not need to be a
master anymore, so flash it with the `corne_peripheral_left*.uf2` file. Flash
the right half with the `corne_right*.uf2` file.

Use these files for dongle mode:

- Dongle: `corne_dongle*.uf2`
- Left half: `corne_peripheral_left*.uf2`
- Right half: `corne_right*.uf2`

Do not flash `corne_left*.uf2` to the left half when using the dongle. That
firmware makes the left half the central device, so it will not behave as a
dongle peripheral.

### Reset and Re-pair Dongle Mode

If the halves do not connect to the dongle after a keymap, shield, or ZMK
configuration change, clear the saved settings on all three devices before
flashing the normal firmware again.

1. Flash the dongle with `settings_reset-xiao_ble*.uf2`, then flash it with
   `corne_dongle*.uf2`.
2. Flash the left half with `settings_reset-nice_nano*.uf2`, then flash it with
   `corne_peripheral_left*.uf2`.
3. Flash the right half with `settings_reset-nice_nano*.uf2`, then flash it with
   `corne_right*.uf2`.
4. Power off both halves.
5. Plug in the dongle.
6. Turn on the left half and wait a few seconds.
7. Turn on the right half and wait a few seconds.

## ❓ Troubleshooting

This repository uses [nice!nano's](https://nicekeyboards.com/nice-nano/) for
the split keyboard itself and a [Seeed XIAO BLE](https://wiki.seeedstudio.com/XIAO_BLE/) for the dongle.
If you do not own the same hardware, this repository will not work without any
adjustments.

If you have the same hardware and still encounter connection issues,
be sure to reset your settings on all your hardware by flashing the matching
`settings_reset*.uf2` file as described [here](https://zmk.dev/docs/troubleshooting#split-keyboard-halves-unable-to-pair).
The nice!nano halves and the XIAO BLE dongle use different reset UF2 files, so
use `settings_reset-nice_nano*.uf2` for the halves and
`settings_reset-xiao_ble*.uf2` for the dongle.
