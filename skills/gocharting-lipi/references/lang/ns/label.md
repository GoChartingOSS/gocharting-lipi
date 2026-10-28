Contents: label (library) · label (type) · label.all (variable) · label.all (function) · label.copy (function) · label.delete (function) · label.get_text (function) · label.get_x (function) · label.get_y (function) · label.new (function) · label.set_color (function) · label.set_point (function) · label.set_size (function) · label.set_style (function) · label.set_text (function) · label.set_text_font_family (function) · label.set_text_formatting (function) · label.set_textalign (function) · label.set_textcolor (function) · label.set_tooltip (function) · label.set_x (function) · label.set_xloc (function) · label.set_xy (function) · label.set_y (function) · label.set_yloc (function) · label.style_arrowdown (constant) · label.style_arrowup (constant) · label.style_circle (constant) · label.style_cross (constant) · label.style_diamond (constant) · label.style_flag (constant) · label.style_label_center (constant) · label.style_label_down (constant) · label.style_label_left (constant) · label.style_label_lower_left (constant) · label.style_label_lower_right (constant) · label.style_label_right (constant) · label.style_label_up (constant) · label.style_label_upper_left (constant) · label.style_label_upper_right (constant) · label.style_none (constant) · label.style_square (constant) · label.style_text_outline (constant) · label.style_triangledown (constant) · label.style_triangleup (constant) · label.style_xcross (constant)

# label

## label (library)

Functions for creating and mutating text label drawings on the chart.

### notes

- A `label.<name>(l, ...)` function can also be called on the label as `l.<name>(...)`, for example `l.set_text("u")`.

### example

```lipi
//@lipi=2
indicator("label Library Example", overlay=true)
static label lastLabel = label(na)
if barstate.islast {
    if not na(lastLabel) {
        label.delete(lastLabel)
    }
    lastLabel := label.new(bar_index, high, text="Close", style=label.style_label_down, color=color.blue, textcolor=color.white)
    label.set_text(lastLabel, "Close: " + str.tostring(math.round(close, 2)))
}
```

### id

library:label

## label (type)

A text marker anchored to a bar/price. Use label.new to create labels and label.set_* functions to change them.

### example

```lipi
//@lipi=2
indicator("Label Type Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="High", color=color.green, style=label.style_label_down)
}
```

### id

type:label

## label.all (variable)

Array of all currently existing label drawings, from oldest to newest.

### type

series array<label>

### example

```lipi
//@lipi=2
indicator("label.all Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="H")
}
plot(array.length(label.all), title="Label Count")
```

### id

variable:label.all

## label.all (function)

Returns the array of all existing label objects (same as label.all).

### syntax

```
label.all() → series array<label>
```

### returnedType

series array<label>

### returnDesc

An array of label IDs, oldest to newest.

### example

```lipi
//@lipi=2
indicator("label.all Example", overlay=true)
plot(array.length(label.all), title="Count")
```

### id

function:label.all

## label.copy (function)

Creates a copy of a label.

### syntax

```
label.copy(series label id) → series label
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label

### returnedType

series label

### returnDesc

The new label ID.

### example

```lipi
//@lipi=2
indicator("label.copy Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    c = label.copy(lb)
}
```

### id

function:label.copy

## label.delete (function)

Deletes a label.

### syntax

```
label.delete(series label id) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.delete Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.delete(lb)
}
```

### id

function:label.delete

## label.get_text (function)

Returns a label's text.

### syntax

```
label.get_text(series label id) → series string
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label

### returnedType

series string

### returnDesc

The label text.

### example

```lipi
//@lipi=2
indicator("label.get_text Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_text(lb, label.get_text(lb) + " " + str.tostring(close))
}
```

### id

function:label.get_text

## label.get_x (function)

Returns a label's x-coordinate.

### syntax

