Contents: color (library) · color (type) · color.a (function) · color.a (function) · color.a (function) · color.a (function) · color.aqua (constant) · color.b (function) · color.b (function) · color.b (function) · color.b (function) · color.black (constant) · color.blue (constant) · color.from_gradient (function) · color.from_gradient (function) · color.from_gradient (function) · color.from_gradient (function) · color.fuchsia (constant) · color.g (function) · color.g (function) · color.g (function) · color.g (function) · color.gray (constant) · color.green (constant) · color.lime (constant) · color.maroon (constant) · color.navy (constant) · color.new (function) · color.new (function) · color.new (function) · color.new (function) · color.olive (constant) · color.orange (constant) · color.purple (constant) · color.r (function) · color.r (function) · color.r (function) · color.r (function) · color.red (constant) · color.rgb (function) · color.rgb (function) · color.rgb (function) · color.rgb (function) · color.silver (constant) · color.teal (constant) · color.white (constant) · color.yellow (constant)

# color

## color (library)

Seven functions: `color.new` and `color.rgb` build a colour, `color.from_gradient` builds one between two colours, and `color.r`, `color.g`, `color.b` and `color.a` read one apart. Seventeen named colour constants sit alongside them.

Seven is the whole namespace. There is no separate transparency function — set opacity with `color.new` on a colour you already have. `color.new`, `color.r`, `color.g`, `color.b` and `color.a` return `na` when the colour they are given is `na`.

### example

```lipi
//@lipi=2
indicator("color Library Example", overlay=true)
// Green when rising, red when falling, stronger with bigger moves
change = math.abs(close - close[1]) / talib.atr(14)
base = close >= close[1] ? color.green : color.red
bgcolor(color.new(base, math.min(change, 1) * 0.4))
```

### id

library:color

## color (type)

A colour. You can write one directly as a hex literal — six digits for the colour, eight to carry alpha as well.

Seventeen named constants and seven functions in the `color` namespace give you the other ways to get one. No fields.

### example

```lipi
//@lipi=2
indicator("Color Keyword Example", overlay=true)
// Define custom colors using `color` keyword
color bullishColor = color.green
color bearishColor = color.red
color neutralColor = color.gray
// Check conditions
isBullish = close > open
isBearish = close < open
// Assign colors based on conditions
color barColor = isBullish ? bullishColor : isBearish ? bearishColor : neutralColor
// Apply color to bars
barcolor(barColor)
```

### id

type:color

## color.a (function)

Reads the opacity of a colour.

Reading is asymmetric with writing: this one returns a fraction from 0 to 1, while the three component functions return whole numbers from 0 to 255.

### syntax

```
color.a(const color color) → const float
```

### args

- `color`: const color
  Color.
  types: const color, literal color

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("color.a Example", overlay=false)
c = color.new(color.green, 0.4)
plot(color.a(c), title="Opacity (0.4)", color=color.green)
```

### id

function:color.a~1

## color.a (function)

Reads the opacity of a colour.

Reading is asymmetric with writing: this one returns a fraction from 0 to 1, while the three component functions return whole numbers from 0 to 255.

### syntax

```
color.a(input color color) → input float
```

### args

- `color`: input color
  Color.
  types: input color, const color, literal color

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("color.a Example", overlay=false)
c = color.new(color.green, 0.4)
plot(color.a(c), title="Opacity (0.4)", color=color.green)
```

### id

function:color.a~2

## color.a (function)

Reads the opacity of a colour.

Reading is asymmetric with writing: this one returns a fraction from 0 to 1, while the three component functions return whole numbers from 0 to 255.

### syntax

```
color.a(simple color color) → simple float
```

### args

- `color`: simple color
  Color.
  types: simple color, input color, const color, literal color

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("color.a Example", overlay=false)
c = color.new(color.green, 0.4)
plot(color.a(c), title="Opacity (0.4)", color=color.green)
```

### id

function:color.a~3

## color.a (function)

Reads the opacity of a colour.

Reading is asymmetric with writing: this one returns a fraction from 0 to 1, while the three component functions return whole numbers from 0 to 255.

### syntax

```
color.a(series color color) → series float
```

### args

- `color`: series color
  Color.
  types: series color, simple color, input color, const color, literal color

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("color.a Example", overlay=false)
c = color.new(color.green, 0.4)
plot(color.a(c), title="Opacity (0.4)", color=color.green)
```

