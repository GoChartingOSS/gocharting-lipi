Contents: position (library) · position.bottom_center (constant) · position.bottom_left (constant) · position.bottom_right (constant) · position.middle_center (constant) · position.middle_left (constant) · position.middle_right (constant) · position.top_center (constant) · position.top_left (constant) · position.top_right (constant)

# position

## position (library)

Named constants for table placement on the chart pane (top/middle/bottom × left/center/right). Only one live table is allowed at each position.

### example

```lipi
//@lipi=2
indicator("position Library Example", overlay=true)
if barstate.islast {
    t = table.new(position.bottom_left, 2, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="RSI", textcolor=color.white)
    table.cell(t, 1, 0, text=str.tostring(math.round(talib.rsi(close, 14), 1)), textcolor=color.white)
}
```

### id

library:position

## position.bottom_center (constant)

Table position: bottom-center of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.bottom_center Example", overlay=true)
if barstate.islast {
    t = table.new(position.bottom_center, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.bottom_center

## position.bottom_left (constant)

Table position: bottom-left corner of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.bottom_left Example", overlay=true)
if barstate.islast {
    t = table.new(position.bottom_left, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.bottom_left

## position.bottom_right (constant)

Table position: bottom-right corner of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.bottom_right Example", overlay=true)
if barstate.islast {
    t = table.new(position.bottom_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.bottom_right

## position.middle_center (constant)

Table position: center of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.middle_center Example", overlay=true)
if barstate.islast {
    t = table.new(position.middle_center, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.middle_center

## position.middle_left (constant)

Table position: middle-left of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.middle_left Example", overlay=true)
if barstate.islast {
    t = table.new(position.middle_left, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.middle_left

## position.middle_right (constant)

Table position: middle-right of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.middle_right Example", overlay=true)
if barstate.islast {
    t = table.new(position.middle_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.middle_right

## position.top_center (constant)

Table position: top-center of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.top_center Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_center, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.top_center

## position.top_left (constant)

Table position: top-left corner of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.top_left Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_left, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.top_left

## position.top_right (constant)

Table position: top-right corner of the chart pane.

### type

const string

### example

```lipi
//@lipi=2
indicator("position.top_right Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)), textcolor=color.white)
}
```

### id

constant:position.top_right
