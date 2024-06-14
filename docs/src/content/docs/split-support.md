---
title: Split keyboard support
---

### Split keyboard support

```markdown
## Split support

Central and peripheral sides are *fully independently* defined, so no considerations need to be made about symmetry, pin placement, and whatnot. They can be two entirely different keyboards connected together for all FAK cares.

```markdown
# This is an example of how a 10-key "split macropad" would be defined in keyboard.ncl

let { DirectPinKey, PeripheralSideKey, .. } = import "fak/keyboard.ncl" in
let { CH552T, .. } = import "fak/mcus.ncl" in

let D = DirectPinKey in
let S = PeripheralSideKey in

let side_periph = {
  mcu = CH552T,
  split.channel = CH552T.features.uart_30_31,
  keys = [
    D 13, D 14, D 15,
    D 32, D 33, D 12,
  ]
} in

# The central side has two fields that aren't in the peripheral:
# `split.peripheral` and `usb_dev`
{
  mcu = CH552T,
  split.channel = CH552T.features.uart_12_13,
  split.peripheral = side_periph,
  usb_dev = {
    # Nickel doesn't support hex literals yet
    vendor_id = 2023,
    product_id = 69,
    product_ver = 420,
  },
  keys = [
    D 14, D 15,   S 0, S 1, S 2,
    D 30, D 11,   S 3, S 4, S 5,
  ]
}
