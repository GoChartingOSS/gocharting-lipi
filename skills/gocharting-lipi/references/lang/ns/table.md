Contents: table (library) · table (type) · table.all (variable) · table.all (function) · table.cell (function) · table.cell_set_bgcolor (function) · table.cell_set_height (function) · table.cell_set_text (function) · table.cell_set_text_color (function) · table.cell_set_text_font_family (function) · table.cell_set_text_formatting (function) · table.cell_set_text_halign (function) · table.cell_set_text_size (function) · table.cell_set_text_valign (function) · table.cell_set_tooltip (function) · table.cell_set_width (function) · table.clear (function) · table.delete (function) · table.merge_cells (function) · table.new (function) · table.set_bgcolor (function) · table.set_border_color (function) · table.set_border_width (function) · table.set_frame_color (function) · table.set_frame_width (function) · table.set_position (function)

# table

## table (library)

Functions for screen-anchored tables. Create with table.new, fill cells with table.cell, merge with table.merge_cells. One table per position.*; a later table.new at the same position deletes the older table. Maximum of 9 tables.

### notes

- A `table.<name>(t, ...)` function can also be called on the table as `t.<name>(...)`, for example `t.cell(0, 0, "a")`.

### example

```lipi
//@lipi=2
indicator("table Library Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_right, 2, 2, bgcolor=color.gray, border_width=1, border_color=color.black)
    table.cell(t, 0, 0, text="High", textcolor=color.white)
    table.cell(t, 1, 0, text=str.tostring(high), textcolor=color.white)
    table.cell(t, 0, 1, text="Low", textcolor=color.white)
    table.cell(t, 1, 1, text=str.tostring(low), textcolor=color.white)
}
```

### id

library:table

## table (type)

A screen-anchored grid (not bar/price anchored). At most one live table is shown per position.*; creating another table at the same position deletes the previous one. Cells are created with table.cell; merged cells store colspan/rowspan on the origin cell.

### example

```lipi
//@lipi=2
indicator("Table Type Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text=str.tostring(close))
}
```

### id

type:table

## table.all (variable)

Array of all currently existing tables, from oldest to newest. Hidden/stacked tables do not exist: only the live table at each position is present. Maximum of 9 tables (one per position.*).

### type

series array<table>

### example

```lipi
//@lipi=2
indicator("table.all Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text=str.tostring(array.length(table.all)))
}
```

### id

variable:table.all

## table.all (function)

Returns the array of all existing table objects (same as the table.all variable). One live table per position.

### syntax

```
table.all() → series array<table>
```

### returnedType

series array<table>

### returnDesc

An array of table IDs, oldest to newest.

### example

```lipi
//@lipi=2
indicator("table.all Function Example")
plot(array.length(table.all), title="Tables")
```

### id

function:table.all

## table.cell (function)

Defines a cell at (column, row). If that cell was previously merged as an origin, its colspan/rowspan is kept. Covered cells from a merge are not created as placeholders.

### syntax

