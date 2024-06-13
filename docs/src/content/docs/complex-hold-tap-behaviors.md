---
title: Complex hold-tap behaviors
---

### Complex hold-tap behaviors

```markdown
## Complex hold-tap behaviors

Inspired by and building on top of ZMK.

- You can choose a flavor *per key*. Tap-preferred on key 3, hold-preferred on key 42, and balanced on key 69? No problem!
- Quick tap. Allows hold-taps to remain resolved as a tap if tapped then held quickly.
- Quick tap interrupt. Allows a quick tap to re-resolve to a hold if interrupted by another key press.
- Global quick tap. Allows hold-taps to resolve as a tap during continuous typing.
- Global quick tap ignore consecutive. Ignores global quick tap if the same key is pressed at least twice in a row.
- Eager decision. Allows hold-taps to pre-resolve as a hold or a tap until the actual decision is made. If the actual decision doesn't match the eager decision, the eager is reversed then the actual is applied. Otherwise, if the decisions match, nothing else happens because it's as if the hold-tap predicted the future.

```markdown
let my_crazy_behavior = {
  timeout_ms = 200,          # Known as tapping term in QMK and ZMK. 200 by default.
  timeout_decision = 'hold,  # Can be set to 'hold (default) or 'tap
  eager_decision = 'tap,     # Can be set to 'hold, 'tap, or 'none (default)
  key_interrupts = [         # Size of this must match key count. This assumes we have 5 keys.
    { decision = 'hold, trigger_on = 'press },      # Similar to ZMK's hold-preferred / QMK's HOLD_ON_OTHER_KEY_PRESS
    { decision = 'tap, trigger_on = 'press },
    { decision = 'hold, trigger_on = 'release },    # Similar to ZMK's balanced / QMK's PERMISSIVE_HOLD
    { decision = 'tap, trigger_on = 'release },
    { decision = 'none },                           # Similar to ZMK's tap-preferred
  ],
  quick_tap_ms = 150,              # 0 (disabled) by default
  quick_tap_interrupt_ms = 500,    # 0 (disabled) by default
  global_quick_tap_ms = 120,       # 0 (disabled) by default
  global_quick_tap_ignore_consecutive = true,     # false by default
} in

# Behaviors are bound to hold-taps like so
let my_crazy_key =
  tap.reg.kc.A
  & hold.reg.layer 1
  & hold.reg.behavior my_crazy_behavior
in
