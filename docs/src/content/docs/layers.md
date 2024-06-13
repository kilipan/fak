---
title: Layers
---

### Layers

```markdown
## Layers

Yep. Layers. Up to 32.

```markdown
# Momentary layer (like MO in QMK)
hold.reg.layer [0-31]

# TG, like in QMK, toggles the layer on or off
tap.layer.TG [0-31]

# DF, roughly like in QMK, clears all layers except for the new specified default layer
tap.layer.DF [0-31]

# TO, like in QMK, turns the specified layer on, and clears all others except for the default layer
tap.layer.TO [0-31]
