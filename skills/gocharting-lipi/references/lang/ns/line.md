Contents: line (library) · line (type) · line.all (variable) · line.all (function) · line.copy (function) · line.delete (function) · line.get_price (function) · line.get_x1 (function) · line.get_x2 (function) · line.get_y1 (function) · line.get_y2 (function) · line.new (function) · line.new (function) · line.set_color (function) · line.set_extend (function) · line.set_point1 (function) · line.set_point2 (function) · line.set_style (function) · line.set_width (function) · line.set_x1 (function) · line.set_x2 (function) · line.set_xloc (function) · line.set_xloc (function) · line.set_xy1 (function) · line.set_xy2 (function) · line.set_y1 (function) · line.set_y2 (function) · line.style_arrow_both (constant) · line.style_arrow_left (constant) · line.style_arrow_right (constant) · line.style_dashed (constant) · line.style_dotted (constant) · line.style_solid (constant)

# line

## line (library)

Functions for creating and mutating line drawings between two chart points.

### notes

- A `line.<name>(ln, ...)` function can also be called on the line as `ln.<name>(...)`, for example `ln.set_x2(bar_index)`. The one exception is the four-argument form of `line.set_xloc`, which is a function only (see that entry).

### example

```lipi
//@lipi=2
indicator("line Library Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[20], close[20], bar_index, close, color=color.blue, width=2)
    line.set_style(l, line.style_dashed)
}
```

### id

library:line

## line (type)

A line drawing between two chart points. Use line.new to create lines and line.set_* functions to change them.

### example

```lipi
//@lipi=2
indicator("Line Type Example", overlay=true)
if barstate.islast {
    line.new(bar_index[10], high[10], bar_index, high, color=color.red, width=2)
}
```

### id

type:line

## line.all (variable)

Array of all currently existing line drawings, from oldest to newest.

### type

series array<line>

### example

```lipi
//@lipi=2
indicator("line.all Example", overlay=true)
if barstate.islast {
    line.new(bar_index[5], high[5], bar_index, high)
}
plot(array.length(line.all), title="Line Count")
```

### id

variable:line.all

## line.all (function)

Returns the array of all existing line objects (same as line.all).

### syntax

```
line.all() → series array<line>
```

### returnedType

series array<line>

### returnDesc

An array of line IDs, oldest to newest.

### example

```lipi
//@lipi=2
indicator("line.all Example", overlay=true)
plot(array.length(line.all), title="Count")
```

### id

function:line.all

## line.copy (function)

Creates a copy of a line.

### syntax

```
line.copy(series line id) → series line
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line

### returnedType

series line

### returnDesc

The new line ID.

### example

```lipi
//@lipi=2
indicator("line.copy Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    c = line.copy(l)
}
```

### id

function:line.copy

## line.delete (function)

Deletes a line. Any linefill that uses this line is also deleted.

### syntax

```
line.delete(series line id) → void
```

### args

- `id`: series line
  Line object to delete.
  types: series line, simple line, input line, const line, literal line

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.delete Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[5], high[5], bar_index, high)
    line.delete(l)
}
```

### id

function:line.delete

## line.get_price (function)

Returns the price of a line at x (interpolated between the two endpoints).

### syntax

```
line.get_price(series line id, series int x) → series float
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `x`: series int
  X-coordinate (bar index or time, depending on xloc).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### returnDesc

Price at x.

### example

```lipi
//@lipi=2
indicator("line.get_price Example", overlay=true)
static line l = line(na)
if barstate.islast {
    l := line.new(bar_index[10], high[10], bar_index, high, color=color.red)
}
plot(na(l) ? na : line.get_price(l, bar_index))
```

### id

function:line.get_price

## line.get_x1 (function)

Returns the first point's x-coordinate.

### syntax

```
line.get_x1(series line id) → series int
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line

### returnedType

series int

### returnDesc

X-coordinate of the first point.

### example

```lipi
//@lipi=2
indicator("line.get_x1 Example", overlay=true)
static line l = line(na)
if barstate.islast {
    l := line.new(bar_index[10], high[10], bar_index, high, color=color.red)
}
plot(na(l) ? na : line.get_x1(l))
```

### id

function:line.get_x1

## line.get_x2 (function)

Returns the second point's x-coordinate.

### syntax