### id

function:color.a~4

## color.aqua (constant)

It is a predefined constant  for #00FFFF color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.aqua Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.aqua, linewidth=2)
```

### id

constant:color.aqua

## color.b (function)

Reads the blue component of a colour.

Its result is an int from 0 to 255, as with red and green.

### syntax

```
color.b(const color color) → const int
```

### args

- `color`: const color
  Color.
  types: const color, literal color

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("color.b Example", overlay=false)
c = color.rgb(40, 120, 220)
plot(color.b(c), title="Blue Component (220)", color=color.blue)
```

### id

function:color.b~1

## color.b (function)

Reads the blue component of a colour.

Its result is an int from 0 to 255, as with red and green.

### syntax

```
color.b(input color color) → input int
```

### args

- `color`: input color
  Color.
  types: input color, const color, literal color

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("color.b Example", overlay=false)
c = color.rgb(40, 120, 220)
plot(color.b(c), title="Blue Component (220)", color=color.blue)
```

### id

function:color.b~2

## color.b (function)

Reads the blue component of a colour.

Its result is an int from 0 to 255, as with red and green.

### syntax

```
color.b(simple color color) → simple int
```

### args

- `color`: simple color
  Color.
  types: simple color, input color, const color, literal color

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("color.b Example", overlay=false)
c = color.rgb(40, 120, 220)
plot(color.b(c), title="Blue Component (220)", color=color.blue)
```

### id

function:color.b~3

## color.b (function)

Reads the blue component of a colour.

Its result is an int from 0 to 255, as with red and green.

### syntax

```
color.b(series color color) → series int
```

### args

- `color`: series color
  Color.
  types: series color, simple color, input color, const color, literal color

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("color.b Example", overlay=false)
c = color.rgb(40, 120, 220)
plot(color.b(c), title="Blue Component (220)", color=color.blue)
```

### id

function:color.b~4

## color.black (constant)

It is a predefined constant  for #000000 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.black Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.black, linewidth=2)
```

### id

constant:color.black

## color.blue (constant)