```
table.cell(series table id, series int column, series int row, series string text, series float width, series float height, series color textcolor, series string texthalign, series string textvalign, series size size, series color bgcolor, series string tooltip, input font text_font_family, series string text_formatting) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column index.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row index.
  types: series int, simple int, input int, const int, literal int
- `text?`: series string
  Cell text. Default is an empty string.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `width?`: series float
  Cell width as a percentage of the pane. Default is 0 (auto).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: 0
- `height?`: series float
  Cell height as a percentage of the pane. Default is 0 (auto).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: 0
- `textcolor?`: series color
  Text color. Optional.
  The old name `text_color` still compiles for now, with a deprecation warning.
  types: series color, simple color, input color, const color, literal color
  default: na
- `texthalign?`: series string
  Horizontal text align: left, center, or right. Default is center.
  The old name `text_halign` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: text.align_left, text.align_center, text.align_right
  default: "center"
- `textvalign?`: series string
  Vertical text align: top, center, or bottom. Default is center.
  The old name `text_valign` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: text.align_top, text.align_center, text.align_bottom
  default: "center"
- `size?`: series size
  Cell text size (`size.auto`, `size.tiny` … `size.huge`). Optional. Default is `size.normal`.
  The old name `text_size` still compiles for now, with a deprecation warning.
  types: series size, simple size, input size, const size, literal size
  default: size.normal
- `bgcolor?`: series color
  Cell background color. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `tooltip?`: series string
  Tooltip text. Default is an empty string.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `text_font_family?`: input font
  Font family (`font.family_default` or `font.family_monospace`). Optional. Default is `font.family_default`.
  types: input font, const font, literal font
  default: font.family_default
- `text_formatting?`: series string
  Text formatting. Default is none.
  types: series string, simple string, input string, const string, literal string
  values: text.format_bold, text.format_italic, text.format_none
  default: "none"

### returnedType

void

### returnDesc

void

### notes

- The `size` argument takes a `size.*` constant (`size.auto`, `size.tiny`, `size.small`, `size.normal`, `size.large`, `size.huge`). A string such as "small" still compiles, with a deprecation warning: write the constant.
- The old names `text_color`, `text_halign`, `text_valign` and `text_size` still compile, with a deprecation warning that names the new spelling (`textcolor`, `texthalign`, `textvalign`, `size`). Giving both spellings of one argument is an error. Write the new names.
- A string that is not a size name, such as "giant", stops the compiler with the error "internal validator error": write a `size.*` constant.

### example

```lipi
//@lipi=2
indicator("table.merge_cells example")
SMA50 = talib.sma(close, 50)
SMA100 = talib.sma(close, 100)
SMA200 = talib.sma(close, 200)
if barstate.islast {
    maTable = table.new(position.bottom_right, 3, 3, bgcolor=color.gray, border_width=1, border_color=color.black)
    table.cell(maTable, 0, 0, text="SMA Table")
    table.merge_cells(maTable, 0, 0, 2, 0)
    table.cell(maTable, 0, 1, text="SMA 50")
    table.cell(maTable, 1, 1, text="SMA 100")
    table.cell(maTable, 2, 1, text="SMA 200")
    table.cell(maTable, 0, 2, bgcolor=color.white, text=str.tostring(SMA50))
    table.cell(maTable, 1, 2, bgcolor=color.white, text=str.tostring(SMA100))
    table.cell(maTable, 2, 2, bgcolor=color.white, text=str.tostring(SMA200))
}
```

### id

function:table.cell

## table.cell_set_bgcolor (function)

Sets the background color of an existing cell. No-op if the cell does not exist.

### syntax

```
table.cell_set_bgcolor(series table id, series int column, series int row, series color color) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `color`: series color
  New cell background color.
  types: series color, simple color, input color, const color, literal color

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.cell_set_bgcolor Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hi")
    table.cell_set_bgcolor(t, 0, 0, color.green)
}
```

### id

function:table.cell_set_bgcolor

## table.cell_set_height (function)

Sets the height of an existing cell as a percentage of the pane.

### syntax

```
table.cell_set_height(series table id, series int column, series int row, series float height) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `height`: series float
  Height as a percentage of the pane.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.cell_set_height Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hello")
    table.cell_set_height(t, 0, 0, 5)
}
```

### id

function:table.cell_set_height

## table.cell_set_text (function)

Sets the text of an existing cell. No-op if the cell does not exist.

### syntax

```
table.cell_set_text(series table id, series int column, series int row, series string text) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `text`: series string
  New cell text.
  types: series string, simple string, input string, const string, literal string

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.cell_set_text Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="")
    table.cell_set_text(t, 0, 0, str.tostring(close))
}
```

### id

function:table.cell_set_text

## table.cell_set_text_color (function)

Sets the text color of an existing cell.

### syntax

```
table.cell_set_text_color(series table id, series int column, series int row, series color color) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `color`: series color
  New text color.
  The old name `text_color` still compiles for now, with a deprecation warning.
  types: series color, simple color, input color, const color, literal color

### returnedType

void

### returnDesc

void

### notes

- The old name `text_color` still compiles, with a deprecation warning that names `color`. Write the new name.

### example

```lipi
//@lipi=2
indicator("table.cell_set_text_color Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text=str.tostring(close))
    table.cell_set_text_color(t, 0, 0, color.white)
}
```

### id

function:table.cell_set_text_color

## table.cell_set_text_font_family (function)

Sets the font family of an existing cell.

### syntax