```
line.get_x2(series line id) → series int
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line

### returnedType

series int

### returnDesc

X-coordinate of the second point.

### example

```lipi
//@lipi=2
indicator("line.get_x2 Example", overlay=true)
static line l = line(na)
if barstate.islast {
    l := line.new(bar_index[10], high[10], bar_index, high, color=color.red)
}
plot(na(l) ? na : line.get_x2(l))
```

### id

function:line.get_x2

## line.get_y1 (function)

Returns the first point's y-coordinate.

### syntax

```
line.get_y1(series line id) → series float
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line

### returnedType

series float

### returnDesc

Y-coordinate of the first point.

### example

```lipi
//@lipi=2
indicator("line.get_y1 Example", overlay=true)
static line l = line(na)
if barstate.islast {
    l := line.new(bar_index[10], high[10], bar_index, high, color=color.red)
}
plot(na(l) ? na : line.get_y1(l))
```

### id

function:line.get_y1

## line.get_y2 (function)

Returns the second point's y-coordinate.

### syntax

```
line.get_y2(series line id) → series float
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line

### returnedType

series float

### returnDesc

Y-coordinate of the second point.

### example

```lipi
//@lipi=2
indicator("line.get_y2 Example", overlay=true)
static line l = line(na)
if barstate.islast {
    l := line.new(bar_index[10], high[10], bar_index, high, color=color.red)
}
plot(na(l) ? na : line.get_y2(l))
```

### id

function:line.get_y2

## line.new (function)

Creates a line between two points. Coordinates can be passed as x1/y1/x2/y2 or as chartPoint first_point/second_point.

### syntax

```
line.new(series int x1, series float y1, series int x2, series float y2, series string xloc, series string extend, series color color, series string style, series int width, const bool forceOverlay) → series line
```

### args

- `x1`: series int
  X-coordinate of the first point (bar index or time, depending on xloc).
  types: series int, simple int, input int, const int, literal int
- `y1`: series float
  Y-coordinate (price) of the first point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `x2`: series int
  X-coordinate of the second point.
  types: series int, simple int, input int, const int, literal int
- `y2`: series float
  Y-coordinate (price) of the second point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `xloc?`: series string
  xloc.bar_index or xloc.bar_time. Default is bar_index.
  types: series string, simple string, input string, const string, literal string
  values: xloc.bar_index, xloc.bar_time
  default: xloc.bar_index
- `extend?`: series string
  extend.none, left, right, or both. Default is none.
  types: series string, simple string, input string, const string, literal string
  values: extend.both, extend.left, extend.none, extend.right
  default: extend.none
- `color?`: series color
  Line color. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `style?`: series string
  line.style_* constant. Optional.
  types: series string, simple string, input string, const string, literal string
  values: line.style_arrow_both, line.style_arrow_left, line.style_arrow_right, line.style_dashed, line.style_dotted, line.style_solid
  default: line.style_solid
- `width?`: series int
  Line width in pixels. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 1
- `forceOverlay?`: const bool
  If true, the line is drawn on the main chart pane even when the script runs in its own pane. Optional. The default is false. Spelled `forceOverlay` here, unlike the `force_overlay` of the other drawing and plot functions: `force_overlay=` is rejected on `line.new`.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false

### returnedType

series line

### returnDesc

The ID of the created line.

### example

```lipi
//@lipi=2
indicator("line.new Example", overlay=true)
if barstate.islast {
    line.new(bar_index[10], high[10], bar_index, high, color=color.red, width=2, style=line.style_solid, extend=extend.none)
}
```

### id

function:line.new~1

## line.new (function)

Creates a line between two points. Coordinates can be passed as x1/y1/x2/y2 or as chartPoint first_point/second_point.

### syntax

```
line.new(series chartPoint first_point, series chartPoint second_point, series string xloc, series string extend, series color color, series string style, series int width, const bool forceOverlay) → series line
```

### args

- `first_point`: series chartPoint
  Chart point for the first endpoint (alternative to x1/y1). Required argument.
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint
- `second_point`: series chartPoint
  Chart point for the second endpoint (alternative to x2/y2). Required argument.
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint
- `xloc?`: series string
  xloc.bar_index or xloc.bar_time. Default is bar_index.
  types: series string, simple string, input string, const string, literal string
  values: xloc.bar_index, xloc.bar_time
  default: xloc.bar_index
- `extend?`: series string
  extend.none, left, right, or both. Default is none.
  types: series string, simple string, input string, const string, literal string
  values: extend.both, extend.left, extend.none, extend.right
  default: extend.none
- `color?`: series color
  Line color. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `style?`: series string
  line.style_* constant. Optional.
  types: series string, simple string, input string, const string, literal string
  values: line.style_arrow_both, line.style_arrow_left, line.style_arrow_right, line.style_dashed, line.style_dotted, line.style_solid
  default: line.style_solid
- `width?`: series int
  Line width in pixels. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 1
- `forceOverlay?`: const bool
  If true, the line is drawn on the main chart pane even when the script runs in its own pane. Optional. The default is false. Spelled `forceOverlay` here, unlike the `force_overlay` of the other drawing and plot functions: `force_overlay=` is rejected on `line.new`.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false

### returnedType

series line

### returnDesc

The ID of the created line.

### example

```lipi
//@lipi=2
indicator("line.new Example", overlay=true)
if barstate.islast {
    line.new(bar_index[10], high[10], bar_index, high, color=color.red, width=2, style=line.style_solid, extend=extend.none)
}
```

### id

function:line.new~2

## line.set_color (function)

Sets a line's color.

### syntax

```
line.set_color(series line id, series color color) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `color`: series color
  Color value.
  types: series color, simple color, input color, const color, literal color

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_color Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_color(l, color.blue)
}
```

### id

function:line.set_color

## line.set_extend (function)

Sets whether a line extends past its endpoints.

### syntax

```
line.set_extend(series line id, series string extend) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `extend`: series string
  extend.none, left, right, or both.
  types: series string, simple string, input string, const string, literal string
  values: extend.both, extend.left, extend.none, extend.right

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_extend Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_extend(l, extend.right)
}
```

### id

function:line.set_extend

## line.set_point1 (function)

Sets a line's first endpoint from a chartPoint. X is taken from the point's index or time depending on the line's xloc.

### syntax

```
line.set_point1(series line id, series chartPoint point) → void
```

### args

- `id`: series line
  Line object to modify.
  types: series line, simple line, input line, const line, literal line
- `point`: series chartPoint
  A chartPoint for the first endpoint.
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_point1 Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_point1(l, chartPoint.from_index(bar_index[20], high[20]))
}
```

