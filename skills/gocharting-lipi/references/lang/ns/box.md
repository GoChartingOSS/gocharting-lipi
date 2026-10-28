Contents: box (library) · box (type) · box.all (variable) · box.all (function) · box.copy (function) · box.delete (function) · box.get_bottom (function) · box.get_left (function) · box.get_right (function) · box.get_top (function) · box.new (function) · box.new (function) · box.set_bgcolor (function) · box.set_border_color (function) · box.set_border_style (function) · box.set_border_width (function) · box.set_bottom (function) · box.set_bottom_right_point (function) · box.set_extend (function) · box.set_left (function) · box.set_lefttop (function) · box.set_right (function) · box.set_rightbottom (function) · box.set_text (function) · box.set_text_color (function) · box.set_text_font_family (function) · box.set_text_formatting (function) · box.set_text_halign (function) · box.set_text_size (function) · box.set_text_valign (function) · box.set_text_wrap (function) · box.set_top (function) · box.set_top_left_point (function) · box.set_xloc (function)

# box

## box (library)

Functions for creating and mutating rectangular box drawings on the chart.

`box.new` text options use `size`, `textcolor`, `texthalign`, `textvalign`, `textwrap`, and `text_font_family`; setters keep the `box.set_text_*` names.

### notes

- A `box.<name>(b, ...)` function can also be called on the box as `b.<name>(...)`, for example `b.set_right(bar_index)`.

### example

```lipi
//@lipi=2
indicator("box Library Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[20], talib.highest(high, 20), bar_index, talib.lowest(low, 20), bgcolor=color.new(color.blue, 0.15), border_color=color.blue, textcolor=color.white)
    box.set_text(b, "20-bar range")
}
```

### id

library:box

## box (type)

A rectangular drawing on the chart, defined by two corners. Use box.new to create boxes and box.set_* functions to change them.

### example

```lipi
//@lipi=2
indicator("Box Type Example", overlay=true)
if barstate.islast {
    box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
}
```

### id

type:box

## box.all (variable)

Array of all currently existing box drawings, from oldest to newest. The pointer is stable for the script lifetime.

### type

series array<box>

### example

```lipi
//@lipi=2
indicator("box.all Example", overlay=true)
if barstate.islast {
    box.new(bar_index[5], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
}
plot(array.length(box.all), title="Box Count")
```

### id

variable:box.all

## box.all (function)

Returns the array of all existing box objects (same as box.all).

### syntax

```
box.all() → series array<box>
```

### returnedType

series array<box>

### returnDesc

An array of box IDs, oldest to newest.

### example

```lipi
//@lipi=2
indicator("box.all Example", overlay=true)
plot(array.length(box.all), title="Count")
```

### id

function:box.all

## box.copy (function)

Creates a copy of a box.

### syntax

```
box.copy(series box id) → series box
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box

### returnedType

series box

### returnDesc

The new box ID.

### example

```lipi
//@lipi=2
indicator("box.copy Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    c = box.copy(b)
}
```

### id

function:box.copy

## box.delete (function)

Deletes a box.

### syntax

```
box.delete(series box id) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.delete Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.delete(b)
}
```

### id

function:box.delete

## box.get_bottom (function)

Returns the bottom price of a box.

### syntax

```
box.get_bottom(series box id) → series float
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box

### returnedType

series float

### returnDesc

Bottom y-coordinate.

### example

```lipi
//@lipi=2
indicator("box.get_bottom Example", overlay=true)
static box b = box(na)
if barstate.islast {
    b := box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
}
plot(na(b) ? na : box.get_bottom(b))
```

### id

function:box.get_bottom

## box.get_left (function)

Returns the left x-coordinate of a box.

### syntax

```
box.get_left(series box id) → series int
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box

### returnedType

series int

### returnDesc

Left x-coordinate.

### example

```lipi
//@lipi=2
indicator("box.get_left Example", overlay=true)
static box b = box(na)
if barstate.islast {
    b := box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
}
plot(na(b) ? na : box.get_left(b))
```

### id

function:box.get_left

## box.get_right (function)

Returns the right x-coordinate of a box.

### syntax

```
box.get_right(series box id) → series int
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box

### returnedType

series int

### returnDesc

Right x-coordinate.

### example

```lipi
//@lipi=2
indicator("box.get_right Example", overlay=true)
static box b = box(na)
if barstate.islast {
    b := box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
}
plot(na(b) ? na : box.get_right(b))
```

### id

function:box.get_right

## box.get_top (function)

