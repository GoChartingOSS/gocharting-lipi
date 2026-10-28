Contents: linefill (library) · linefill (type) · linefill.all (variable) · linefill.all (function) · linefill.delete (function) · linefill.get_line1 (function) · linefill.get_line2 (function) · linefill.new (function) · linefill.set_color (function)

# linefill

## linefill (library)

Functions for filling the region between two line drawings. One fill per ordered line pair; creating another fill on the same pair replaces the previous one. Deleting a line also deletes fills that use it.

### example

```lipi
//@lipi=2
indicator("linefill Library Example", overlay=true)
if barstate.islast {
    upper = line.new(bar_index[20], talib.highest(high, 20), bar_index, talib.highest(high, 20), color=color.green)
    lower = line.new(bar_index[20], talib.lowest(low, 20), bar_index, talib.lowest(low, 20), color=color.red)
    linefill.new(upper, lower, color.new(color.gray, 0.2))
}
```

### id

library:linefill

## linefill (type)

A colored fill between two line drawings. The fill follows the current geometry of those lines. Only one fill may exist for a given ordered pair of lines; a later linefill.new on the same pair replaces the previous fill.

### example

```lipi
//@lipi=2
indicator("Linefill Type Example", overlay=true)
if barstate.islast {
    l1 = line.new(bar_index[10], high[10], bar_index, high, color=color.green)
    l2 = line.new(bar_index[10], low[10], bar_index, low, color=color.red)
    linefill.new(l1, l2, color.new(color.blue, 0.7))
}
```

### id

type:linefill

## linefill.all (variable)

Array of all currently existing linefill drawings, from oldest to newest. A second fill on the same ordered line pair replaces the previous one, so this array never holds two fills for the same pair.

### type

series array<linefill>

### example

```lipi
//@lipi=2
indicator("linefill.all Example", overlay=true)
if barstate.islast {
    l1 = line.new(bar_index[10], high[10], bar_index, high)
    l2 = line.new(bar_index[10], low[10], bar_index, low)
    linefill.new(l1, l2, color.new(color.teal, 0.7))
}
plot(array.length(linefill.all), title="Linefill Count")
```

### id

variable:linefill.all

## linefill.all (function)

Returns the array of all existing linefill objects (same as the linefill.all variable).

### syntax

```
linefill.all() → series array<linefill>
```

### returnedType

series array<linefill>

### returnDesc

An array of linefill IDs, oldest to newest.

### example

```lipi
//@lipi=2
indicator("linefill.all Function Example", overlay=true)
plot(array.length(linefill.all), title="Fills")
```

### id

function:linefill.all

## linefill.delete (function)

Deletes a linefill. Does not delete the two lines it was attached to. Deleting either line also deletes attached fills.

### syntax

```
linefill.delete(series linefill id) → void
```

### args

- `id`: series linefill
  Linefill object to delete.
  types: series linefill, simple linefill, input linefill, const linefill, literal linefill

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("linefill.delete Example", overlay=true)
if barstate.islast {
    l1 = line.new(bar_index[10], high[10], bar_index, high)
    l2 = line.new(bar_index[10], low[10], bar_index, low)
    f = linefill.new(l1, l2, color.new(color.blue, 0.7))
    linefill.delete(f)
}
```

### id

function:linefill.delete

## linefill.get_line1 (function)

Returns the first line used when the fill was created.

### syntax

```
linefill.get_line1(series linefill id) → series line
```

### args

- `id`: series linefill
  Linefill object.
  types: series linefill, simple linefill, input linefill, const linefill, literal linefill

### returnedType

series line

### returnDesc

The first line object, or na if the fill or line no longer exists.

### example

```lipi
//@lipi=2
indicator("linefill.get_line1 Example", overlay=true)
if barstate.islast {
    l1 = line.new(bar_index[10], high[10], bar_index, high)
    l2 = line.new(bar_index[10], low[10], bar_index, low)
    f = linefill.new(l1, l2, color.new(color.blue, 0.7))
    line.set_color(linefill.get_line1(f), color.green)
}
```

### id

function:linefill.get_line1

## linefill.get_line2 (function)

Returns the second line used when the fill was created.

### syntax

```
linefill.get_line2(series linefill id) → series line
```

### args

- `id`: series linefill
  Linefill object.
  types: series linefill, simple linefill, input linefill, const linefill, literal linefill

### returnedType

series line

### returnDesc

The second line object, or na if the fill or line no longer exists.

### example

```lipi
//@lipi=2
indicator("linefill.get_line2 Example", overlay=true)
if barstate.islast {
    l1 = line.new(bar_index[10], high[10], bar_index, high)
    l2 = line.new(bar_index[10], low[10], bar_index, low)
    f = linefill.new(l1, l2, color.new(color.blue, 0.7))
    line.set_color(linefill.get_line2(f), color.red)
}
```

### id

function:linefill.get_line2

## linefill.new (function)

Creates a fill between two lines. If a fill already exists for this ordered pair (line1, line2), the previous fill is deleted and replaced. (line2, line1) is a different pair.

### syntax

```
linefill.new(series line line1, series line line2, series color color) → series linefill
```

### args

- `line1`: series line
  First line object. The fill tracks this line's current points.
  types: series line, simple line, input line, const line, literal line
- `line2`: series line
  Second line object. The fill tracks this line's current points.
  types: series line, simple line, input line, const line, literal line
- `color?`: series color
  Fill color. Optional. Default is na.
  types: series color, simple color, input color, const color, literal color
  default: na

### returnedType

series linefill

### returnDesc

The ID of the created linefill, or na if either line is invalid.

### example

```lipi
//@lipi=2
indicator("linefill.new Example", overlay=true)
if barstate.islast {
    l1 = line.new(bar_index[20], high[20], bar_index, high, color=color.green)
    l2 = line.new(bar_index[20], low[20], bar_index, low, color=color.red)
    f = linefill.new(l1, l2, color.new(color.blue, 0.7))
}
```

### id

function:linefill.new

## linefill.set_color (function)

Sets the fill color of an existing linefill.

### syntax

```
linefill.set_color(series linefill id, series color color) → void
```

### args

- `id`: series linefill
  Linefill object.
  types: series linefill, simple linefill, input linefill, const linefill, literal linefill
- `color`: series color
  New fill color.
  types: series color, simple color, input color, const color, literal color

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("linefill.set_color Example", overlay=true)
if barstate.islast {
    l1 = line.new(bar_index[10], high[10], bar_index, high)
    l2 = line.new(bar_index[10], low[10], bar_index, low)
    f = linefill.new(l1, l2, color.new(color.blue, 0.7))
    linefill.set_color(f, color.new(color.orange, 0.7))
}
```

### id

function:linefill.set_color