```
table.cell_set_text_font_family(series table id, series int column, series int row, input font text_font_family) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `text_font_family`: input font
  Font family (`font.family_default` or `font.family_monospace`).
  types: input font, const font, literal font

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.cell_set_text_font_family Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hello")
    table.cell_set_text_font_family(t, 0, 0, font.family_default)
}
```

### id

function:table.cell_set_text_font_family

## table.cell_set_text_formatting (function)

Sets text formatting of an existing cell (for example none, bold, italic).

### syntax

```
table.cell_set_text_formatting(series table id, series int column, series int row, series string text_formatting) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `text_formatting`: series string
  Formatting string.
  types: series string, simple string, input string, const string, literal string
  values: text.format_bold, text.format_italic, text.format_none

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.cell_set_text_formatting Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hello")
    table.cell_set_text_formatting(t, 0, 0, "bold")
}
```

### id

function:table.cell_set_text_formatting

## table.cell_set_text_halign (function)

Sets horizontal text alignment of an existing cell: left, center, or right.

### syntax

```
table.cell_set_text_halign(series table id, series int column, series int row, series string texthalign) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `texthalign`: series string
  Horizontal alignment: left, center, or right.
  The old name `text_halign` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: text.align_left, text.align_center, text.align_right

### returnedType

void

### returnDesc

void

### notes

- The old name `text_halign` still compiles, with a deprecation warning that names `texthalign`. Write the new name.

### example

```lipi
//@lipi=2
indicator("table.cell_set_text_halign Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hello")
    table.cell_set_text_halign(t, 0, 0, "left")
}
```

### id

function:table.cell_set_text_halign

## table.cell_set_text_size (function)

Sets the text size of an existing cell.

### syntax

```
table.cell_set_text_size(series table id, series int column, series int row, series size size) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `size`: series size
  Text size (`size.auto`, `size.tiny` … `size.huge`).
  The old name `text_size` still compiles for now, with a deprecation warning.
  types: series size, simple size, input size, const size, literal size

### returnedType

void

### returnDesc

void

### notes

- The `size` argument takes a `size.*` constant (`size.auto`, `size.tiny`, `size.small`, `size.normal`, `size.large`, `size.huge`). A string such as "small" still compiles, with a deprecation warning: write the constant.
- The old name `text_size` still compiles, with a deprecation warning that names `size`. Write the new name.

### example

```lipi
//@lipi=2
indicator("table.cell_set_text_size Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hello")
    table.cell_set_text_size(t, 0, 0, size.large)
}
```

### id

function:table.cell_set_text_size

## table.cell_set_text_valign (function)

Sets vertical text alignment of an existing cell: top, center, or bottom.

### syntax

```
table.cell_set_text_valign(series table id, series int column, series int row, series string textvalign) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `textvalign`: series string
  Vertical alignment: top, center, or bottom.
  The old name `text_valign` still compiles for now, with a deprecation warning.
  types: series string, simple string, input string, const string, literal string
  values: text.align_top, text.align_center, text.align_bottom

### returnedType

void

### returnDesc

void

### notes

- The old name `text_valign` still compiles, with a deprecation warning that names `textvalign`. Write the new name.

### example

```lipi
//@lipi=2
indicator("table.cell_set_text_valign Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hello")
    table.cell_set_text_valign(t, 0, 0, "top")
}
```

### id

function:table.cell_set_text_valign

## table.cell_set_tooltip (function)

Sets the tooltip of an existing cell.

### syntax

```
table.cell_set_tooltip(series table id, series int column, series int row, series string tooltip) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
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
indicator("table.cell_set_tooltip Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text=str.tostring(close))
    table.cell_set_tooltip(t, 0, 0, "Last close")
}
```

### id

function:table.cell_set_tooltip

## table.cell_set_width (function)

Sets the width of an existing cell as a percentage of the pane.

### syntax

```
table.cell_set_width(series table id, series int column, series int row, series float width) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `column`: series int
  0-based column.
  types: series int, simple int, input int, const int, literal int
- `row`: series int
  0-based row.
  types: series int, simple int, input int, const int, literal int