```
label.get_x(series label id) → series int
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label

### returnedType

series int

### returnDesc

X-coordinate.

### example

```lipi
//@lipi=2
indicator("label.get_x Example", overlay=true)
static label lb = label(na)
if barstate.islast {
    lb := label.new(bar_index, high, text="Hi", color=color.green)
}
plot(na(lb) ? na : label.get_x(lb))
```

### id

function:label.get_x

## label.get_y (function)

Returns a label's y-coordinate (price).

### syntax

```
label.get_y(series label id) → series float
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label

### returnedType

series float

### returnDesc

Y-coordinate.

### example

```lipi
//@lipi=2
indicator("label.get_y Example", overlay=true)
static label lb = label(na)
if barstate.islast {
    lb := label.new(bar_index, high, text="Hi", color=color.green)
}
plot(na(lb) ? na : label.get_y(lb))
```

### id

function:label.get_y

## label.new (function)

Creates a label at (x, y) with optional text, color, and style.

### syntax

```
label.new(series int x, series float y, series string text, series string xloc, series string yloc, series color color, series string style, series color textcolor, series size size, series string textalign, series string tooltip, input font text_font_family, const bool force_overlay, series string text_formatting) → series label
```

### args

- `x`: series int
  X-coordinate (bar index or time, depending on xloc).
  types: series int, simple int, input int, const int, literal int
- `y`: series float
  Y-coordinate (price).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `text?`: series string
  Label text. Optional.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `xloc?`: series string
  xloc.bar_index or xloc.bar_time. Default is bar_index.
  types: series string, simple string, input string, const string, literal string
  values: xloc.bar_index, xloc.bar_time
  default: xloc.bar_index
- `yloc?`: series string
  Vertical location relative to the bar (yloc.price, etc.). Optional.
  types: series string, simple string, input string, const string, literal string
  values: yloc.abovebar, yloc.belowbar, yloc.price
  default: yloc.price
- `color?`: series color
  Label background color. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `style?`: series string
  Label style (label.style_*). Optional.
  types: series string, simple string, input string, const string, literal string
  values: label.style_arrowdown, label.style_arrowup, label.style_circle, label.style_cross, label.style_diamond, label.style_flag, label.style_label_center, label.style_label_down, label.style_label_left, label.style_label_lower_left, label.style_label_lower_right, label.style_label_right, label.style_label_up, label.style_label_upper_left, label.style_label_upper_right, label.style_none, label.style_square, label.style_text_outline, label.style_triangledown, label.style_triangleup, label.style_xcross
  default: label.style_label_down
- `textcolor?`: series color
  Text color. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `size?`: series size
  Label size (`size.auto`, `size.tiny` … `size.huge`). Optional. Default is `size.normal`.
  types: series size, simple size, input size, const size, literal size
  default: size.normal
- `textalign?`: series string
  Text alignment: `text.align_left`, `text.align_center` or `text.align_right`.
  types: series string, simple string, input string, const string, literal string
  values: text.align_left, text.align_center, text.align_right
  default: text.align_center
- `tooltip?`: series string
  Tooltip text shown on hover. Optional.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `text_font_family?`: input font
  Font family for label text (`font.family_default` or `font.family_monospace`). Optional. Default is `font.family_default`.
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

series label

### returnDesc

The ID of the created label.

### notes

- The `size` argument takes a `size.*` constant (`size.auto`, `size.tiny`, `size.small`, `size.normal`, `size.large`, `size.huge`). A string such as "small" still compiles, with a deprecation warning: write the constant. A string that is not a size name, such as "giant", stops the compiler with the error "internal validator error".

### example

```lipi
//@lipi=2
indicator("label.new Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="High", color=color.green, style=label.style_label_down, textcolor=color.white)
}
```

### id

function:label.new

## label.set_color (function)

Sets a label's background color.

### syntax

```
label.set_color(series label id, series color color) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
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
indicator("label.set_color Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_color(lb, color.red)
}
```

### id

function:label.set_color

## label.set_point (function)

Sets a label's position from a chartPoint.

### syntax

```
label.set_point(series label id, series chartPoint point) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
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
indicator("label.set_point Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_point(lb, chartPoint.from_index(bar_index, close))
}
```

