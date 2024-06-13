---
title: Tap dance
---

## Tap dance

Similar to ZMK, the bindings can be hold-taps! This means in the following example, if you do a tap-tap-hold, you'll momentarily access layer 2.

```markdown
# 200 is the tapping_term_ms
td.make 200 [
  tap.reg.kc.F,
  tap.reg.kc.A & hold.reg.layer 1,
  tap.reg.kc.K & hold.reg.layer 2,
]