- `width`: series float
  Width as a percentage of the pane.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.cell_set_width Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hello")
    table.cell_set_width(t, 0, 0, 10)
}
```

### id

function:table.cell_set_width

## table.clear (function)

Removes cells in the inclusive rectangle. `end_column` and `end_row` are required; leaving either out is an error. Clearing a merge origin drops that merge.

### syntax

```
table.clear(series table id, series int start_column, series int start_row, series int end_column, series int end_row) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `start_column`: series int
  Column of one corner (0-based).
  types: series int, simple int, input int, const int, literal int
- `start_row`: series int
  Row of one corner (0-based).
  types: series int, simple int, input int, const int, literal int
- `end_column`: series int
  Column of the opposite corner (0-based). Required argument.
  types: series int, simple int, input int, const int, literal int
- `end_row`: series int
  Row of the opposite corner (0-based). Required argument.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.clear Example")
if barstate.islast {
    t = table.new(position.top_right, 2, 2)
    table.cell(t, 0, 0, text="A")
    table.cell(t, 1, 0, text="B")
    table.clear(t, 0, 0, 1, 0)
}
```

### id

function:table.clear

## table.delete (function)

Deletes a table. The position slot becomes empty.

### syntax

```
table.delete(series table id) → void
```

### args

- `id`: series table
  Table object to delete.
  types: series table, simple table, input table, const table, literal table

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.delete Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Bye")
    table.delete(t)
}
```

### id

function:table.delete

## table.merge_cells (function)

Merges the inclusive rectangle from (start_column, start_row) to (end_column, end_row) into the top-left origin cell. That cell gets colspan/rowspan; other cells in the rect are removed. Corners may be passed in any order. A later overlapping merge clears the old origin span.

### syntax

```
table.merge_cells(series table id, series int start_column, series int start_row, series int end_column, series int end_row) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `start_column`: series int
  Column of one corner of the merge rect (0-based).
  types: series int, simple int, input int, const int, literal int
- `start_row`: series int
  Row of one corner of the merge rect (0-based).
  types: series int, simple int, input int, const int, literal int
- `end_column`: series int
  Column of the opposite corner (0-based).
  types: series int, simple int, input int, const int, literal int
- `end_row`: series int
  Row of the opposite corner (0-based).
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.merge_cells example")
SMA50 = talib.sma(close, 50)
SMA100 = talib.sma(close, 100)
SMA200 = talib.sma(close, 200)
if barstate.islast {
    maTable = table.new(position.bottom_right, 3, 3, bgcolor=color.gray, border_width=1, border_color=color.black)
    table.cell(maTable, 0, 0, text="SMA Table")
    table.merge_cells(maTable, 0, 0, 2, 0)
    table.cell(maTable, 0, 1, text="SMA 50")
    table.cell(maTable, 1, 1, text="SMA 100")
    table.cell(maTable, 2, 1, text="SMA 200")
    table.cell(maTable, 0, 2, bgcolor=color.white, text=str.tostring(SMA50))
    table.cell(maTable, 1, 2, bgcolor=color.white, text=str.tostring(SMA100))
    table.cell(maTable, 2, 2, bgcolor=color.white, text=str.tostring(SMA200))
}
```

### id

function:table.merge_cells

## table.new (function)

Creates a new table at a chart position. If a table already exists at that position, the previous table is deleted. At most 9 tables can exist (one per position.*).

### syntax

```
table.new(series string position, series int columns, series int rows, series color bgcolor, series color frame_color, series int frame_width, series color border_color, series int border_width, const bool force_overlay) → series table
```

### args

- `position`: series string
  Where to place the table. One of position.top_left, top_center, top_right, middle_left, middle_center, middle_right, bottom_left, bottom_center, bottom_right.
  types: series string, simple string, input string, const string, literal string
  values: position.bottom_center, position.bottom_left, position.bottom_right, position.middle_center, position.middle_left, position.middle_right, position.top_center, position.top_left, position.top_right
- `columns`: series int
  Number of columns. Must be >= 1.
  types: series int, simple int, input int, const int, literal int
- `rows`: series int
  Number of rows. Must be >= 1.
  types: series int, simple int, input int, const int, literal int