Returns the top price of a box.

### syntax

```
box.get_top(series box id) → series float
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box

### returnedType

series float

### returnDesc

Top y-coordinate.

### example

```lipi
//@lipi=2
indicator("box.get_top Example", overlay=true)
static box b = box(na)
if barstate.islast {
    b := box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
}
plot(na(b) ? na : box.get_top(b))
```

### id

function:box.get_top

## box.new (function)

Creates a box from left/top/right/bottom coordinates, or from two chartPoint corners.

Text styling uses `size`, `textcolor`, `texthalign`, `textvalign`, `textwrap`, and `text_font_family` (typed `size` and `font` enums where noted).

### syntax

```
box.new(series int left, series float top, series int right, series float bottom, series color border_color, series int border_width, series string border_style, series string extend, series string xloc, series color bgcolor, series string text, series size size, series color textcolor, series string texthalign, series string textvalign, series string textwrap, input font text_font_family, const bool force_overlay, series string text_formatting) → series box
```

### args

- `left`: series int
  Left x-coordinate (bar index or time, depending on xloc).
  types: series int, simple int, input int, const int, literal int
- `top`: series float
  Top price of the box.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `right`: series int
  Right x-coordinate (bar index or time, depending on xloc).
  types: series int, simple int, input int, const int, literal int
- `bottom`: series float
  Bottom price of the box.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `border_color?`: series color
  Border color. Optional. Default is `#483D8B`.
  types: series color, simple color, input color, const color, literal color
  default: #483D8B
- `border_width?`: series int
  Border width in pixels. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 1
- `border_style?`: series string
  Border style (line.style_*). Optional.
  types: series string, simple string, input string, const string, literal string
  values: line.style_arrow_both, line.style_arrow_left, line.style_arrow_right, line.style_dashed, line.style_dotted, line.style_solid
  default: line.style_solid
- `extend?`: series string
  Whether the box extends past its corners: extend.none, left, right, or both.
  types: series string, simple string, input string, const string, literal string
  values: extend.both, extend.left, extend.none, extend.right
  default: extend.none
- `xloc?`: series string
  xloc.bar_index or xloc.bar_time. Default is bar_index.
  types: series string, simple string, input string, const string, literal string
  values: xloc.bar_index, xloc.bar_time
  default: xloc.bar_index
- `bgcolor?`: series color
  Background fill color of the box. Optional. Default is `#483D8B`.
  types: series color, simple color, input color, const color, literal color
  default: #483D8B
- `text?`: series string
  Text drawn inside the box. Optional.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `size?`: series size
  Text size inside the box (`size.auto`, `size.tiny` … `size.huge`). Optional. Default is `size.auto`.
  The old name `text_size` still compiles for now, with a deprecation warning.
  types: series size, simple size, input size, const size, literal size
  default: size.auto
- `textcolor?`: series color
  Text color inside the box. Optional. Default is `#483D8B`.
  The old name `text_color` still compiles for now, with a deprecation warning.
  types: series color, simple color, input color, const color, literal color
  default: #483D8B
- `texthalign?`: series string
  Horizontal text alignment: left, center, or right. Default is center.
  The old name `text_halign` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: text.align_left, text.align_center, text.align_right
  default: text.align_center
- `textvalign?`: series string
  Vertical text alignment: top, center, or bottom. Default is center.
  The old name `text_valign` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: text.align_top, text.align_center, text.align_bottom
  default: text.align_center
- `textwrap?`: series string
  Text wrap mode (`none` or `word`). Default is `none`.
  The old name `text_wrap` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: "none", "word"
  default: "none"
- `text_font_family?`: input font
  Font family for box text (`font.family_default` or `font.family_monospace`). Optional. Default is `font.family_default`.
  types: input font, const font, literal font
  default: font.family_default
- `force_overlay?`: const bool
  If true, draw on the main pane even when the script is not overlay. Default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `text_formatting?`: series string
  Text formatting (none, bold, italic). Optional.
  types: series string, simple string, input string, const string, literal string
  values: text.format_bold, text.format_italic, text.format_none
  default: text.format_none

### returnedType

series box

### returnDesc

The ID of the created box.

### notes

