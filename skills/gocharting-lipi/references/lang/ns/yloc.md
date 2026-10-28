# yloc

## yloc (library)

Named constants for how label y-coordinates are interpreted: price, above the bar, or below the bar.

### example

```lipi
//@lipi=2
indicator("yloc Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, "above", xloc=xloc.bar_index, yloc=yloc.abovebar)
    label.new(bar_index, low, "below", xloc=xloc.bar_index, yloc=yloc.belowbar)
    label.new(bar_index, close, "price", xloc=xloc.bar_index, yloc=yloc.price)
}
```

### id

library:yloc

## yloc.abovebar (constant)

Vertical text alignment constant that places a label above the bar.

### type

const string

### example

```lipi
//@lipi=2
indicator("yloc.abovebar Example", overlay=true)
if barstate.islast {
    // The y value is ignored: the label sits above the bar
    label.new(bar_index, na, text="Above", yloc=yloc.abovebar, style=label.style_label_down)
}
```

### id

constant:yloc.abovebar

## yloc.belowbar (constant)

Vertical text alignment constant that places a label below the bar.

### type

const string

### example

```lipi
//@lipi=2
indicator("yloc.belowbar Example", overlay=true)
if barstate.islast {
    // The y value is ignored: the label sits below the bar
    label.new(bar_index, na, text="Below", yloc=yloc.belowbar, style=label.style_label_up)
}
```

### id

constant:yloc.belowbar

## yloc.price (constant)

Vertical location constant that places a label at a specific price level.

### type

const string

### example

```lipi
//@lipi=2
indicator("yloc.price Example", overlay=true)
if barstate.islast {
    label.new(bar_index, close, text="At the close", yloc=yloc.price)
}
```

### id

constant:yloc.price