- `bgcolor?`: series color
  Background color of the table. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `frame_color?`: series color
  Outer frame color. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `frame_width?`: series int
  Outer frame width in pixels. Default is 0.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `border_color?`: series color
  Inner cell-border color. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `border_width?`: series int
  Inner cell-border width in pixels. Default is 0.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `force_overlay?`: const bool
  If true, draw on the main pane even when the script is not overlay. Default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false

### returnedType

series table

### returnDesc

The ID of the created table, or na if columns/rows are less than 1.

### example

```lipi
//@lipi=2
indicator("table.merge_cells example")
SMA50 = talib.sma(close, 50)
SMA100 = talib.sma(close, 100)
SMA200 = talib.sma(close, 200)
if barstate.islast {
    maTable = table.new(position.bottom_right, 3, 3, bgcolor=color.gray, border_width=1, border_color=color.black)
    table.cell(maTable, 0, 0, text="SMA Table")
    table.merge_cells(maTable, 0, 0, 2, 0)
    table.cell(maTable, 0, 1, text="SMA 50")
    table.cell(maTable, 1, 1, text="SMA 100")
    table.cell(maTable, 2, 1, text="SMA 200")
    table.cell(maTable, 0, 2, bgcolor=color.white, text=str.tostring(SMA50))
    table.cell(maTable, 1, 2, bgcolor=color.white, text=str.tostring(SMA100))
    table.cell(maTable, 2, 2, bgcolor=color.white, text=str.tostring(SMA200))
}
```

### id

function:table.new

## table.set_bgcolor (function)

Sets the table background color.

### syntax

```
table.set_bgcolor(series table id, series color color) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `color`: series color
  New table background color.
  types: series color, simple color, input color, const color, literal color

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.set_bgcolor Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hi")
    table.set_bgcolor(t, color.navy)
}
```

### id

function:table.set_bgcolor

## table.set_border_color (function)

Sets the inner cell-border color.

### syntax

```
table.set_border_color(series table id, series color color) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `color`: series color
  New border color.
  types: series color, simple color, input color, const color, literal color

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.set_border_color Example")
if barstate.islast {
    t = table.new(position.top_right, 2, 1, border_width=1)
    table.cell(t, 0, 0, text="A")
    table.cell(t, 1, 0, text="B")
    table.set_border_color(t, color.black)
}
```

### id

function:table.set_border_color

## table.set_border_width (function)

Sets the inner cell-border width in pixels.

### syntax

```
table.set_border_width(series table id, series int width) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `width`: series int
  Border width in pixels.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.set_border_width Example")
if barstate.islast {
    t = table.new(position.top_right, 2, 1)
    table.cell(t, 0, 0, text="A")
    table.cell(t, 1, 0, text="B")
    table.set_border_width(t, 1)
}
```

### id

function:table.set_border_width

## table.set_frame_color (function)

Sets the outer frame color.

### syntax

```
table.set_frame_color(series table id, series color color) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `color`: series color
  New frame color.
  types: series color, simple color, input color, const color, literal color

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.set_frame_color Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1, frame_width=1)
    table.cell(t, 0, 0, text="Hi")
    table.set_frame_color(t, color.white)
}
```

### id

function:table.set_frame_color

## table.set_frame_width (function)

Sets the outer frame width in pixels.

### syntax

```
table.set_frame_width(series table id, series int width) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `width`: series int
  Frame width in pixels.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.set_frame_width Example")
if barstate.islast {
    t = table.new(position.top_right, 1, 1)
    table.cell(t, 0, 0, text="Hi")
    table.set_frame_width(t, 2)
}
```

### id

function:table.set_frame_width

## table.set_position (function)

Moves a table to a new position. If another table already occupies that position, it is deleted. The previous slot is left empty.

### syntax

```
table.set_position(series table id, series string position) → void
```

### args

- `id`: series table
  Table object.
  types: series table, simple table, input table, const table, literal table
- `position`: series string
  New position.* value.
  types: series string, simple string, input string, const string, literal string
  values: position.bottom_center, position.bottom_left, position.bottom_right, position.middle_center, position.middle_left, position.middle_right, position.top_center, position.top_left, position.top_right

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("table.set_position Example")
if barstate.islast {
    t = table.new(position.top_left, 1, 1)
    table.cell(t, 0, 0, text="Moved")
    table.set_position(t, position.bottom_right)
}
```

### id

function:table.set_position
