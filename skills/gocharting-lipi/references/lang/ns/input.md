Contents: input (library) · input.bool (function) · input.color (function) · input.enum (function) · input.float (function) · input.float (function) · input.int (function) · input.int (function) · input.price (function) · input.session (function) · input.source (function) · input.string (function) · input.text_area (function) · input.time (function) · input.timeframe (function)

# input

## input (library)

Twelve functions, one per kind of setting the reader can change from the chart: bool, colour, enum, float, int, price, session, source, string, text area, time and timeframe.

A value that came from one of these carries the `input` form — you never write that qualifier, the call produces it.

### example

```lipi
//@lipi=2
indicator("input Library Example", overlay=true)
length = input.int(20, title="Length", minval=1)
src = input.source(close, title="Source")
showBands = input.bool(true, title="Show Bands")
lineColor = input.color(color.blue, title="Line Colour")
basis = talib.sma(src, length)
plot(basis, title="Basis", color=lineColor)
plot(showBands ? basis + talib.stdev(src, length) * 2 : na, title="Upper", color=color.gray)
plot(showBands ? basis - talib.stdev(src, length) * 2 : na, title="Lower", color=color.gray)
```

### id

library:input

## input.bool (function)

Offers the reader a true-or-false setting and hands back what they chose.

One of twelve input functions, one per kind of control. Only `defval` is required.

### syntax

```
input.bool(const bool defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input bool
```

### args

- `defval`: const bool
  Default value of the input. The reader can change it from the chart.
  types: const bool, const int, literal int, const float, literal float, literal bool
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.none`: the value is shown only in the settings.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.none

### returnedType

input bool

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.bool()` cannot be `na`." Any constant expression of type bool is accepted, such as `true`.

### example

```lipi
//@lipi=2
indicator("Boolean Input Example", overlay=true)
showSMA = input.bool(true, title="Show SMA")
sma_value = talib.sma(close, 14)
plot(showSMA ? sma_value : na, title="SMA", color=color.blue, linewidth=2)
```

### id

function:input.bool

## input.color (function)

Asks the reader for a colour.

Pass the result straight to a colour argument of a chart-output call; those arguments accept an input-form colour.

### syntax

```
input.color(const color defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input color
```

### args

- `defval`: const color
  Default value of the input. The reader can change it from the chart.
  types: const color, literal color
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.none`: the value is shown only in the settings.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.none

### returnedType

input color

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.color()` cannot be `na`." Any constant expression of type color is accepted, such as `color.red` or `color.new(color.red, 0.5)`.

### example

```lipi
//@lipi=2
indicator("Custom SMA", overlay=true)
smaColor = input.color(color.blue, title="SMA Color")
plot(talib.sma(close, 14), color=smaColor)
```

### id

function:input.color

## input.enum (function)

Adds a dropdown setting whose choices are the members of an enum you declare. It returns the chosen member, so the script can compare it with the members directly.

Each member's title, the text after `=` in the enum declaration, is what the reader sees in the dropdown. `options` can limit the dropdown to some of the members.

### syntax

```
input.enum(const enum defval, const string title, [const enum...] options, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input enum
```

### args

- `defval`: const enum
  The enum member used as the default value.
  types: const enum
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `options?`: [const enum...]
  The enum members the dropdown is limited to.
  types: const [enum...]
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input enum

### example

```lipi
//@lipi=2
indicator("input.enum Example", overlay=true)
enum Source {
    ClosePrice = "Close"
    MidPrice = "High/Low Midpoint"
}
src = input.enum(Source.ClosePrice, "Price Source")
price = src == Source.ClosePrice ? close : hl2
plot(talib.sma(price, 20), title="SMA", color=color.blue)
```

### id

function:input.enum

## input.float (function)

The decimal counterpart of `input.int`, with the same arguments and `const float` in place of `const int`.

`minval`, `maxval` and `step` may each be given by name, as in `input.float(2.0, "Mult", step=0.5)`.

### syntax

```
input.float(const float defval, const string title, const float minval, const float maxval, const float step, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input float
```

### args

- `defval`: const float
  Default value of the input. The reader can change it from the chart.
  types: const float, const int, literal int, literal float
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `minval?`: const float
  Minimal possible value of the input variable. Optional.
  types: const float, const int, literal int, literal float
  default: na
- `maxval?`: const float
  Maximum possible value of the input variable. Optional.
  types: const float, const int, literal int, literal float
  default: na