### id

function:line.set_point1

## line.set_point2 (function)

Sets a line's second endpoint from a chartPoint. X is taken from the point's index or time depending on the line's xloc.

### syntax

```
line.set_point2(series line id, series chartPoint point) → void
```

### args

- `id`: series line
  Line object to modify.
  types: series line, simple line, input line, const line, literal line
- `point`: series chartPoint
  A chartPoint for the second endpoint.
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_point2 Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_point2(l, chartPoint.from_index(bar_index, close))
}
```

### id

function:line.set_point2

## line.set_style (function)

Sets a line's style (line.style_*).

### syntax

```
line.set_style(series line id, series string style) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `style`: series string
  Style constant for this drawing type.
  types: series string, simple string, input string, const string, literal string
  values: line.style_arrow_both, line.style_arrow_left, line.style_arrow_right, line.style_dashed, line.style_dotted, line.style_solid

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_style Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_style(l, line.style_dashed)
}
```

### id

function:line.set_style

## line.set_width (function)

Sets a line's width in pixels.

### syntax

```
line.set_width(series line id, series int width) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `width`: series int
  Width in pixels.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_width Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_width(l, 2)
}
```

### id

function:line.set_width

## line.set_x1 (function)

Sets a line's first x-coordinate.

### syntax

```
line.set_x1(series line id, series int x1) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `x1`: series int
  X-coordinate of the first line point.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_x1 Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_x1(l, bar_index[10])
}
```

### id

function:line.set_x1

## line.set_x2 (function)

Sets a line's second x-coordinate.

### syntax

```
line.set_x2(series line id, series int x2) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `x2`: series int
  X-coordinate of the second line point.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_x2 Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_x2(l, bar_index)
}
```

### id

function:line.set_x2

## line.set_xloc (function)

Sets whether a line's x-coordinates are bar indexes or times.

### syntax

```
line.set_xloc(series line id, series string xloc) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `xloc`: series string
  xloc.bar_index or xloc.bar_time.
  types: series string, simple string, input string, const string, literal string
  values: xloc.bar_index, xloc.bar_time

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_xloc Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_xloc(l, xloc.bar_index)
}
```

### id

function:line.set_xloc~1

## line.set_xloc (function)

Sets whether a line's x-coordinates are bar indexes or times.

### syntax

```
line.set_xloc(series line id, series string xloc, series int x1, series int x2) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `xloc`: series string
  xloc.bar_index or xloc.bar_time.
  types: series string, simple string, input string, const string, literal string
  values: xloc.bar_index, xloc.bar_time
