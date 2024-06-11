## Duplex matrix support

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