### id

function:label.set_point

## label.set_size (function)

Sets a label's size.

### syntax

```
label.set_size(series label id, series size size) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `size`: series size
  Label size: a `size.*` constant. A string such as "small" still compiles, with a deprecation warning.
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
indicator("label.set_size Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_size(lb, size.small)
}
```

### id

function:label.set_size

## label.set_style (function)

Sets a label's style (label.style_*).

### syntax

```
label.set_style(series label id, series string style) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `style`: series string
  Style constant for this drawing type.
  types: series string, simple string, input string, const string, literal string
  values: label.style_arrowdown, label.style_arrowup, label.style_circle, label.style_cross, label.style_diamond, label.style_flag, label.style_label_center, label.style_label_down, label.style_label_left, label.style_label_lower_left, label.style_label_lower_right, label.style_label_right, label.style_label_up, label.style_label_upper_left, label.style_label_upper_right, label.style_none, label.style_square, label.style_text_outline, label.style_triangledown, label.style_triangleup, label.style_xcross

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.set_style Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_style(lb, label.style_label_down)
}
```

### id

function:label.set_style

## label.set_text (function)

Sets a label's text.

### syntax

```
label.set_text(series label id, series string text) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
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
indicator("label.set_text Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_text(lb, str.tostring(close))
}
```

### id

function:label.set_text

## label.set_text_font_family (function)

Sets a label's font family.

### syntax

```
label.set_text_font_family(series label id, input font family) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
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
indicator("label.set_text_font_family Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_text_font_family(lb, font.family_default)
}
```

### id

function:label.set_text_font_family

## label.set_text_formatting (function)

Sets a label's text formatting.

### syntax

```
label.set_text_formatting(series label id, series string formatting) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
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
indicator("label.set_text_formatting Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_text_formatting(lb, "bold")
}
```

### id

function:label.set_text_formatting

## label.set_textalign (function)

Sets a label's text alignment.

### syntax

```
label.set_textalign(series label id, series string textalign) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `textalign`: series string
  Text alignment: `text.align_left`, `text.align_center` or `text.align_right`.
  types: series string, simple string, input string, const string, literal string
  values: text.align_left, text.align_center, text.align_right

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.set_textalign Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_textalign(lb, "center")
}
```

### id

function:label.set_textalign

## label.set_textcolor (function)

Sets a label's text color.

### syntax

```
label.set_textcolor(series label id, series color textcolor) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `textcolor`: series color
  Text color.
  types: series color, simple color, input color, const color, literal color

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.set_textcolor Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_textcolor(lb, color.white)
}
```

### id

function:label.set_textcolor

## label.set_tooltip (function)

Sets a label's tooltip.

### syntax

```
label.set_tooltip(series label id, series string tooltip) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `tooltip`: series string
  Tooltip text.
  types: series string, simple string, input string, const string, literal string

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.set_tooltip Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_tooltip(lb, "Last close")
}
```

### id

function:label.set_tooltip

## label.set_x (function)

Sets a label's x-coordinate.

### syntax

```
label.set_x(series label id, series int x) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `x`: series int
  X-coordinate (bar index or time, depending on xloc).
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.set_x Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_x(lb, bar_index)
}
```

### id

function:label.set_x

## label.set_xloc (function)

Sets whether a label's x-coordinate is a bar index or time.

### syntax

```
label.set_xloc(series label id, series int x, series string xloc) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `x`: series int
  X-coordinate (bar index or time, depending on xloc).
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
indicator("label.set_xloc Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_xloc(lb, bar_index, xloc.bar_index)
}
```

### id

function:label.set_xloc

## label.set_xy (function)

Sets a label's x and y coordinates.

### syntax

```
label.set_xy(series label id, series int x, series float y) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `x`: series int
  X-coordinate (bar index or time, depending on xloc).
  types: series int, simple int, input int, const int, literal int
- `y`: series float
  Y-coordinate (price).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.set_xy Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_xy(lb, bar_index, close)
}
```

### id

function:label.set_xy

