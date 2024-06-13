---
title: Partial and full transparency
---

### Partial and full transparency

```markdown
## Partial and full transparency

Either one or both of the tap and hold portions can be transparent. Full transparency is equivalent to `KC_TRNS` in QMK.

```markdown
let kc = tap.reg.kc in
let mod = hold.reg.mod in
{
  layers = [
    [ # Layer 0
      kc.A & mod.lctl,       kc.B & mod.lsft,    kc.C & mod.lalt,         hold.reg.layer 1
    ],
    [ # Layer 1
      tap.trans & mod.lsft,  kc.J & hold.trans,  tap.trans & hold.trans,  tap.trans & hold.trans
    ]
  ]
}