- `x1`: series int
  X-coordinate of the first line point.
  types: series int, simple int, input int, const int, literal int
- `x2`: series int
  X-coordinate of the second line point.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### notes

- Function form only: `ln.set_xloc(xloc.bar_time, x1, x2)` is rejected with "Too many arguments passed into the `line.set_xloc()` function call. Passed 4 arguments but expected 2." The two-argument form also works as `ln.set_xloc(xloc.bar_index)`.

### example

```lipi
//@lipi=2
indicator("line.set_xloc Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_xloc(l, xloc.bar_index)
}
```

### id

function:line.set_xloc~2

## line.set_xy1 (function)

Sets a line's first endpoint (x1, y1).

### syntax

```
line.set_xy1(series line id, series int x1, series float y1) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `x1`: series int
  X-coordinate of the first line point.
  types: series int, simple int, input int, const int, literal int
- `y1`: series float
  Y-coordinate of the first line point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_xy1 Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_xy1(l, bar_index[10], high[10])
}
```

### id

function:line.set_xy1

## line.set_xy2 (function)

Sets a line's second endpoint (x2, y2).

### syntax

```
line.set_xy2(series line id, series int x2, series float y2) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `x2`: series int
  X-coordinate of the second line point.
  types: series int, simple int, input int, const int, literal int
- `y2`: series float
  Y-coordinate of the second line point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_xy2 Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_xy2(l, bar_index, high)
}
```

### id

function:line.set_xy2

## line.set_y1 (function)

Sets a line's first y-coordinate.

### syntax

```
line.set_y1(series line id, series float y1) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `y1`: series float
  Y-coordinate of the first line point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_y1 Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_y1(l, high[10])
}
```

### id

function:line.set_y1

## line.set_y2 (function)

Sets a line's second y-coordinate.

### syntax

```
line.set_y2(series line id, series float y2) → void
```

### args

- `id`: series line
  Drawing object to modify or query.
  types: series line, simple line, input line, const line, literal line
- `y2`: series float
  Y-coordinate of the second line point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("line.set_y2 Example", overlay=true)
if barstate.islast {
    l = line.new(bar_index[10], high[10], bar_index, high, color=color.red)
    line.set_y2(l, high)
}
```

### id

function:line.set_y2

## line.style_arrow_both (constant)

Line style with arrows on both points.

### type

const string

### example

```lipi
//@lipi=2
indicator("line.style_arrow_both Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], close[20], bar_index, close, color=color.blue, width=2, style=line.style_arrow_both)
}
```

### id

constant:line.style_arrow_both

## line.style_arrow_left (constant)

Line style with an arrow on the first point.

### type

const string

### example

```lipi
//@lipi=2
indicator("line.style_arrow_left Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], close[20], bar_index, close, color=color.blue, width=2, style=line.style_arrow_left)
}
```

### id

constant:line.style_arrow_left

## line.style_arrow_right (constant)

Line style with an arrow on the second point.

### type

const string

### example

```lipi
//@lipi=2
indicator("line.style_arrow_right Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], close[20], bar_index, close, color=color.blue, width=2, style=line.style_arrow_right)
}
```

### id

constant:line.style_arrow_right

## line.style_dashed (constant)

Dashed line style for line.new / line.set_style.

### type

const string

### example

```lipi
//@lipi=2
indicator("line.style_dashed Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], close[20], bar_index, close, color=color.blue, width=2, style=line.style_dashed)
}
```

### id

constant:line.style_dashed

## line.style_dotted (constant)

Dotted line style for line.new / line.set_style.

### type

const string

### example

```lipi
//@lipi=2
indicator("line.style_dotted Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], close[20], bar_index, close, color=color.blue, width=2, style=line.style_dotted)
}
```

### id

constant:line.style_dotted

## line.style_solid (constant)

Solid line style for line.new / line.set_style.

### type

const string

### example

```lipi
//@lipi=2
indicator("line.style_solid Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], close[20], bar_index, close, color=color.blue, width=2, style=line.style_solid)
}
```

### id

constant:line.style_solid