## label.set_y (function)

Sets a label's y-coordinate (price).

### syntax

```
label.set_y(series label id, series float y) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `y`: series float
  Y-coordinate (price).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.set_y Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_y(lb, close)
}
```

### id

function:label.set_y

## label.set_yloc (function)

Sets a label's vertical location relative to the bar.

### syntax

```
label.set_yloc(series label id, series string yloc) → void
```

### args

- `id`: series label
  Drawing object to modify or query.
  types: series label, simple label, input label, const label, literal label
- `yloc`: series string
  Vertical location relative to the bar (yloc.price, etc.).
  types: series string, simple string, input string, const string, literal string
  values: yloc.abovebar, yloc.belowbar, yloc.price

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("label.set_yloc Example", overlay=true)
if barstate.islast {
    lb = label.new(bar_index, high, text="Hi", color=color.green)
    label.set_yloc(lb, yloc.price)
}
```

### id

function:label.set_yloc

## label.style_arrowdown (constant)

Down-arrow marker style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_arrowdown Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="arrowdown", style=label.style_arrowdown, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_arrowdown

## label.style_arrowup (constant)

Up-arrow marker style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_arrowup Example", overlay=true)
if barstate.islast {
    label.new(bar_index, low, text="arrowup", style=label.style_arrowup, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_arrowup

## label.style_circle (constant)

Circle marker style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_circle Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="circle", style=label.style_circle, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_circle

## label.style_cross (constant)

Cross marker style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_cross Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="cross", style=label.style_cross, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_cross

## label.style_diamond (constant)

Diamond marker style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_diamond Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="diamond", style=label.style_diamond, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_diamond

## label.style_flag (constant)

Flag marker style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_flag Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="flag", style=label.style_flag, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_flag

## label.style_label_center (constant)

Centered label bubble.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_center Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="label_center", style=label.style_label_center, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_center

## label.style_label_down (constant)

Label bubble pointing down.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_down Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="label_down", style=label.style_label_down, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_down

## label.style_label_left (constant)

Label bubble pointing left.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_left Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="label_left", style=label.style_label_left, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_left

## label.style_label_lower_left (constant)

Label bubble in the lower-left.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_lower_left Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="label_lower_left", style=label.style_label_lower_left, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_lower_left

## label.style_label_lower_right (constant)

Label bubble in the lower-right.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_lower_right Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="label_lower_right", style=label.style_label_lower_right, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_lower_right

## label.style_label_right (constant)

Label bubble pointing right.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_right Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="label_right", style=label.style_label_right, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_right

## label.style_label_up (constant)

Label bubble pointing up.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_up Example", overlay=true)
if barstate.islast {
    label.new(bar_index, low, text="label_up", style=label.style_label_up, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_up

## label.style_label_upper_left (constant)

Label bubble in the upper-left.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_upper_left Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="label_upper_left", style=label.style_label_upper_left, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_upper_left

## label.style_label_upper_right (constant)

Label bubble in the upper-right.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_label_upper_right Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="label_upper_right", style=label.style_label_upper_right, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_label_upper_right

## label.style_none (constant)

Label with no visual style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_none Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="none", style=label.style_none, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_none

## label.style_square (constant)

Square marker style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_square Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="square", style=label.style_square, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_square

## label.style_text_outline (constant)

Text with an outline.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_text_outline Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="text_outline", style=label.style_text_outline, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_text_outline

## label.style_triangledown (constant)

Down-pointing triangle marker.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_triangledown Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="triangledown", style=label.style_triangledown, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_triangledown

## label.style_triangleup (constant)

Up-pointing triangle marker.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_triangleup Example", overlay=true)
if barstate.islast {
    label.new(bar_index, low, text="triangleup", style=label.style_triangleup, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_triangleup

## label.style_xcross (constant)

X-cross marker style.

### type

const string

### example

```lipi
//@lipi=2
indicator("label.style_xcross Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="xcross", style=label.style_xcross, color=color.blue, textcolor=color.white)
}
```

### id

constant:label.style_xcross