- `step?`: const float
  The amount the value changes by in the settings' up and down buttons. Optional. The default is 1.
  types: const float, const int, literal int, literal float
  default: 1
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input float

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.float()` cannot be `na`." Any constant expression of type float is accepted, such as `-5.5` or `2.5 * 2`.

### example

```lipi
//@lipi=2
indicator("float")
multiplier = input.float(2.0, title="Multiplier")
atr = talib.atr(14) * multiplier
plot(atr, color=color.blue, title="ATR Multiplied")
```

### id

function:input.float~1

## input.float (function)

The decimal counterpart of `input.int`, with the same arguments and `const float` in place of `const int`.

`minval`, `maxval` and `step` may each be given by name, as in `input.float(2.0, "Mult", step=0.5)`.

### syntax

```
input.float(const float defval, const string title, [const float...] options, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input float
```

### args

- `defval`: const float
  Default value of the input. The reader can change it from the chart. When `options` is given, `defval` must be one of its values.
  types: const float, const int, literal int, literal float
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `options?`: [const float...]
  List of values the reader can choose from. The value of `defval` must be one of them.
  types: const [float...], literal [float...]
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input float

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.float()` cannot be `na`." Any constant expression of type float is accepted, such as `-5.5` or `2.5 * 2`.

### example

```lipi
//@lipi=2
indicator("float")
multiplier = input.float(2.0, title="Multiplier")
atr = talib.atr(14) * multiplier
plot(atr, color=color.blue, title="ATR Multiplied")
```

### id

function:input.float~2

## input.int (function)

A whole-number setting, with optional bounds and an optional increment.

It and `input.float` are the only two input functions that take `minval`, `maxval` and `step`; each may be given by name, as in `input.int(14, "Length", minval=1, step=2)`.

### syntax

```
input.int(const int defval, const string title, const int minval, const int maxval, const int step, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input int
```

### args

- `defval`: const int
  Default value of the input. The reader can change it from the chart.
  types: const int, literal int
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `minval?`: const int
  Minimal possible value of the input variable. Optional.
  types: const int, literal int
  default: na
- `maxval?`: const int
  Maximum possible value of the input variable. Optional.
  types: const int, literal int
  default: na
- `step?`: const int
  The amount the value changes by in the settings' up and down buttons. Optional. The default is 1.
  types: const int, literal int
  default: 1
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input int

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.int()` cannot be `na`." Any constant expression of type int is accepted, such as `-5` or `2 * 3`.

### example

```lipi
//@lipi=2
indicator("Custom High-Low Offset", overlay=true)
offset = input.int(2, title="Offset Value", minval=1)
plot(high + offset, color=color.green, title="High Offset")
plot(low - offset, color=color.red, title="Low Offset")
```

### id

function:input.int~1

## input.int (function)

A whole-number setting, with optional bounds and an optional increment.

It and `input.float` are the only two input functions that take `minval`, `maxval` and `step`; each may be given by name, as in `input.int(14, "Length", minval=1, step=2)`.

### syntax

```
input.int(const int defval, const string title, [const int...] options, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input int
```

### args

- `defval`: const int
  Default value of the input. The reader can change it from the chart. When `options` is given, `defval` must be one of its values.
  types: const int, literal int
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `options?`: [const int...]
  List of values the reader can choose from. The value of `defval` must be one of them.
  types: const [int...], literal [int...]
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input int

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.int()` cannot be `na`." Any constant expression of type int is accepted, such as `-5` or `2 * 3`.

### example

```lipi
//@lipi=2
indicator("Custom High-Low Offset", overlay=true)
offset = input.int(2, title="Offset Value", minval=1)
plot(high + offset, color=color.green, title="High Offset")
plot(low - offset, color=color.red, title="Low Offset")
```

### id

function:input.int~2

## input.price (function)

A price setting. The value comes back as a float.

Unlike `input.float` it takes no bounds and no step, so use `input.float` where a range matters.

### syntax

```
input.price(const float defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input float
```

### args

- `defval`: const float
  Default value of the input. The reader can change it from the chart.
  types: const float, const int, literal int, literal float
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
   Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input float

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.price()` cannot be `na`." Any constant expression of type float is accepted, such as `100.5` or `2.5 * 2`.

### example

```lipi
//@lipi=2
indicator("Custom Price Input", overlay=true)
priceLevel = input.price(22300.0, title="Custom Price Level", confirm=true)
plot(priceLevel, title="Selected Price", color=color.blue, linewidth=2, style=plotStyle.scatter)
```

### id

function:input.price

## input.session (function)

Asks the reader for a session and gives you back a string.

The string is a session in the form that `time()` reads: `HHMM-HHMM` on a 24-hour clock, such as "0930-1600". Join ranges with commas, as in "1000-1100,1400-1500". Add `:` and the digits 1 to 7 to limit the session to days, Sunday being 1, as in "0930-1600:23456". A range that ends before it starts wraps past midnight, and "0000-0000" is the whole day.

### syntax

```
input.session(const string defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input string
```

### args

- `defval`: const string
  Default value of the input. The reader can change it from the chart.
  types: const string, literal string
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("input.session Example", overlay=true)
sess = input.session("0930-1600", "Trading Session")
inSession = not na(time(interval.interval, sess))
bgcolor(inSession ? color.new(color.blue, 0.1) : na)
```

### id

function:input.session

## input.source (function)

Lets the reader pick which series the script reads — the close, the high, a midpoint, and so on.

It is the exception in this namespace: it returns a `series float` rather than an input-form value, so what you get back can differ on every bar.

### syntax

```
input.source(series float defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → series float
```

### args

- `defval`: series float
  Default source: a built-in series float variable such as `close` or `hlc3`. The reader can change it from the chart.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Custom Source Input", overlay=true)
src = input.source(close, title="Data Source")
smaValue = talib.sma(src, 14)
plot(smaValue, title="SMA", color=color.blue, linewidth=2)
```

### id

function:input.source

## input.string (function)

A one-line text setting.

For a longer piece of text, reach for `input.text_area` instead; both return an `input string`.

### syntax

```
input.string(const string defval, const string title, [const string...] options, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input string
```

### args

- `defval`: const string
  Default value of the input. The reader can change it from the chart. When `options` is given, `defval` must be one of its values.
  types: const string, literal string
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `options?`: [const string...]
  List of values the reader can choose from. The value of `defval` must be one of them.
  types: const [string...], literal [string...]
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input string

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.string()` cannot be `na`." Any constant expression of type string is accepted, such as `"a" + "b"`.

### example

```lipi
//@lipi=2
indicator("String Input Example", overlay=true)
customText = input.string("Bullish", title="Trend Direction")
bgcolor(customText == "Bullish" ? color.green : customText == "Bearish" ? color.red : na)
```

### id

function:input.string

## input.text_area (function)

A multi-line text setting, for a message or a note rather than a single word.

### syntax

```
input.text_area(const string defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input string
```

### args

- `defval`: const string
  Default value of the input. The reader can change it from the chart.
  types: const string, literal string
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.none`: the value is shown only in the settings.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.none

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("Text Area Input Example", overlay=true)
customNotes = input.text_area("Enter your notes here...", title="Custom Notes")
bgcolor(customNotes == "Bullish" ? color.green : customNotes == "Bearish" ? color.red : na)
```

### id

function:input.text_area

## input.time (function)

A time setting, returned as an int.

The date functions take a time and a timezone, so a value from here can be fed to `hour`, `year` and the rest.

### syntax

```
input.time(const int defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input int
```

### args

- `defval`: const int
  The default time, in milliseconds since 1970-01-01 UTC, for example `1704067200000` for 2024-01-01 00:00 UTC. The reader can change it in the script's settings. Write the number itself: `timestamp(...)` compiles here but is worked out only when the script runs, so as a default it gives `na`.
  types: const int, literal int
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
   Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader sets the time by clicking on the chart when the script is added to it, or afterwards by selecting the script and moving the selection. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.none`: the value is shown only in the settings.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.none

### returnedType

input int

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input.time()` cannot be `na`." Any constant expression of type int that gives a time in milliseconds is accepted, such as `1700000000000` or `1000 * 60 * 60`.

### example

```lipi
//@lipi=2
indicator("input.time Example", overlay=true)
startTime = input.time(1767225600000, "Start Date")
// Highlight every bar from the chosen date onwards
bgcolor(time >= startTime ? color.new(color.green, 0.9) : na)
```

### id

function:input.time

## input.timeframe (function)

Asks the reader for a timeframe. The answer arrives as a string.

Note what it is not: choosing a timeframe here does not fetch that timeframe's data. Lipi has no way to request another symbol's or another interval's series.

### syntax

```
input.timeframe(const string defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input string
```

### args

- `defval`: const string
  Default value of the input. The reader can change it from the chart.
  types: const string, literal string
- `title?`: const string
  Title of the input. If not specified, the title is `Untitled`. If the title is specified but empty, the title is an empty string.
  types: const string, literal string
  default: "Untitled"
- `tooltip?`: const string
  Text of a tooltip shown with the input.
  types: const string, literal string
  default: ""
- `inline?`: const string
  Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
  types: const string, literal string
  default: ""
- `group?`: const string
  Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
  types: const string, literal string
  default: ""
- `confirm?`: const bool
  If true, the reader is asked to confirm the value before the script is added to the chart. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: const display
  Where the input's value is shown outside the script's settings, as a `display.*` constant: `display.status_line`, `display.data_window`, `display.all` or `display.none`. Combine constants with `+`. The default is `display.all`.
  types: const display, literal display
  values: display.none, display.data_window, display.status_line, display.all
  default: display.all

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("input.timeframe Example", overlay=true)
tf = input.timeframe("1D", "Reference Timeframe")
// The input returns text only: compare it with the chart's own interval
sameAsChart = tf == interval.interval
bgcolor(sameAsChart ? color.new(color.green, 0.1) : na)
```

### id

function:input.timeframe
