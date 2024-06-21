## Combos

Combos are implemented as *virtual keys*. They're like regular keys, but they are activated by pressing multiple physical keys simultaneously. And since they're like regular keys, they're just like any other key in your keymap with full support for all the features. They can even have different keycodes across layers.

IMPORTANT NOTE: As you will see in the example below, There are 6 keys and 3 virtual keys, for a total of 9 keys. If you have complex hold-tap behaviors set up, you need to add those keys into your behaviors as well.

## Definitions:
combo.slow_release — By default, the combo is released once any combo key is released. Adding this to your combo means that both keys have to be released before it registers. 

combo.require_prior_idle_ms - During fast typing, you might want to ignore combos to prevent triggering them temporarily. You can prevent this by adding this to your combo.


Here are several examples of how this is implemented: 
```
let kc = tap.reg.kc in
let mod = hold.reg.mod in
let my_tap_dance = td.make 200 [kc.SPC, kc.ENT, hold.reg.layer 1] in
{
  virtual_keys = [
    # The first argument is the timeout_ms (up to 255)
    # The second argument is the key indices/positions (min 2, max 9 keys)
    combo.make 50 [2, 3],

    # By default, the combo is released once *any one* of the key indices is released
    # Merge with `combo.slow_release` if you want the combo to release once *all* of the key indices are released instead
    combo.make 30 [0, 2, 5] & combo.slow_release,

    # During fast typing, you might want to temporarily ignore combos to prevent triggering them
    # To do this, merge with `combo.require_prior_idle_ms [ms]`
    # For example, the following combo is ignored if the last keypress happened no more than 180ms ago.
    combo.make 60 [0, 1] & combo.require_prior_idle_ms 180

    # You can't use virtual key indices. Just physical keys.
  ],
  # Assuming a 6-key macropad + 3 virtual keys, our layers need to have 9 keycodes.
  layers = [
    [
      kc.A, kc.B, kc.C,
      kc.D, kc.E, kc.F,
      # After physical keycodes, our virtual keycodes begin:
      kc.N1 & mod.lctl,
      kc.N2 & mod.lalt,
      kc.N3,
    ],
    [
      kc.G, kc.H, kc.I,
      kc.J, kc.K, kc.L,
      # Like physical keys, they can be different across layers and use transparency
      my_tap_dance,
      tap.trans & mod.lgui,
      kc.N4,
    ],
  ],
}
```

Limitations:
- Fully overlapping combos (e.g., `[2, 3]` and `[2, 3, 4]`) are not supported yet. Partially overlapping combos (e.g., `[2, 3]` and `[3, 4, 5]`) are supported though, as shown in the example above.