- The `size` argument takes a `size.*` constant (`size.auto`, `size.tiny`, `size.small`, `size.normal`, `size.large`, `size.huge`). A string such as "small" still compiles, with a deprecation warning: write the constant.
- The old names `text_color`, `text_halign`, `text_valign`, `text_size` and `text_wrap` still compile, with a deprecation warning that names the new spelling (`textcolor`, `texthalign`, `textvalign`, `size`, `textwrap`). Giving both spellings of one argument is an error. Write the new names.
- A string that is not a size name, such as "giant", stops the compiler with the error "internal validator error": write a `size.*` constant.
- The two forms have different default colors. Given `left`, `top`, `right` and `bottom`, `border_color`, `bgcolor` and `textcolor` default to `#483D8B`. Given two chartPoint corners, `border_color` and `bgcolor` default to `color.blue` and `textcolor` to `color.white`.

### example

```lipi
//@lipi=2
indicator("box.new Example", overlay=true)
if barstate.islast {
    box.new(bar_index[10], high, bar_index, low, bgcolor=color.new(color.blue, 0.8), border_color=color.blue, textcolor=color.white)
}
```

### id

function:box.new~1

## box.new (function)

Creates a box from left/top/right/bottom coordinates, or from two chartPoint corners.

Text styling uses `size`, `textcolor`, `texthalign`, `textvalign`, `textwrap`, and `text_font_family` (typed `size` and `font` enums where noted).

### syntax

```
box.new(series chartPoint top_left, series chartPoint bottom_right, series color border_color, series int border_width, series string border_style, series string extend, series string xloc, series color bgcolor, series string text, series size size, series color textcolor, series string texthalign, series string textvalign, series string textwrap, input font text_font_family, const bool force_overlay, series string text_formatting) → series box
```

### args

- `top_left`: series chartPoint
  Top-left corner as a chartPoint (alternative to left/top).
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint
- `bottom_right`: series chartPoint
  Bottom-right corner as a chartPoint (alternative to right/bottom).
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint
- `border_color?`: series color
  Border color. Optional. Default is `color.blue`.
  types: series color, simple color, input color, const color, literal color
  default: color.blue
- `border_width?`: series int
  Border width in pixels. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 1
- `border_style?`: series string
  Border style (line.style_*). Optional.
  types: series string, simple string, input string, const string, literal string
  values: line.style_arrow_both, line.style_arrow_left, line.style_arrow_right, line.style_dashed, line.style_dotted, line.style_solid
  default: line.style_solid
- `extend?`: series string
  Whether the box extends past its corners: extend.none, left, right, or both.
  types: series string, simple string, input string, const string, literal string
  values: extend.both, extend.left, extend.none, extend.right
  default: extend.none
- `xloc?`: series string
  xloc.bar_index or xloc.bar_time. Default is bar_index.
  types: series string, simple string, input string, const string, literal string
  values: xloc.bar_index, xloc.bar_time
  default: xloc.bar_index
- `bgcolor?`: series color
  Background fill color of the box. Optional. Default is `color.blue`.
  types: series color, simple color, input color, const color, literal color
  default: color.blue
- `text?`: series string
  Text drawn inside the box. Optional.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `size?`: series size
  Text size inside the box (`size.auto`, `size.tiny` … `size.huge`). Optional. Default is `size.auto`.
  The old name `text_size` still compiles for now, with a deprecation warning.
  types: series size, simple size, input size, const size, literal size
  default: size.auto
- `textcolor?`: series color
  Text color inside the box. Optional. Default is `color.white`.
  The old name `text_color` still compiles for now, with a deprecation warning.
  types: series color, simple color, input color, const color, literal color
  default: color.white
- `texthalign?`: series string
  Horizontal text alignment: left, center, or right. Default is center.
  The old name `text_halign` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: text.align_left, text.align_center, text.align_right
  default: text.align_center
- `textvalign?`: series string
  Vertical text alignment: top, center, or bottom. Default is center.
  The old name `text_valign` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: text.align_top, text.align_center, text.align_bottom
  default: text.align_center
- `textwrap?`: series string
  Text wrap mode (`none` or `word`). Default is `none`.
  The old name `text_wrap` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: "none", "word"
  default: "none"
- `text_font_family?`: input font
  Font family for box text (`font.family_default` or `font.family_monospace`). Optional. Default is `font.family_default`.
  types: input font, const font, literal font
  default: font.family_default
- `force_overlay?`: const bool
  If true, draw on the main pane even when the script is not overlay. Default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `text_formatting?`: series string
  Text formatting (none, bold, italic). Optional.
  types: series string, simple string, input string, const string, literal string
  values: text.format_bold, text.format_italic, text.format_none
  default: text.format_none

### returnedType

series box

### returnDesc

The ID of the created box.

### notes