It is a predefined constant  for #0000FF color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.blue Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.blue, linewidth=2)
```

### id

constant:color.blue

## color.from_gradient (function)

Returns a color calculated from the linear gradient between bottom_color and top_color based on the relative position of value within the range defined by bottom_value and top_value.

### syntax

```
color.from_gradient(const float value, const float bottom_value, const float top_value, const color bottom_color, const color top_color) → const color
```

### args

- `value`: const float
  Value used to determine the position within the gradient range.
  types: const float, const int, literal int, literal float
- `bottom_value`: const float
  Lower boundary of the gradient range.
  types: const float, const int, literal int, literal float
- `top_value`: const float
  Upper boundary of the gradient range.
  types: const float, const int, literal int, literal float
- `bottom_color`: const color
  Color returned when value equals bottom_value (or is below the range).
  types: const color, literal color
- `top_color`: const color
  Color returned when value equals top_value (or is above the range).
  types: const color, literal color

### returnedType

const color

### returnDesc

const color

### example

```lipi
//@lipi=2
indicator("from_gradient example", overlay=true)
c1 = color.from_gradient(close, low, high, color.yellow, color.lime)
c2 = color.from_gradient(talib.rsi(close, 7), 0, 100, color.rgb(255, 0, 0), color.rgb(0, 255, 0, 0.5))
bgcolor(c1)
```

### id

function:color.from_gradient~1

## color.from_gradient (function)

Returns a color calculated from the linear gradient between bottom_color and top_color based on the relative position of value within the range defined by bottom_value and top_value.

### syntax

```
color.from_gradient(input float value, input float bottom_value, input float top_value, input color bottom_color, input color top_color) → input color
```

### args

- `value`: input float
  Value used to determine the position within the gradient range.
  types: input float, input int, const int, literal int, const float, literal float
- `bottom_value`: input float
  Lower boundary of the gradient range.
  types: input float, input int, const int, literal int, const float, literal float
- `top_value`: input float
  Upper boundary of the gradient range.
  types: input float, input int, const int, literal int, const float, literal float
- `bottom_color`: input color
  Color returned when value equals bottom_value (or is below the range).
  types: input color, const color, literal color
- `top_color`: input color
  Color returned when value equals top_value (or is above the range).
  types: input color, const color, literal color

### returnedType

input color

### returnDesc

input color

### example

```lipi
//@lipi=2
indicator("from_gradient example", overlay=true)
c1 = color.from_gradient(close, low, high, color.yellow, color.lime)
c2 = color.from_gradient(talib.rsi(close, 7), 0, 100, color.rgb(255, 0, 0), color.rgb(0, 255, 0, 0.5))
bgcolor(c1)
```

### id

function:color.from_gradient~2

## color.from_gradient (function)

Returns a color calculated from the linear gradient between bottom_color and top_color based on the relative position of value within the range defined by bottom_value and top_value.

### syntax

```
color.from_gradient(simple float value, simple float bottom_value, simple float top_value, simple color bottom_color, simple color top_color) → simple color
```

### args

- `value`: simple float
  Value used to determine the position within the gradient range.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
- `bottom_value`: simple float
  Lower boundary of the gradient range.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
- `top_value`: simple float
  Upper boundary of the gradient range.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
- `bottom_color`: simple color
  Color returned when value equals bottom_value (or is below the range).
  types: simple color, input color, const color, literal color
- `top_color`: simple color
  Color returned when value equals top_value (or is above the range).
  types: simple color, input color, const color, literal color

### returnedType

simple color

### returnDesc

simple color

### example

```lipi
//@lipi=2
indicator("from_gradient example", overlay=true)
c1 = color.from_gradient(close, low, high, color.yellow, color.lime)
c2 = color.from_gradient(talib.rsi(close, 7), 0, 100, color.rgb(255, 0, 0), color.rgb(0, 255, 0, 0.5))
bgcolor(c1)
```

### id

function:color.from_gradient~3

## color.from_gradient (function)

Returns a color calculated from the linear gradient between bottom_color and top_color based on the relative position of value within the range defined by bottom_value and top_value.

### syntax

```
color.from_gradient(series float value, series float bottom_value, series float top_value, series color bottom_color, series color top_color) → series color
```

### args

- `value`: series float
  Value used to determine the position within the gradient range.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `bottom_value`: series float
  Lower boundary of the gradient range.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `top_value`: series float
  Upper boundary of the gradient range.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `bottom_color`: series color
  Color returned when value equals bottom_value (or is below the range).
  types: series color, simple color, input color, const color, literal color
- `top_color`: series color
  Color returned when value equals top_value (or is above the range).
  types: series color, simple color, input color, const color, literal color

### returnedType

series color

### returnDesc

series color

### example

```lipi
//@lipi=2
indicator("from_gradient example", overlay=true)
c1 = color.from_gradient(close, low, high, color.yellow, color.lime)
c2 = color.from_gradient(talib.rsi(close, 7), 0, 100, color.rgb(255, 0, 0), color.rgb(0, 255, 0, 0.5))
bgcolor(c1)
```

### id

function:color.from_gradient~4

## color.fuchsia (constant)

It is a predefined constant  for #FF00FF color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.fuchsia Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.fuchsia, linewidth=2)
```

### id

constant:color.fuchsia

## color.g (function)

Reads the green component of a colour.

Like the other two component functions, it returns a whole number from 0 to 255.

### syntax

```
color.g(const color color) → const int
```

### args

- `color`: const color
  Color.
  types: const color, literal color

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("color.g Example", overlay=true)
c = color.new(color.red, 0)
g = color.g(c)
plot(g, title="Green component", color=color.green)
```

### id

function:color.g~1

## color.g (function)

Reads the green component of a colour.

Like the other two component functions, it returns a whole number from 0 to 255.

### syntax

```
color.g(input color color) → input int
```

### args

- `color`: input color
  Color.
  types: input color, const color, literal color

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("color.g Example", overlay=true)
c = color.new(color.red, 0)
g = color.g(c)
plot(g, title="Green component", color=color.green)
```

### id

function:color.g~2

## color.g (function)

Reads the green component of a colour.

Like the other two component functions, it returns a whole number from 0 to 255.

### syntax

```
color.g(simple color color) → simple int
```

### args

- `color`: simple color
  Color.
  types: simple color, input color, const color, literal color

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("color.g Example", overlay=true)
c = color.new(color.red, 0)
g = color.g(c)
plot(g, title="Green component", color=color.green)
```

### id

function:color.g~3

## color.g (function)

Reads the green component of a colour.

Like the other two component functions, it returns a whole number from 0 to 255.

### syntax

```
color.g(series color color) → series int
```

### args

- `color`: series color
  Color.
  types: series color, simple color, input color, const color, literal color

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("color.g Example", overlay=true)
c = color.new(color.red, 0)
g = color.g(c)
plot(g, title="Green component", color=color.green)
```

