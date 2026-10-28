Contents: text (library) · text.align_bottom (constant) · text.align_center (constant) · text.align_left (constant) · text.align_right (constant) · text.align_top (constant) · text.format_bold (constant) · text.format_italic (constant) · text.format_none (constant)

# text

## text (library)

Named constants for text alignment (`text.align_*`) and formatting (`text.format_*`) used by label, box, and table.

On boxes and tables, pass alignment to `texthalign` and `textvalign` (not the older `text_halign` / `text_valign` names).

### example

```lipi
//@lipi=2
indicator("text Example", overlay=true)
if barstate.islast {
    box.new(bar_index - 10, high, bar_index, low, border_color=color.blue, bgcolor=color.new(color.blue, 0.2), text="Hi", textcolor=color.white, texthalign=text.align_center, textvalign=text.align_bottom, text_formatting=text.format_bold)
    label.new(bar_index, high, "BUY", text_formatting=text.format_italic)
}
```

### id

library:text

## text.align_bottom (constant)

Vertical text alignment constant that aligns text to the bottom of the container.

### type

const string

### example

```lipi
//@lipi=2
indicator("text.align_bottom Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close", width=10, height=5, textvalign=text.align_bottom, textcolor=color.white)
}
```

### id

constant:text.align_bottom

## text.align_center (constant)

Text alignment constant that centers text horizontally or vertically in the container.

### type

const string

### example

```lipi
//@lipi=2
indicator("text.align_center Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close", width=10, height=5, texthalign=text.align_center, textcolor=color.white)
}
```

### id

constant:text.align_center

## text.align_left (constant)

Horizontal text alignment constant that aligns text to the left of the container.

### type

const string

### example

```lipi
//@lipi=2
indicator("text.align_left Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close", width=10, height=5, texthalign=text.align_left, textcolor=color.white)
}
```

### id

constant:text.align_left

## text.align_right (constant)

Horizontal text alignment constant that aligns text to the right of the container.

### type

const string

### example

```lipi
//@lipi=2
indicator("text.align_right Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close", width=10, height=5, texthalign=text.align_right, textcolor=color.white)
}
```

### id

constant:text.align_right

## text.align_top (constant)

Vertical text alignment constant that aligns text to the top of the container.

### type

const string

### example

```lipi
//@lipi=2
indicator("text.align_top Example", overlay=true)
if barstate.islast {
    t = table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close", width=10, height=5, textvalign=text.align_top, textcolor=color.white)
}
```

### id

constant:text.align_top

## text.format_bold (constant)

Text formatting constant that renders text in bold.

### type

const string

### example

```lipi
//@lipi=2
indicator("text.format_bold Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Close: " + str.tostring(math.round(close, 2)), text_formatting=text.format_bold)
}
```

### id

constant:text.format_bold

## text.format_italic (constant)

Text formatting constant that renders text in italic.

### type

const string

### example

```lipi
//@lipi=2
indicator("text.format_italic Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Close: " + str.tostring(math.round(close, 2)), text_formatting=text.format_italic)
}
```

### id

constant:text.format_italic

## text.format_none (constant)

Text formatting constant that applies no special formatting.

### type

const string

### example

```lipi
//@lipi=2
indicator("text.format_none Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Close: " + str.tostring(math.round(close, 2)), text_formatting=text.format_none)
}
```

### id

constant:text.format_none