- The `size` argument takes a `size.*` constant (`size.auto`, `size.tiny`, `size.small`, `size.normal`, `size.large`, `size.huge`). A string such as "small" still compiles, with a deprecation warning: write the constant.
- The old names `text_color`, `text_halign`, `text_valign`, `text_size` and `text_wrap` still compile, with a deprecation warning that names the new spelling (`textcolor`, `texthalign`, `textvalign`, `size`, `textwrap`). Giving both spellings of one argument is an error. Write the new names.
- A string that is not a size name, such as "giant", stops the compiler with the error "internal validator error": write a `size.*` constant.
- The two forms have different default colors. Given `left`, `top`, `right` and `bottom`, `border_color`, `bgcolor` and `textcolor` default to `#483D8B`. Given two chartPoint corners, `border_color` and `bgcolor` default to `color.blue` and `textcolor` to `color.white`.

### example

```lipi
//@lipi=2
indicator("box.new Example", overlay=true)
if barstate.islast {
    box.new(chartPoint.from_index(bar_index[10], high), chartPoint.from_index(bar_index, low), border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
}
```

### id

function:box.new~2

## box.set_bgcolor (function)

Sets a box's background color.

### syntax

```
box.set_bgcolor(series box id, series color color) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
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
indicator("box.set_bgcolor Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_bgcolor(b, color.new(color.green, 0.8))
}
```

### id

function:box.set_bgcolor

## box.set_border_color (function)

Sets a box's border color.

### syntax

```
box.set_border_color(series box id, series color color) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
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
indicator("box.set_border_color Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_border_color(b, color.black)
}
```

### id

function:box.set_border_color

## box.set_border_style (function)

Sets a box's border style.

### syntax

```
box.set_border_style(series box id, series string style) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
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
indicator("box.set_border_style Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_border_style(b, line.style_dashed)
}
```

### id

function:box.set_border_style

## box.set_border_width (function)

Sets a box's border width in pixels.

### syntax

```
box.set_border_width(series box id, series int width) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
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
indicator("box.set_border_width Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_border_width(b, 2)
}
```

### id

function:box.set_border_width

## box.set_bottom (function)

Sets a box's bottom price.

### syntax

```
box.set_bottom(series box id, series float bottom) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `bottom`: series float
  Bottom price of the box.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_bottom Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_bottom(b, low)
}
```

### id

function:box.set_bottom

## box.set_bottom_right_point (function)

Sets a box's bottom-right corner from a chartPoint.

### syntax

```
box.set_bottom_right_point(series box id, series chartPoint point) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `point`: series chartPoint
  A chartPoint.
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_bottom_right_point Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_bottom_right_point(b, chartPoint.from_index(bar_index, low))
}
```

### id

function:box.set_bottom_right_point

## box.set_extend (function)

Sets whether a box extends past its corners.

### syntax

```
box.set_extend(series box id, series string extend) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
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
indicator("box.set_extend Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_extend(b, extend.none)
}
```

### id

function:box.set_extend

## box.set_left (function)

Sets a box's left x-coordinate.

### syntax

```
box.set_left(series box id, series int left) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `left`: series int
  Left x-coordinate of the box.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_left Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_left(b, bar_index[5])
}
```

### id

function:box.set_left

## box.set_lefttop (function)

Sets a box's left x-coordinate and top price.

### syntax

```
box.set_lefttop(series box id, series int left, series float top) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `left`: series int
  Left x-coordinate of the box.
  types: series int, simple int, input int, const int, literal int
- `top`: series float
  Top price of the box.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_lefttop Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_lefttop(b, bar_index[5], high)
}
```

### id

function:box.set_lefttop

## box.set_right (function)

Sets a box's right x-coordinate.

### syntax

```
box.set_right(series box id, series int right) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `right`: series int
  Right x-coordinate of the box.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_right Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_right(b, bar_index)
}
```

### id

function:box.set_right

## box.set_rightbottom (function)

Sets a box's right x-coordinate and bottom price.

### syntax

```
box.set_rightbottom(series box id, series int right, series float bottom) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `right`: series int
  Right x-coordinate of the box.
  types: series int, simple int, input int, const int, literal int
- `bottom`: series float
  Bottom price of the box.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_rightbottom Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_rightbottom(b, bar_index, low)
}
```

### id

function:box.set_rightbottom

## box.set_text (function)

Sets a box's text.

### syntax

```
box.set_text(series box id, series string text) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `text`: series string
  Text string.
  types: series string, simple string, input string, const string, literal string

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_text Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_text(b, "Zone")
}
```