### id

function:color.g~4

## color.gray (constant)

It is a predefined constant  for #808080 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.gray Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.gray, linewidth=2)
```

### id

constant:color.gray

## color.green (constant)

It is a predefined constant  for #008000 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.green Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.green, linewidth=2)
```

### id

constant:color.green

## color.lime (constant)

It is a predefined constant  for #00FF00 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.lime Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.lime, linewidth=2)
```

### id

constant:color.lime

## color.maroon (constant)

It is a predefined constant  for #800000 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.maroon Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.maroon, linewidth=2)
```

### id

constant:color.maroon

## color.navy (constant)

It is a predefined constant  for #000080 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.navy Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.navy, linewidth=2)
```

### id

constant:color.navy

## color.new (function)

Takes a colour and an opacity, and returns that colour at that opacity.

Opacity runs from 0 to 1, where 1 is solid and 0 invisible. A value outside the range is clamped to it rather than rejected. A literal or constant value outside the range gets a warning, for example `opacity 50 is outside 0–1; 1 is solid`.

### syntax

```
color.new(const color color, const float alpha) → const color
```

### args

- `color`: const color
  The base color (e.g., color.red, #00ff7f, color.rgb(255, 0, 0)).
  types: const color, literal color
- `alpha`: const float
  Opacity, from 0 to 1, where 1 is solid and 0 is invisible.
  types: const float, const int, literal int, literal float

### returnedType

const color

### notes

- `alpha` is an opacity from 0 to 1, where 1 is solid and 0 is invisible. It is not a transparency from 0 to 100. A literal or constant value outside 0 to 1 compiles with the warning `opacity 50 is outside 0–1; 1 is solid`.

### example

```lipi
//@lipi=2
indicator("color.new Example", overlay=true)
c = color.new(color.blue, 0.3)
bgcolor(c)
```

### id

function:color.new~1

## color.new (function)

Takes a colour and an opacity, and returns that colour at that opacity.

Opacity runs from 0 to 1, where 1 is solid and 0 invisible. A value outside the range is clamped to it rather than rejected. A literal or constant value outside the range gets a warning, for example `opacity 50 is outside 0–1; 1 is solid`.

### syntax

```
color.new(input color color, input float alpha) → input color
```

### args

- `color`: input color
  The base color (e.g., color.red, #00ff7f, color.rgb(255, 0, 0)).
  types: input color, const color, literal color
- `alpha`: input float
  Opacity, from 0 to 1, where 1 is solid and 0 is invisible.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input color

### notes

- `alpha` is an opacity from 0 to 1, where 1 is solid and 0 is invisible. It is not a transparency from 0 to 100. A literal or constant value outside 0 to 1 compiles with the warning `opacity 50 is outside 0–1; 1 is solid`.

### example

```lipi
//@lipi=2
indicator("color.new Example", overlay=true)
c = color.new(color.blue, 0.3)
bgcolor(c)
```

### id

function:color.new~2

## color.new (function)

Takes a colour and an opacity, and returns that colour at that opacity.

Opacity runs from 0 to 1, where 1 is solid and 0 invisible. A value outside the range is clamped to it rather than rejected. A literal or constant value outside the range gets a warning, for example `opacity 50 is outside 0–1; 1 is solid`.

### syntax

```
color.new(simple color color, simple float alpha) → simple color
```

### args

- `color`: simple color
  The base color (e.g., color.red, #00ff7f, color.rgb(255, 0, 0)).
  types: simple color, input color, const color, literal color
- `alpha`: simple float
  Opacity, from 0 to 1, where 1 is solid and 0 is invisible.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple color

### notes

- `alpha` is an opacity from 0 to 1, where 1 is solid and 0 is invisible. It is not a transparency from 0 to 100. A literal or constant value outside 0 to 1 compiles with the warning `opacity 50 is outside 0–1; 1 is solid`.

### example

```lipi
//@lipi=2
indicator("color.new Example", overlay=true)
c = color.new(color.blue, 0.3)
bgcolor(c)
```

### id

function:color.new~3

## color.new (function)

Takes a colour and an opacity, and returns that colour at that opacity.

Opacity runs from 0 to 1, where 1 is solid and 0 invisible. A value outside the range is clamped to it rather than rejected. A literal or constant value outside the range gets a warning, for example `opacity 50 is outside 0–1; 1 is solid`.

### syntax

```
color.new(series color color, series float alpha) → series color
```

### args

- `color`: series color
  The base color (e.g., color.red, #00ff7f, color.rgb(255, 0, 0)).
  types: series color, simple color, input color, const color, literal color
- `alpha`: series float
  Opacity, from 0 to 1, where 1 is solid and 0 is invisible.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series color

### notes

- `alpha` is an opacity from 0 to 1, where 1 is solid and 0 is invisible. It is not a transparency from 0 to 100. A literal or constant value outside 0 to 1 compiles with the warning `opacity 50 is outside 0–1; 1 is solid`.

### example

```lipi
//@lipi=2
indicator("color.new Example", overlay=true)
c = color.new(color.blue, 0.3)
bgcolor(c)
```

### id

function:color.new~4

## color.olive (constant)

It is a predefined constant  for #808000 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.olive Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.olive, linewidth=2)
```

