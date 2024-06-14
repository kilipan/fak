---
title: Composable keycodes
---

## Composable keycodes

Keycodes are in 32 bits. 16 for the hold portion. 16 for the tap portion. If both portions exist, you get a hold-tap.

```markdown
# A
tap.reg.kc.A

# Ctrl-A
tap.reg.kc.A & tap.reg.mod.lctl

# Ctrl-A when tapped, Layer 1 (like MO(1) in QMK) when held
# Both portions exist. This is a hold-tap.
tap.reg.kc.A & tap.reg.mod.lctl & hold.reg.layer 1 & hold.reg.behavior {}

# Ctrl-Shift-A when tapped, Layer 1 with Alt and Shift when held
tap.reg.kc.A & tap.reg.mod.lctl & tap.reg.mod.lsft & hold.reg.layer 1 & hold.reg.mod.lalt & hold.reg.mod.lsft & hold.reg.behavior {}

# Layer 1 when pressed/held
# Only hold portion exists. This is not a hold-tap.
hold.reg.layer 1