### id

function:box.set_text

## box.set_text_color (function)

Sets a box's text color.

### syntax

```
box.set_text_color(series box id, series color color) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
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
indicator("box.set_text_color Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_text_color(b, color.white)
}
```

### id

function:box.set_text_color

## box.set_text_font_family (function)

Sets a box's text font family.

### syntax

```
box.set_text_font_family(series box id, input font family) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `family`: input font
  Font family (`font.family_default` or `font.family_monospace`).
  types: input font, const font, literal font

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_text_font_family Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, bgcolor=color.new(color.blue, 0.8))
    box.set_text_font_family(b, font.family_default)
}
```

### id

function:box.set_text_font_family

## box.set_text_formatting (function)

Sets a box's text formatting.

### syntax

```
box.set_text_formatting(series box id, series string formatting) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `formatting`: series string
  Text formatting: `text.format_none`, `text.format_bold` or `text.format_italic`.
  types: series string, simple string, input string, const string, literal string
  values: text.format_bold, text.format_italic, text.format_none

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_text_formatting Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_text_formatting(b, "bold")
}
```

### id

function:box.set_text_formatting

## box.set_text_halign (function)

Sets a box's horizontal text alignment.

### syntax

```
box.set_text_halign(series box id, series string align) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `align`: series string
  Horizontal text alignment: `text.align_left`, `text.align_center` or `text.align_right`.
  types: series string, simple string, input string, const string, literal string
  values: text.align_left, text.align_center, text.align_right

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_text_halign Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_text_halign(b, "center")
}
```

### id

function:box.set_text_halign

## box.set_text_size (function)

Sets a box's text size.

### syntax

```
box.set_text_size(series box id, series size size) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `size`: series size
  Text size: a `size.*` constant. A string such as "small" still compiles, with a deprecation warning.
  types: series size, simple size, input size, const size, literal size

### returnedType

void

### returnDesc

void

### notes

- The `size` argument takes a `size.*` constant (`size.auto`, `size.tiny`, `size.small`, `size.normal`, `size.large`, `size.huge`). A string such as "small" still compiles, with a deprecation warning: write the constant.

### example

```lipi
//@lipi=2
indicator("box.set_text_size Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_text_size(b, size.normal)
}
```

### id

function:box.set_text_size

## box.set_text_valign (function)

Sets a box's vertical text alignment.

### syntax

```
box.set_text_valign(series box id, series string align) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `align`: series string
  Vertical text alignment: `text.align_top`, `text.align_center` or `text.align_bottom`.
  types: series string, simple string, input string, const string, literal string
  values: text.align_top, text.align_center, text.align_bottom

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_text_valign Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_text_valign(b, "center")
}
```

### id

function:box.set_text_valign

## box.set_text_wrap (function)

Sets whether a box's text wraps.

### syntax

```
box.set_text_wrap(series box id, series string wrap) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `wrap`: series string
  Text wrap mode (`none` or `word`).
  types: series string, simple string, input string, const string, literal string
  values: "none", "word"

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_text_wrap Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_text_wrap(b, "auto")
}
```

### id

function:box.set_text_wrap

## box.set_top (function)

Sets a box's top price.

### syntax

```
box.set_top(series box id, series float top) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `top`: series float
  Top price of the box.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_top Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_top(b, high)
}
```

### id

function:box.set_top

## box.set_top_left_point (function)

Sets a box's top-left corner from a chartPoint.

### syntax

```
box.set_top_left_point(series box id, series chartPoint point) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `point`: series chartPoint
  A chartPoint.
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("box.set_top_left_point Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_top_left_point(b, chartPoint.from_index(bar_index[10], high))
}
```

### id

function:box.set_top_left_point

## box.set_xloc (function)

Sets whether a box's x-coordinates are bar indexes or times.

### syntax

```
box.set_xloc(series box id, series int left, series int right, series string xloc) → void
```

### args

- `id`: series box
  Drawing object to modify or query.
  types: series box, simple box, input box, const box, literal box
- `left`: series int
  Left x-coordinate of the box.
  types: series int, simple int, input int, const int, literal int
- `right`: series int
  Right x-coordinate of the box.
  types: series int, simple int, input int, const int, literal int
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
indicator("box.set_xloc Example", overlay=true)
if barstate.islast {
    b = box.new(bar_index[10], high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.8), textcolor=color.white)
    box.set_xloc(b, bar_index[10], bar_index, xloc.bar_index)
}
```

### id

function:box.set_xloc