### id

constant:color.olive

## color.orange (constant)

It is a predefined constant  for #FFA500 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.orange Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.orange, linewidth=2)
```

### id

constant:color.orange

## color.purple (constant)

It is a predefined constant  for #800080 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.purple Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.purple, linewidth=2)
```

### id

constant:color.purple

## color.r (function)

Reads the red component back out of a colour.

The figure comes back on the scale it went in on, 0 to 255.

### syntax

```
color.r(const color color) → const int
```

### args

- `color`: const color
  Color.
  types: const color, literal color

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("color.r Example", overlay=false)
c = close > open ? color.lime : color.red
plot(color.r(c), title="Red Component", color=color.red)
```

### id

function:color.r~1

## color.r (function)

Reads the red component back out of a colour.

The figure comes back on the scale it went in on, 0 to 255.

### syntax

```
color.r(input color color) → input int
```

### args

- `color`: input color
  Color.
  types: input color, const color, literal color

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("color.r Example", overlay=false)
c = close > open ? color.lime : color.red
plot(color.r(c), title="Red Component", color=color.red)
```

### id

function:color.r~2

## color.r (function)

Reads the red component back out of a colour.

The figure comes back on the scale it went in on, 0 to 255.

### syntax

```
color.r(simple color color) → simple int
```

### args

- `color`: simple color
  Color.
  types: simple color, input color, const color, literal color

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("color.r Example", overlay=false)
c = close > open ? color.lime : color.red
plot(color.r(c), title="Red Component", color=color.red)
```

### id

function:color.r~3

## color.r (function)

Reads the red component back out of a colour.

The figure comes back on the scale it went in on, 0 to 255.

### syntax

```
color.r(series color color) → series int
```

### args

- `color`: series color
  Color.
  types: series color, simple color, input color, const color, literal color

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("color.r Example", overlay=false)
c = close > open ? color.lime : color.red
plot(color.r(c), title="Red Component", color=color.red)
```

### id

function:color.r~4

## color.red (constant)

