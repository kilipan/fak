---
title: Matrix support
---

## Supported Matrix Types

| Matrix  | Status | Required I/O pins |
|---------|---------|---------|
| Direct  |  ❓ Not tested ??? | Number of Keys |
| Standard  | ✅ Fully supported and tested | Row + Column |
| Folded  | ✅ Fully supported and tested | Row * 2 + Column / 2 |
| Duplex  | ✅ Fully supported and tested | Row * Column / 2 |


## Direct Pin

A direct pin design (not really a matrix) is ideal for smaller designs like a macro pad or similar, where you really want to simplify the design and build and keep components to a minimum, as it requires no diodes to be soldered. The downside is that you are limited in number of pins to the available pins on the MCU. 
 
## Standard matrix

FAK supports both col-to-row and row-to-col matrix scanning with `ColToRowKey` and `RowToColKey` respectively. the simplest matrix can be calculated as plain `Rows + Columns` in how many pins are required. This is perfect for an ortholinear square design with no wasted pins or split designs that have limited keys per hand, but the type is rather inefficient in how many pins it uses.

## Folded Matrix

When you want to design a more standard keyboard that is longer and have far more columns, and need to use a few less pins, a folded matrix does just that by making the matrix a bit more square.

## Duplex matrix

When you simply need all of the keys, or if you are trying to get by with one of the MCU's with less pins, a Duplex Matrix is the most efficient option.

FAK supports both col-to-row and row-to-col matrix scanning with `ColToRowKey` and `RowToColKey` respectively. Now, it's also possible to mix both of these two in one, resulting in a [duplex matrix](https://kbd.news/The-Japanese-duplex-matrix-1391.html). There is an [example keyboard definition](https://github.com/semickolon/fak-config/blob/main/keyboards/kazik/keyboard.ncl) for the [Kazik](https://github.com/monokuroumu/Kazik), a duplex matrix keyboard, for your reference. But basically, to get a duplex matrix keyboard working, you just mix both `ColToRowKey`s and `RowToColKey`s like so in your `keyboard.ncl`.

```
let { ColToRowKey, RowToColKey, .. } = import "fak/keyboard.ncl" in

# (snip)

# Here we have a 12-key layout that only uses 5 pins
  keys =
      let C = ColToRowKey in
      let R = RowToColKey in
      [
        R 0 0, C 0 0, R 1 0, C 1 0, R 2 0, C 2 0,
        R 0 1, C 0 1, R 1 1, C 1 1, R 2 1, C 2 1,
      ]