It is a predefined constant  for #FF0000 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.red Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.red, linewidth=2)
```

### id

constant:color.red

## color.rgb (function)

Builds a colour from red, green and blue components, with an optional opacity.

Two scales meet in one call: the components run from 0 to 255 and the opacity from 0 to 1. Leave the opacity out and the colour is solid; components and opacity are both clamped to their range.

### syntax

```
color.rgb(const int r, const int g, const int b, const float a) → const color
```

### args

- `r`: const int
  Red color component. Possible values are from 0 to 255.
  types: const int, literal int
- `g`: const int
  Green color component. Possible values are from 0 to 255.
  types: const int, literal int
- `b`: const int
  Blue color component. Possible values are from 0 to 255.
  types: const int, literal int
- `a?`: const float
  0 to 1, where 1 is fully opaque and 0 is fully transparent.
  types: const float, const int, literal int, literal float
  default: 1

### returnedType

const color

### example

```lipi
//@lipi=2
indicator("color.rgb Example", overlay=true)
// Solid orange, and the same colour at 30% opacity
solid = color.rgb(255, 165, 0)
faded = color.rgb(255, 165, 0, 0.3)
plot(close, title="Close", color=solid, linewidth=2)
bgcolor(faded)
```

### id

function:color.rgb~1

## color.rgb (function)

Builds a colour from red, green and blue components, with an optional opacity.

Two scales meet in one call: the components run from 0 to 255 and the opacity from 0 to 1. Leave the opacity out and the colour is solid; components and opacity are both clamped to their range.

### syntax

```
color.rgb(input int r, input int g, input int b, input float a) → input color
```

### args

- `r`: input int
  Red color component. Possible values are from 0 to 255.
  types: input int, const int, literal int
- `g`: input int
  Green color component. Possible values are from 0 to 255.
  types: input int, const int, literal int
- `b`: input int
  Blue color component. Possible values are from 0 to 255.
  types: input int, const int, literal int
- `a?`: input float
  0 to 1, where 1 is fully opaque and 0 is fully transparent.
  types: input float, input int, const int, literal int, const float, literal float
  default: 1

### returnedType

input color

### example

```lipi
//@lipi=2
indicator("color.rgb Example", overlay=true)
// Solid orange, and the same colour at 30% opacity
solid = color.rgb(255, 165, 0)
faded = color.rgb(255, 165, 0, 0.3)
plot(close, title="Close", color=solid, linewidth=2)
bgcolor(faded)
```

### id

function:color.rgb~2

## color.rgb (function)

Builds a colour from red, green and blue components, with an optional opacity.

Two scales meet in one call: the components run from 0 to 255 and the opacity from 0 to 1. Leave the opacity out and the colour is solid; components and opacity are both clamped to their range.

### syntax

```
color.rgb(simple int r, simple int g, simple int b, simple float a) → simple color
```

### args

- `r`: simple int
  Red color component. Possible values are from 0 to 255.
  types: simple int, input int, const int, literal int
- `g`: simple int
  Green color component. Possible values are from 0 to 255.
  types: simple int, input int, const int, literal int
- `b`: simple int
  Blue color component. Possible values are from 0 to 255.
  types: simple int, input int, const int, literal int
- `a?`: simple float
  0 to 1, where 1 is fully opaque and 0 is fully transparent.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
  default: 1

### returnedType

simple color

### example

```lipi
//@lipi=2
indicator("color.rgb Example", overlay=true)
// Solid orange, and the same colour at 30% opacity
solid = color.rgb(255, 165, 0)
faded = color.rgb(255, 165, 0, 0.3)
plot(close, title="Close", color=solid, linewidth=2)
bgcolor(faded)
```

### id

function:color.rgb~3

## color.rgb (function)

Builds a colour from red, green and blue components, with an optional opacity.

Two scales meet in one call: the components run from 0 to 255 and the opacity from 0 to 1. Leave the opacity out and the colour is solid; components and opacity are both clamped to their range.

### syntax

```
color.rgb(series int r, series int g, series int b, series float a) → series color
```

### args

- `r`: series int
  Red color component. Possible values are from 0 to 255.
  types: series int, simple int, input int, const int, literal int
- `g`: series int
  Green color component. Possible values are from 0 to 255.
  types: series int, simple int, input int, const int, literal int
- `b`: series int
  Blue color component. Possible values are from 0 to 255.
  types: series int, simple int, input int, const int, literal int
- `a?`: series float
  0 to 1, where 1 is fully opaque and 0 is fully transparent.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: 1

### returnedType

series color

### example

```lipi
//@lipi=2
indicator("color.rgb Example", overlay=true)
// Solid orange, and the same colour at 30% opacity
solid = color.rgb(255, 165, 0)
faded = color.rgb(255, 165, 0, 0.3)
plot(close, title="Close", color=solid, linewidth=2)
bgcolor(faded)
```

### id

function:color.rgb~4

## color.silver (constant)

It is a predefined constant  for #C0C0C0 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.silver Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.silver, linewidth=2)
```

### id

constant:color.silver

## color.teal (constant)

It is a predefined constant  for #008080 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.teal Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.teal, linewidth=2)
```

### id

constant:color.teal

## color.white (constant)

It is a predefined constant  for #FFFFFF color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.white Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.white, linewidth=2)
```

### id

constant:color.white

## color.yellow (constant)

It is a predefined constant  for #FFFF00 color.

### type

const color

### example

```lipi
//@lipi=2
indicator("color.yellow Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=color.yellow, linewidth=2)
```

### id

constant:color.yellow
