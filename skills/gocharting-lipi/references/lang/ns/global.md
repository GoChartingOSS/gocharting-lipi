Contents: ! (operator) · != (operator) · % (operator) · %= (operator) · && (operator) · * (operator) · *= (operator) · + (operator) · += (operator) · - (operator) · -= (operator) · / (operator) · /= (operator) · := (operator) · < (operator) · <= (operator) · = (operator) · == (operator) · > (operator) · >= (operator) · ? (operator) · @lipi= (annotation) · alert (function) · alertcondition (function) · and (keyword) · bar_index (variable) · barcolor (function) · bgcolor (function) · bool (type) · bool (function) · bool (function) · bool (function) · bool (function) · box (function) · break (keyword) · case (keyword) · close (variable) · color (function) · color (function) · color (function) · color (function) · const (keyword) · continue (keyword) · dayofmonth (variable) · dayofmonth (function) · dayofweek (variable) · dayofweek (function) · def (keyword) · default (keyword) · display (type) · display (enum) · else (keyword) · enum (keyword) · false (constant) · fill (function) · fill (function) · fill (function) · fill (function) · fixnan (function) · fixnan (function) · fixnan (function) · fixnan (function) · float (type) · float (function) · float (function) · float (function) · float (function) · font (type) · font (enum) · for in (keyword) · for to (keyword) · func (keyword) · high (variable) · hl2 (variable) · hlc3 (variable) · hlcc4 (variable) · hline (type) · hline (function) · hlineStyle (type) · hlineStyle (enum) · hour (variable) · hour (function) · if (keyword) · indicator (function) · input (function) · input (function) · input (function) · input (function) · input (function) · input (function) · int (type) · int (function) · int (function) · int (function) · int (function) · intra (keyword) · label (function) · last_bar_index (variable) · last_bar_time (variable) · line (function) · linefill (function) · location (type) · location (enum) · low (variable) · minute (variable) · minute (function) · month (variable) · month (function) · na (constant) · na (function) · not (keyword) · nz (function) · nz (function) · nz (function) · nz (function) · nz (function) · ohlc4 (variable) · oi (variable) · open (variable) · or (keyword) · plot (type) · plot (function) · plotStyle (type) · plotStyle (enum) · plotarrow (function) · plotbar (function) · plotcandle (function) · plotchar (function) · plotchar (function) · plotshape (function) · plotshape (function) · polyline (function) · return (keyword) · scale (type) · scale (enum) · second (variable) · second (function) · series (keyword) · shape (type) · shape (enum) · simple (keyword) · size (type) · size (enum) · static (keyword) · step (keyword) · strategy (function) · string (type) · string (function) · string (function) · string (function) · string (function) · switch (keyword) · table (function) · time (variable) · time (function) · time (function) · time_close (variable) · time_close (function) · time_close (function) · time_sessionday (variable) · timenow (variable) · timestamp (function) · timestamp (function) · timestamp (function) · timestamp (function) · timestamp (function) · timestamp (function) · true (constant) · type (keyword) · volume (variable) · weekofyear (function) · while (keyword) · year (variable) · year (function) · || (operator)

# global

## ! (operator)

Logical NOT. Applicable to boolean expressions: `!x` is true when `x` is false, and false when `x` is true.

It is the symbol spelling of `not`, and the two are the same token to the lexer.

### syntax

```
!expr0 | not expr0
```

### example

```lipi
//@lipi=2
indicator("Logical NOT Example", overlay=true)
// Condition: Close is above the previous close
abovePrevClose = close > close[1]
// Use `!` to invert the condition
bgcolor(!abovePrevClose ? color.red : color.green)
```

### id

operator:!

## != (operator)

Not equal to. Applicable to expressions of any type. True when its two operands differ.

### syntax

```
expr0 != expr1
```

### example

```lipi
//@lipi=2
indicator("Not Equal Example", overlay=true)
// Mark bars whose close differs from the previous close
changed = close != close[1]
bgcolor(changed ? na : color.new(color.gray, 0.3))
```

### id

operator:!=

## % (operator)

Modulo: the remainder of dividing the left operand by the right one. Applicable to numerical expressions, ints and floats.

The result is an int when both operands are ints, and a float when either is a float (so `int x = 7.5 % 2` is rejected: use `math.floor`, `math.round` or `math.ceil`). A string operand is rejected. The result has the sign of the left operand: `-7 % 3` is -1, `7 % -3` is 1 and `-7.5 % 2` is -1.5.

### syntax

```
expr0 % expr1
```

### example

```lipi
//@lipi=2
indicator("Even or Odd Bars", overlay=true)
// Check if bar index is even or odd
isEvenBar = bar_index % 2 == 0
// Color background based on even or odd
bgcolor(isEvenBar ? color.green : color.red)
```

### id

operator:%

## %= (operator)

Modulo assignment. Replaces the variable with the remainder of dividing its current value by the right-hand expression.

The result follows `%`: a float variable accepts an int or a float operand; an int variable accepts only an int operand, and a float operand is an error that suggests `math.floor`, `math.round` or `math.ceil`. A string variable is rejected.

### syntax

```
<variableIdentifier> %= <expression>
```

### example

```lipi
//@lipi=2
indicator("Modulo Assign Example", overlay=true)
static int tick = 0
tick += 1
tick %= 2
bgcolor(tick == 0 ? color.new(color.green, 0.2) : na)
```

### id

operator:%=

## && (operator)

Logical AND. Applicable to boolean expressions.

### syntax

```
expr0 && expr1 | expr0 and expr1
```

### example

```lipi
//@lipi=2
indicator("Logical AND Example", overlay=true)
// && is the symbol spelling of and
insideBar = high < high[1] && low > low[1]
bgcolor(insideBar ? color.new(color.blue, 0.2) : na)
```

### id

operator:&&

## * (operator)

Multiplication. Applicable to numerical expressions.

### syntax

```
expr0 * expr1
```

### example

```lipi
//@lipi=2
indicator("Price Multiplier", overlay=true)
// Multiply close price by 1.05 (5% increase)
priceAdjusted = close * 1.05
// Plot the adjusted price
plot(priceAdjusted, title="5% Higher Price", color=color.blue)
```

### id

operator:*

## *= (operator)

Multiply assignment. Replaces the variable with the product of its current value and the right-hand expression. Applicable to int and float combinations using the same rules as `*`.

### syntax

```
<variableIdentifier> *= <expression>
```

### example

```lipi
//@lipi=2
indicator("Multiply Assign Example", overlay=true)
scale = 1.0
scale *= 1.01
plot(close * scale, title="Scaled close", color=color.blue)
```

### id

operator:*=

## + (operator)

Addition. Applicable to numerical expressions or strings. A unary plus (`+x`) is accepted.

### syntax

```
expr0 + expr1
```

### example

```lipi
//@lipi=2
indicator("Addition Example", overlay=false)
a = 0
b = 5
sum = a + b
plot(sum, title="Sum", color=color.blue)
```

### id

operator:+

## += (operator)

Add assignment. Replaces the variable with the sum of its current value and the right-hand expression. Works on numbers and on two strings.

The left-hand side may be a dotted field on an object (for example `point.x += 1`) as well as a plain variable. The variable must already exist.

### syntax

```
<variableIdentifier> += <expression>
```

### example

```lipi
//@lipi=2
indicator("Add Assign Example", overlay=false)
static int bars = 0
bars += 1
plot(bars, title="Bar counter", color=color.blue)
```

### id

operator:+=

## - (operator)

Subtraction or unary minus. Applicable to numerical expressions.

### syntax

```
expr0 - expr1 | -expr0
```

### example

```lipi
//@lipi=2
indicator("Close - 10", overlay=true)
// Subtract 10 from the closing price
priceAdjusted = close - 10
// Plot the adjusted price
plot(priceAdjusted, title="Close - 10", color=color.red)
```

### id

operator:-

## -= (operator)

Subtract assignment. Replaces the variable with its current value minus the right-hand expression. Applicable to int and float combinations using the same rules as `-`.

### syntax

```
<variableIdentifier> -= <expression>
```

### example

```lipi
//@lipi=2
indicator("Subtract Assign Example", overlay=true)
offset = close
offset -= open
plot(offset, title="Close minus open", color=color.red)
```

### id

operator:-=

## / (operator)

Division. Applicable to numerical expressions.

### syntax

```
expr0 / expr1
```

### notes

- The result is always a float, so `int h = 4 / 2` is rejected. Use `math.floor`, `math.round` or `math.ceil` to get an int.

### example

```lipi
//@lipi=2
indicator("Close / 2", overlay=true)
// Divide the closing price by 2
priceHalved = close / 2
// Plot the halved price
plot(priceHalved, title="Close / 2", color=color.blue)
```

### id

operator:/

## /= (operator)

Divide assignment. Replaces the variable with its current value divided by the right-hand expression. The result is always a float, so the variable must already be a float (or the assignment is rejected).

### syntax

```
<variableIdentifier> /= <expression>
```

### example

```lipi
//@lipi=2
indicator("Divide Assign Example", overlay=true)
half = close
half /= 2.0
plot(half, title="Half of close", color=color.gray)
```

### id

operator:/=

## := (operator)

Reassignment operator. It is used to assign a new value to a previously declared variable.

### syntax

```
<existing_variable> := <expression>
```

### example

```lipi
//@lipi=2
indicator("Bar Counter", overlay=true)
// Declare a mutable variable
static int barCount = 0
// Increment barCount on each new bar
barCount := barCount + 1
// Plot the bar counter
plot(barCount, title="Bar Count", color=color.blue)
```

### id

operator::=

## < (operator)

Less than. Applicable to numerical expressions.

### syntax

```
expr0 < expr1
```

### example

```lipi
//@lipi=2
indicator("Close Below MA", overlay=true)
// Define a 20-period simple moving average
sma20 = talib.sma(close, 20)
// Check if the close price is below the SMA
isBelowMA = close < sma20
// Change background color when the condition is true
bgcolor(isBelowMA ? color.red : na)
```

### id

operator:<

## <= (operator)

Less than or equal to. Applicable to numerical expressions.

### syntax

```
expr0 <= expr1
```

### example

```lipi
//@lipi=2
indicator("Low Volume Bars", overlay=true)
// Compute 50-period average volume
avgVolume = talib.sma(volume, 50)
// Check if the current volume is below or equal to average
isLowVolume = volume <= avgVolume
// Highlight bars with low volume
plotshape(isLowVolume, title="Low Volume", location=location.bottom, color=color.blue, shape=shape.triangleup)
```

### id

operator:<=

## = (operator)

for assignment.

### syntax

```
[<declaration_type>] [<data_type>] <variable_name> = <expression>
```

### example

```lipi
//@lipi=2
indicator("Assignment Operator Example", overlay=true)
// Assigning values using =
static int myNumber = 10
static float myFloat = 5.5
static string myText = "Hello, Lipi!"
// Reassigning values
myNumber := myNumber + 5
myFloat := myFloat * 2
// Plotting the updated number
plot(myNumber, title="Updated Number", color=color.blue)
```

### id

operator:=

## == (operator)

Equal to. Applicable to expressions of any type.

### syntax

```
expr0 == expr1
```

### example

```lipi
//@lipi=2
indicator("Moving Average Crossover", overlay=true)
// Define two moving averages
fastMA = talib.sma(close, 10)
slowMA = talib.sma(close, 20)
// Check if the fast MA is equal to the slow MA
isEqual = fastMA == slowMA
// Plot moving averages
plot(fastMA, title="Fast MA", color=color.blue)
plot(slowMA, title="Slow MA", color=color.red)
```

### id

operator:==

## > (operator)

Greater than. Applicable to numerical expressions.

### syntax

```
expr0 > expr1
```

### example

```lipi
//@lipi=2
indicator("Bullish Candle Detector", overlay=true)
 // Check if the current candle is bullish
isBullish = close > open  
// Plot a green background when the candle is bullish
bgcolor(isBullish ? color.green : na)
```

### id

operator:>

## >= (operator)

Greater than or equal to. Applicable to numerical expressions.

### syntax

```
expr0 >= expr1
```

### example

```lipi
//@lipi=2
indicator("Close >= Moving Average", overlay=true)
// Define a 20-period simple moving average (SMA)
sma20 = talib.sma(close, 20)
// Check if the closing price is greater than or equal to the SMA
isAboveOrEqual = close >= sma20
// Plot the moving average
plot(sma20, title="20-SMA", color=color.blue)
// Change background color when the condition is met
bgcolor(isAboveOrEqual ? color.green : na)
```

### id

operator:>=

## ? (operator)

Ternary conditional operator.

### syntax

```
expr0 ? expr1 : expr2
```

### example

```lipi
//@lipi=2
indicator("Ternary Operator Example", overlay=true)
// Define conditions
bullish = close > open
bearish = close < open
// Use ternary operator to set color based on conditions
candleColor = bullish ? color.green : bearish ? color.red : color.gray
// Color the candles
barcolor(candleColor)
```

### id

operator:?

## @lipi= (annotation)

Source annotation that selects which Lipi compiler stack runs the script. It must appear in a line comment at the top of the file, before other code.

On the v2 stack, `//@lipi=2` is required. A script with no directive is treated as v1 and is rejected by the v2 compiler. Supported version numbers are `1` and `2`.

Spaces are allowed after `//` and around `=` (for example `// @lipi = 2`); there must be no space between `@` and `lipi`.

### syntax

```
//@lipi=<integer>
```

### example

```lipi
//@lipi=2
indicator("Stack version", overlay=true)
plot(close)
```

## alert (function)

Raises an alert from inside your own logic, with a message you build.

It is the one output-shaped function with no top-level rule, so it may be called inside a branch — which is what makes "alert me when this happens" expressible. It fires at most once per bar, only on realtime bars, and only when the script is running as an alert; on historical bars it does nothing.

### syntax

```
alert(series string message) → void
```

### args

- `message`: series string
  The custom text message shown in the alert notification
  types: series string, simple string, input string, const string, literal string

### returnedType

void

### example

```lipi
//@lipi=2
indicator("RSI Alert", overlay=false)

rsi = talib.rsi(close, 14)

if talib.crossover(rsi, 70) {
    alert("RSI crossed above 70!")
}
```

### id

function:alert

## alertcondition (function)

Declares a condition the platform can offer to the reader. It raises nothing by itself.

Unlike `alert`, it must be called at the top level, and its title and message are const-form — fixed when the script is compiled. Left out, both read `na`.

### syntax

```
alertcondition(series bool condition, const string title, const string message) → void
```

### args

- `condition`: series bool
  Represents a Boolean expression or logic that determines when the alert should fire.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
- `title?`: const string
  Represents the name the alert condition.
  types: const string, literal string
  default: na
- `message?`: const string
  Represents the text message that will be shown or sent when the alert is triggered.
  types: const string, literal string
  default: na

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Volume > 10 Alert", overlay=false)

// Condition
volAbove10 = volume > 10

// Plotting for visual reference
plot(volume, title="Volume", color=color.blue, style=plotStyle.bar)

// Alert condition
alertcondition(volAbove10, title="Volume Greater Than 10", message="Volume has crossed above 10")
```

### id

function:alertcondition

## and (keyword)

True when both of its operands are true.

It has a symbol spelling as well, and the two are the same token to the lexer. There is no difference in behaviour to weigh up, so pick one spelling for a script and keep to it.

### syntax

```
expr0 && expr1 | expr0 and expr1
```

### example

```lipi
//@lipi=2
indicator("and Example", overlay=true)
// Both conditions must hold: an up bar on above-average volume
strongUp = close > open and volume > talib.sma(volume, 20)
bgcolor(strongUp ? color.new(color.green, 0.2) : na)
```

### id

keyword:and

## bar_index (variable)

The index of the bar being evaluated.

It is an int series rather than a float, and it changes bar by bar as a price does.

### type

series int

### example

```lipi
//@lipi=2
indicator("Bar Index Example", overlay=true)
plot(bar_index, color=color.blue)
```

### id

variable:bar_index

## barcolor (function)

Recolours the chart's own price bars. It draws no value of its own.

To colour only some bars, vary the colour rather than the call: the colour argument is series-form, while the call has to stay at the top level. Note that every argument here is optional, `color` included.

### syntax

```
barcolor(series color color, const string title, input int offset, input display display) → void
```

### args

- `color?`: series color
  Bar color. Use a color constant such as `color.blue`, a hex color such as `#00ff7f`, or an expression that returns a color, such as `close >= open ? color.yellow : color.blue`. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `title?`: const string
  Title of the barcolor. Optional argument
  types: const string, literal string
  default: na
- `offset?`: input int
  Shifts the color series to the left or to the right on the given number of bars. Default is 0.
  types: input int, const int, literal int
  default: 0
- `display?`: input display
  Whether the bar colors are shown: `display.all` (the default) or `display.none`. The other `display.*` constants are not supported here.
  types: input display, const display, literal display
  values: display.all, display.none
  default: display.all

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Custom Bar Color", overlay=true)
// Define conditions for different colors
bullish = close > open
bearish = close < open
neutral = close == open
// Assign colors based on conditions
barColor = bullish ? color.green : bearish ? color.red : color.gray
// Apply bar color
barcolor(barColor)
```

### id

function:barcolor

## bgcolor (function)

Shades the pane's background. Like `barcolor` it adds no value to the chart.

It differs from `barcolor` in one way that matters: it takes a `force_overlay` argument and `barcolor` does not.

### syntax

```
bgcolor(series color color, const string title, input int offset, const bool force_overlay, input display display) → void
```

### args

- `color?`: series color
  Color of the filled background. Use a color constant such as `color.blue`, a hex color such as `#00ff7f`, or an expression that returns a color, such as `close >= open ? color.yellow : color.blue`. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `title?`: const string
  Title of the bgcolor. Optional argument
  types: const string, literal string
  default: na
- `offset?`: input int
  Shifts the color series to the left or to the right on the given number of bars. Default is 0.
  types: input int, const int, literal int
  default: 0
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Whether the background color is shown: `display.all` (the default) or `display.none`. The other `display.*` constants are not supported here.
  types: input display, const display, literal display
  values: display.all, display.none
  default: display.all

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Custom Background Color", overlay=true)
bullish = close > open
bearish = close < open
bgColor = bullish ? color.green : bearish ? color.red : na
bgcolor(bgColor)
```

### id

function:bgcolor

## bool (type)

A true-or-false value. The two constants `true` and `false` are the literals for it.

Comparisons produce one, and the marker functions take one as their condition. No fields.

### example

```lipi
//@lipi=2
indicator("Bool Keyword Example", overlay=true)
// Calculate 50-period simple moving average (SMA)
sma50 = talib.sma(close, 50)
// Declare a boolean variable using `bool` keyword
bool isAboveSMA = close > sma50
// Plot a signal dot when the condition is true
plotshape(isAboveSMA, location=location.belowbar, color=color.green, shape=shape.circle, size=size.small, title="Above SMA")
```

### id

type:bool

## bool (function)

Declares a value as a bool.

A number becomes `false` when it is zero and `true` otherwise, so `bool(2)` is `true`. Most functions with a bool argument convert a number the same way; `alertcondition` does not and needs a bool expression ("The `condition` argument of `alertcondition()` must be a boolean series.").

### syntax

```
bool(const bool value) → const bool
```

### args

- `value`: const bool
  The value to convert to the specified type, usually na.
  types: const bool, const int, literal int, const float, literal float, literal bool

### returnedType

const bool

### example

```lipi
//@lipi=2
indicator("bool() Example", overlay=true)
// A typed na: the variable is known to be bool before it has a value
bool signal = bool(na)
signal := close > open
bgcolor(signal ? color.new(color.green, 0.2) : na)
```

### id

function:bool~1

## bool (function)

Declares a value as a bool.

A number becomes `false` when it is zero and `true` otherwise, so `bool(2)` is `true`. Most functions with a bool argument convert a number the same way; `alertcondition` does not and needs a bool expression ("The `condition` argument of `alertcondition()` must be a boolean series.").

### syntax

```
bool(input bool value) → input bool
```

### args

- `value`: input bool
  The value to convert to the specified type, usually na.
  types: input bool, input int, const int, literal int, input float, const float, literal float, const bool, literal bool

### returnedType

input bool

### example

```lipi
//@lipi=2
indicator("bool() Example", overlay=true)
// A typed na: the variable is known to be bool before it has a value
bool signal = bool(na)
signal := close > open
bgcolor(signal ? color.new(color.green, 0.2) : na)
```

### id

function:bool~2

## bool (function)

Declares a value as a bool.

A number becomes `false` when it is zero and `true` otherwise, so `bool(2)` is `true`. Most functions with a bool argument convert a number the same way; `alertcondition` does not and needs a bool expression ("The `condition` argument of `alertcondition()` must be a boolean series.").

### syntax

```
bool(simple bool value) → simple bool
```

### args

- `value`: simple bool
  The value to convert to the specified type, usually na.
  types: simple bool, simple int, input int, const int, literal int, simple float, input float, const float, literal float, input bool, const bool, literal bool

### returnedType

simple bool

### example

```lipi
//@lipi=2
indicator("bool() Example", overlay=true)
// A typed na: the variable is known to be bool before it has a value
bool signal = bool(na)
signal := close > open
bgcolor(signal ? color.new(color.green, 0.2) : na)
```

### id

function:bool~3

## bool (function)

Declares a value as a bool.

A number becomes `false` when it is zero and `true` otherwise, so `bool(2)` is `true`. Most functions with a bool argument convert a number the same way; `alertcondition` does not and needs a bool expression ("The `condition` argument of `alertcondition()` must be a boolean series.").

### syntax

```
bool(series bool value) → series bool
```

### args

- `value`: series bool
  The value to convert to the specified type, usually na.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("bool() Example", overlay=true)
// A typed na: the variable is known to be bool before it has a value
bool signal = bool(na)
signal := close > open
bgcolor(signal ? color.new(color.green, 0.2) : na)
```

### id

function:bool~4

## box (function)

Converts `value` to the `box` type. It is used almost only as `box(na)`, to declare a box variable that has no drawing yet, so that its type is known before the first drawing is assigned.

### syntax

```
box(series box value) → series box
```

### args

- `value`: series box
  The value to convert to the specified type, usually na.
  types: series box, simple box, input box, const box, literal box

### returnedType

series box

### example

```lipi
//@lipi=2
indicator("box() Example", overlay=true)
static box rangeBox = box(na)
if barstate.islast {
    rangeBox := box.new(bar_index[10], talib.highest(high, 10), bar_index, talib.lowest(low, 10), border_color=color.blue, bgcolor=color.new(color.blue, 0.2), textcolor=color.white)
}
```

### id

function:box

## break (keyword)

Leaves the innermost `for` or `while` loop at once.

### syntax

```
break
```

### example

```lipi
//@lipi=2
indicator("break Example")
float s = 0
for i = 0 to 9 {
    if i == 5 {
        break // stop the loop at 5
    }
    s += i
}
plot(s)
```

### id

keyword:break

## case (keyword)

Starts one block of a `switch`: `case <value>:` runs its block when the value of the `switch` equals `<value>`.

The first case that matches runs, and the `switch` ends: the next case does not run. A case takes one value, so `case 1, 2:` is a syntax error. The value must have the type of the `switch` value (an int fits a float `switch`); otherwise the compiler stops with "Case condition is not compatible with switch condition." and the two types.

### syntax

```
case <value>: <statement>
```

### example

```lipi
//@lipi=2
indicator("case Example")
int k = 2
float x = 0
switch k {
    case 1: x := 10
    case 2: x := 20
    default: x := 0
}
plot(x)
```

### id

keyword:case

## close (variable)

The bar's closing price. This is the value most calculations start from.

On a bar that has not finished forming, the reading is that bar's closing value so far.

### type

series float

### example

```lipi
//@lipi=2
indicator("close")
latest_close = close
plot(latest_close, color=color.blue, title="Close Price")
```

### id

variable:close

## color (function)

Converts a value to a colour.

It accepts a colour only. The `color` namespace holds the functions that build a colour from components or read one apart.

### syntax

```
color(const color value) → const color
```

### args

- `value`: const color
  The value to convert to the specified type, usually na.
  types: const color, literal color

### returnedType

const color

### example

```lipi
//@lipi=2
indicator("color() Example", overlay=true)
// A typed na colour, set only on up bars
color c = color(na)
if close > open {
    c := color.green
}
barcolor(c)
```

### id

function:color~1

## color (function)

Converts a value to a colour.

It accepts a colour only. The `color` namespace holds the functions that build a colour from components or read one apart.

### syntax

```
color(input color value) → input color
```

### args

- `value`: input color
  The value to convert to the specified type, usually na.
  types: input color, const color, literal color

### returnedType

input color

### example

```lipi
//@lipi=2
indicator("color() Example", overlay=true)
// A typed na colour, set only on up bars
color c = color(na)
if close > open {
    c := color.green
}
barcolor(c)
```

### id

function:color~2

## color (function)

Converts a value to a colour.

It accepts a colour only. The `color` namespace holds the functions that build a colour from components or read one apart.

### syntax

```
color(simple color value) → simple color
```

### args

- `value`: simple color
  The value to convert to the specified type, usually na.
  types: simple color, input color, const color, literal color

### returnedType

simple color

### example

```lipi
//@lipi=2
indicator("color() Example", overlay=true)
// A typed na colour, set only on up bars
color c = color(na)
if close > open {
    c := color.green
}
barcolor(c)
```

### id

function:color~3

## color (function)

Converts a value to a colour.

It accepts a colour only. The `color` namespace holds the functions that build a colour from components or read one apart.

### syntax

```
color(series color value) → series color
```

### args

- `value`: series color
  The value to convert to the specified type, usually na.
  types: series color, simple color, input color, const color, literal color

### returnedType

series color

### example

```lipi
//@lipi=2
indicator("color() Example", overlay=true)
// A typed na colour, set only on up bars
color c = color(na)
if close > open {
    c := color.green
}
barcolor(c)
```

### id

function:color~4

## const (keyword)

A qualifier written before the type of a parameter of your own function. A `const` parameter takes only a value that is known when the script is compiled, such as `2.0` or `10 * 2`.

A value that changes, such as `close`, is refused with "Cannot call `<function>` with argument `<name>`=`<value>`. An argument of `series float` type was used but a `const float` is expected." The word is not allowed before a variable declaration.

### syntax

```
func <name>(const <data_type> <parameter_name>) => <expression>
```

### example

```lipi
//@lipi=2
indicator("const Example")
func scaled(series float x, const float k) => x * k
plot(scaled(close, 2.0))
```

### id

keyword:const

## continue (keyword)

Skips the rest of the current pass of the innermost `for` or `while` loop and starts the next pass.

### syntax

```
continue
```

### example

```lipi
//@lipi=2
indicator("continue Example")
float s = 0
for i = 0 to 9 {
    if i == 5 {
        continue // skip 5
    }
    s += i
}
plot(s)
```

### id

keyword:continue

## dayofmonth (variable)

The day of the month of the bar being evaluated.

### type

series int

### example

```lipi
//@lipi=2
indicator("Day of Month Example", overlay=true)
bgcolor(dayofmonth == 20 ? color.red : na)
```

### id

variable:dayofmonth

## dayofmonth (function)

The day of the month of a time you supply.

### syntax

```
dayofmonth(series int time, series string timezone) → series int
```

### args

- `time`: series int
  UNIX time, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `timezone?`: series string
  The time zone the value is read in: an IANA time zone database name (for example "America/New_York") or "UTC". Unlike `timestamp`, `time` and `str.format_time`, this function does not accept offset notation such as "UTC-5" or "GMT+0530": a name that cannot be loaded gives 0, not `na`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Day of Month Example", overlay=true)
// Get current bar day of month
currentDay = dayofmonth(time)
// Plot day in Data Window
plot(currentDay, title="Current Day")
```

### id

function:dayofmonth

## dayofweek (variable)

The day of the week of the bar being evaluated, as an int series.

Sunday is `1` and Saturday is `7`. Compare with `dayofweek.sunday` … `dayofweek.saturday` (same numbers) instead of memorising literals.

### type

series int

### example

```lipi
//@lipi=2
indicator("Day of Week Example", overlay=true)
plot(dayofweek == dayofweek.monday ? 1 : 0, title="Monday", color=color.blue)
```

### id

variable:dayofweek

## dayofweek (function)

The day of the week of a time you supply, as an int series.

Uses the same numbering as the `dayofweek` variable: Sunday `1` through Saturday `7` (`dayofweek.sunday` … `dayofweek.saturday`).

### syntax

```
dayofweek(series int time, series string timezone) → series int
```

### args

- `time`: series int
  UNIX time, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `timezone?`: series string
  The time zone the value is read in: an IANA time zone database name (for example "America/New_York") or "UTC". Unlike `timestamp`, `time` and `str.format_time`, this function does not accept offset notation such as "UTC-5" or "GMT+0530": a name that cannot be loaded gives 0, not `na`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Day of Week Example", overlay=true)
// Get current bar day of week
currentDay = dayofweek(time)
// Plot day in Data Window
plot(currentDay, title="Current Day")
```

### id

function:dayofweek

## def (keyword)

Declares a **type function** (method on a type): the **first parameter** is the receiver — its declared type is the type the method belongs to.

You must list **at least one** parameter (the receiver). Use `func` (or a declaration with no leading keyword) for ordinary functions, including `func name() => …` with zero parameters.

`def` is not interchangeable with `func` when the parameter list is empty.

### syntax

```
def <function_name>(<data_type> <param_name> [= <default_value>], ...) {
	<function_body>
}
		
func <function_name>(<data_type> <param_name> [= <default_value>], ...) => <expression>
```

### example

```lipi
//@lipi=2
indicator("def type function Example", overlay=true)
def spread(float h, float l) {
    return h - l
}
plot(spread(high, low), title="Bar spread", color=color.blue)
```

### id

keyword:def

## default (keyword)

Runs its block when no `case` of the `switch` matches.

A `switch` takes at most one `default`: a second one stops the compiler with "Only one `default` case is allowed in a switch statement."

### syntax

```
default: <statement>
```

### example

```lipi
//@lipi=2
indicator("default Example")
float k = close > open ? 1.0 : 2.0
float x = 0
switch k {
    case 1: x := 10
    case 2: x := 20
    default: x := 0
}
plot(x)
```

### id

keyword:default

## display (type)

Controls where a plot or indicator output is visible in the UI (pane, price scale, status line, data window).

### fields

- `none`
  Hide from all display locations.
- `pane`
  Show only in the chart pane.
- `data_window`
  Show only in the Data Window.
- `price_scale`
  Show on the price scale.
- `status_line`
  Show in the status line.
- `all`
  Show in pane, price scale, status line, and data window.

### example

```lipi
//@lipi=2
indicator("display example")
plot(close, display=display.all)
plot(open, display=display.none)
plot(high, display=display.price_scale + display.status_line)
```

### id

type:display

## display (enum)

Controls where a plot or indicator output is visible in the UI (pane, price scale, status line, data window).

### fields

- `none`
  Hide from all display locations.
- `pane`
  Show only in the chart pane.
- `data_window`
  Show only in the Data Window.
- `price_scale`
  Show on the price scale.
- `status_line`
  Show in the status line.
- `all`
  Show in pane, price scale, status line, and data window.

### example

```lipi
//@lipi=2
indicator("display example")
plot(close, display=display.all)
plot(open, display=display.none)
plot(high, display=display.price_scale + display.status_line)
```

### id

enum:display

## else (keyword)

Runs a block when the condition of the `if` before it is false.

It follows the closing `}` of the `if` block, on the same line or on the next, and can be chained as `else if <condition> { ... }`.

### syntax

```
if <condition> {
	...
} else {
	...
}
```

### example

```lipi
//@lipi=2
indicator("else Example")
float level = 0
if close > open {
    level := 1
} else if close < open {
    level := -1
} else {
    level := 0
}
plot(level)
```

### id

keyword:else

## enum (keyword)

Declares an enum of your own, as a braced block of members, one per line.

A member may carry something after `=`. Note what that is: a title, not a value.

### syntax

```
enum <enum_name> {
	<enum_field> [= <title>]
	...
}
```

### example

```lipi
//@lipi=2
indicator("enum Example", overlay=true)
// Each member may carry a title after =, shown in the settings dropdown
enum Signal {
    buy = "Buy"
    sell = "Sell"
    neutral = "Neutral"
}
signal = close > open ? Signal.buy : close < open ? Signal.sell : Signal.neutral
bgcolor(signal == Signal.buy ? color.new(color.green, 0.15) : signal == Signal.sell ? color.new(color.red, 0.15) : na)
```

### id

keyword:enum

## false (constant)

The bool value false. Comparisons and conditions produce it; it can also be written directly, as a default value or a constant.

### type

const bool

### example

```lipi
//@lipi=2
indicator("false Example", overlay=true)
static bool crossedUp = false
if talib.crossover(close, talib.sma(close, 20)) {
    crossedUp := true
}
bgcolor(crossedUp ? color.new(color.green, 0.1) : na)
```

### id

constant:false

## fill (function)

Shades the band between two plots, or between two horizontal lines. It has two forms and no mixed one, so you cannot fill between a plot and a level, and like the other output calls it must sit at the top level.

The forms differ in argument order, and that is the thing that bites: for two levels the third argument is the colour, for two plots it is the title. Name the arguments and the difference stops mattering. When you fill between two plots, the fill keeps an offset only if both plots carry the same one.

### syntax

```
fill(series hline h1, series hline h2, series color color, const string title, const bool fillgaps, input display display) → void
```

### args

- `h1`: series hline
  The first hline object. Required argument.
  types: series hline, simple hline, input hline, const hline, literal hline
- `h2`: series hline
  The second hline object. Required argument.
  types: series hline, simple hline, input hline, const hline, literal hline
- `color?`: series color
  Color of the background fill. Use a color constant such as `color.blue`, a hex color such as `#00ff7f`, or an expression that returns a color, such as `close >= open ? color.yellow : color.blue`. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `title?`: const string
  Title of the created fill object. Optional argument.
  types: const string, literal string
  default: na
- `fillgaps?`: const bool
  Controls continuing fills on gaps, i.e., when one of the plot() calls returns an na value. When true, the last fill will continue on gaps. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Whether the fill is shown: `display.all` (the default) or `display.none`. The other `display.*` constants are not supported here.
  types: input display, const display, literal display
  values: display.all, display.none
  default: display.all

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Fill Example", overlay=true)
// Create two moving averages
ma1 = talib.sma(close, 20)
ma2 = talib.sma(close, 50)
// Plot moving averages
plot1 = plot(ma1, color=color.blue, title="MA 20")
plot2 = plot(ma2, color=color.orange, title="MA 50")
// Fill the area between MA 20 and MA 50
fill(plot1, plot2, color=color.new(color.green, 0.1))
```

### id

function:fill~1

## fill (function)

Shades the band between two plots, or between two horizontal lines. It has two forms and no mixed one, so you cannot fill between a plot and a level, and like the other output calls it must sit at the top level.

The forms differ in argument order, and that is the thing that bites: for two levels the third argument is the colour, for two plots it is the title. Name the arguments and the difference stops mattering. When you fill between two plots, the fill keeps an offset only if both plots carry the same one.

### syntax

```
fill(series hline h1, series hline h2, series float top_value, series float bottom_value, series color top_color, series color bottom_color, const string title, input display display, const bool fillgaps, input bool editable) → void
```

### args

- `h1`: series hline
  The first hline object. Required argument.
  types: series hline, simple hline, input hline, const hline, literal hline
- `h2`: series hline
  The second hline object. Required argument.
  types: series hline, simple hline, input hline, const hline, literal hline
- `top_value`: series float
  Price at which the fill has `top_color`. With `bottom_value` it sets, on each bar, the price range the gradient spans.
  types: series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float
- `bottom_value`: series float
  Price at which the fill has `bottom_color`.
  types: series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float
- `top_color`: series color
  Color of the fill at `top_value`. Between the two values the color changes gradually from `top_color` to `bottom_color`.
  types: series color, simple color, input color, const color, literal color
- `bottom_color`: series color
  Color of the fill at `bottom_value`.
  types: series color, simple color, input color, const color, literal color
- `title?`: const string
  Title of the created fill object. Optional argument.
  types: const string, literal string
  default: na
- `display?`: input display
  Whether the fill is shown: `display.all` (the default) or `display.none`. The other `display.*` constants are not supported here.
  types: input display, const display, literal display
  values: display.all, display.none
  default: display.all
- `fillgaps?`: const bool
  Controls continuing fills on gaps, i.e., when one of the plot() calls returns an na value. When true, the last fill will continue on gaps. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `editable?`: input bool
  If true (the default), the reader can change the fill's colors in the script's settings.
  types: input int, const int, literal int, input float, const float, literal float, input bool, const bool, literal bool
  default: true

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Fill Example", overlay=true)
// Create two moving averages
ma1 = talib.sma(close, 20)
ma2 = talib.sma(close, 50)
// Plot moving averages
plot1 = plot(ma1, color=color.blue, title="MA 20")
plot2 = plot(ma2, color=color.orange, title="MA 50")
// Fill the area between MA 20 and MA 50
fill(plot1, plot2, color=color.new(color.green, 0.1))
```

### id

function:fill~2

## fill (function)

Shades the band between two plots, or between two horizontal lines. It has two forms and no mixed one, so you cannot fill between a plot and a level, and like the other output calls it must sit at the top level.

The forms differ in argument order, and that is the thing that bites: for two levels the third argument is the colour, for two plots it is the title. Name the arguments and the difference stops mattering. When you fill between two plots, the fill keeps an offset only if both plots carry the same one.

### syntax

```
fill(series plot p1, series plot p2, const string title, series color color, const bool fillgaps, input display display) → void
```

### args

- `p1`: series plot
  The first plot object. Required argument.
  types: series plot, simple plot, input plot, const plot, literal plot
- `p2`: series plot
  The second plot object. Required argument.
  types: series plot, simple plot, input plot, const plot, literal plot
- `title?`: const string
  Title of the created fill object. Optional argument.
  types: const string, literal string
  default: na
- `color?`: series color
  Color of the background fill. Use a color constant such as `color.blue`, a hex color such as `#00ff7f`, or an expression that returns a color, such as `close >= open ? color.yellow : color.blue`. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `fillgaps?`: const bool
  Controls continuing fills on gaps, i.e., when one of the plot() calls returns an na value. When true, the last fill will continue on gaps. The default is false.
  types: const int, literal int, const float, literal float, const bool, literal bool
  default: false
- `display?`: input display
  Whether the fill is shown: `display.all` (the default) or `display.none`. The other `display.*` constants are not supported here.
  types: input display, const display, literal display
  values: display.all, display.none
  default: display.all

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Fill Example", overlay=true)
// Create two moving averages
ma1 = talib.sma(close, 20)
ma2 = talib.sma(close, 50)
// Plot moving averages
plot1 = plot(ma1, color=color.blue, title="MA 20")
plot2 = plot(ma2, color=color.orange, title="MA 50")
// Fill the area between MA 20 and MA 50
fill(plot1, plot2, color=color.new(color.green, 0.1))
```

### id

function:fill~3

## fill (function)

Shades the band between two plots, or between two horizontal lines. It has two forms and no mixed one, so you cannot fill between a plot and a level, and like the other output calls it must sit at the top level.

The forms differ in argument order, and that is the thing that bites: for two levels the third argument is the colour, for two plots it is the title. Name the arguments and the difference stops mattering. When you fill between two plots, the fill keeps an offset only if both plots carry the same one.

### syntax

```
fill(series plot plot1, series plot plot2, series float top_value, series float bottom_value, series color top_color, series color bottom_color, const string title, input display display, const bool fillgaps, input bool editable) → void
```

### args

- `plot1`: series plot
  The first plot, the result of a `plot` call.
  types: series plot, simple plot, input plot, const plot, literal plot
- `plot2`: series plot
  The second plot, the result of a `plot` call.
  types: series plot, simple plot, input plot, const plot, literal plot
- `top_value`: series float
  Price at which the fill has `top_color`. With `bottom_value` it sets, on each bar, the price range the gradient spans.
  types: series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float
- `bottom_value`: series float
  Price at which the fill has `bottom_color`.
  types: series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float
- `top_color`: series color
  Color of the fill at `top_value`. Between the two values the color changes gradually from `top_color` to `bottom_color`.
  types: series color, simple color, input color, const color, literal color
- `bottom_color`: series color
  Color of the fill at `bottom_value`.
  types: series color, simple color, input color, const color, literal color
- `title?`: const string
  Title of the created fill object. Optional argument.
  types: const string, literal string
  default: na
- `display?`: input display
  Whether the fill is shown: `display.all` (the default) or `display.none`. The other `display.*` constants are not supported here.
  types: input display, const display, literal display
  values: display.all, display.none
  default: display.all
- `fillgaps?`: const bool
  Controls continuing fills on gaps, i.e., when one of the plot() calls returns an na value. When true, the last fill will continue on gaps. The default is false.
  types: const int, literal int, const float, literal float, const bool, literal bool
  default: false
- `editable?`: input bool
  If true (the default), the reader can change the fill's colors in the script's settings.
  types: input int, const int, literal int, input float, const float, literal float, input bool, const bool, literal bool
  default: true

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Fill Example", overlay=true)
// Create two moving averages
ma1 = talib.sma(close, 20)
ma2 = talib.sma(close, 50)
// Plot moving averages
plot1 = plot(ma1, color=color.blue, title="MA 20")
plot2 = plot(ma2, color=color.orange, title="MA 50")
// Fill the area between MA 20 and MA 50
fill(plot1, plot2, color=color.new(color.green, 0.1))
```

### id

function:fill~4

## fixnan (function)

Takes a series and hands back a series of the same type, with `na` values dealt with.

Four overloads cover bool, colour, float and int. Where `nz` lets you name the replacement, `fixnan` takes no second argument.

### syntax

```
fixnan(series int value) → series int
```

### args

- `value`: series int
  Source used for the calculation.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("fixnan Example", overlay=true)
// Carry the last pivot high forward until the next one
ph = talib.pivothigh(high, 5, 5)
plot(fixnan(ph), title="Last Pivot High", color=color.green)
```

### id

function:fixnan~1

## fixnan (function)

Takes a series and hands back a series of the same type, with `na` values dealt with.

Four overloads cover bool, colour, float and int. Where `nz` lets you name the replacement, `fixnan` takes no second argument.

### syntax

```
fixnan(series float value) → series float
```

### args

- `value`: series float
  Source used for the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("fixnan Example", overlay=true)
// Carry the last pivot high forward until the next one
ph = talib.pivothigh(high, 5, 5)
plot(fixnan(ph), title="Last Pivot High", color=color.green)
```

### id

function:fixnan~2

## fixnan (function)

Takes a series and hands back a series of the same type, with `na` values dealt with.

Four overloads cover bool, colour, float and int. Where `nz` lets you name the replacement, `fixnan` takes no second argument.

### syntax

```
fixnan(series bool value) → series bool
```

### args

- `value`: series bool
  Source used for the calculation.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("fixnan Example", overlay=true)
// Carry the last pivot high forward until the next one
ph = talib.pivothigh(high, 5, 5)
plot(fixnan(ph), title="Last Pivot High", color=color.green)
```

### id

function:fixnan~3

## fixnan (function)

Takes a series and hands back a series of the same type, with `na` values dealt with.

Four overloads cover bool, colour, float and int. Where `nz` lets you name the replacement, `fixnan` takes no second argument.

### syntax

```
fixnan(series color value) → series color
```

### args

- `value`: series color
  Source used for the calculation.
  types: series color, simple color, input color, const color, literal color

### returnedType

series color

### example

```lipi
//@lipi=2
indicator("fixnan Example", overlay=true)
// Carry the last pivot high forward until the next one
ph = talib.pivothigh(high, 5, 5)
plot(fixnan(ph), title="Last Pivot High", color=color.green)
```

### id

function:fixnan~4

## float (type)

A number with a fractional part, written `1.5`. It has no fields.

Most market data is float: the bar's prices, its volume and the averaged prices are all float series.

### example

```lipi
//@lipi=2
indicator("float Example", overlay=true)
float midPoint = (high + low) / 2
plot(midPoint, title="Mid Point", color=color.blue)
```

### id

type:float

## float (function)

Converts a value to a float.

It accepts an int as well as a float, so it is the conversion to use when a calculation must not round.

### syntax

```
float(const float value) → const float
```

### args

- `value`: const float
  The value to convert to the specified type, usually na.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("float() Example", overlay=false)
// Dividing as floats keeps the fractional part
ratio = float(bar_index) / 7
plot(ratio, title="Bar Index / 7", color=color.blue)
```

### id

function:float~1

## float (function)

Converts a value to a float.

It accepts an int as well as a float, so it is the conversion to use when a calculation must not round.

### syntax

```
float(input float value) → input float
```

### args

- `value`: input float
  The value to convert to the specified type, usually na.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("float() Example", overlay=false)
// Dividing as floats keeps the fractional part
ratio = float(bar_index) / 7
plot(ratio, title="Bar Index / 7", color=color.blue)
```

### id

function:float~2

## float (function)

Converts a value to a float.

It accepts an int as well as a float, so it is the conversion to use when a calculation must not round.

### syntax

```
float(simple float value) → simple float
```

### args

- `value`: simple float
  The value to convert to the specified type, usually na.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("float() Example", overlay=false)
// Dividing as floats keeps the fractional part
ratio = float(bar_index) / 7
plot(ratio, title="Bar Index / 7", color=color.blue)
```

### id

function:float~3

## float (function)

Converts a value to a float.

It accepts an int as well as a float, so it is the conversion to use when a calculation must not round.

### syntax

```
float(series float value) → series float
```

### args

- `value`: series float
  The value to convert to the specified type, usually na.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("float() Example", overlay=false)
// Dividing as floats keeps the fractional part
ratio = float(bar_index) / 7
plot(ratio, title="Bar Index / 7", color=color.blue)
```

### id

function:float~4

## font (type)

Font family constants for text drawn on boxes, labels, and table cells.

Pass them to `text_font_family` on `box.new` and `label.new`, to `table.cell`, or to the matching `*.set_text_font_family` setter. The parameter type is `font`, not `string`.

### fields

- `family_default`
  Default proportional font for drawing text.
- `family_monospace`
  Fixed-width font for drawing text.

### example

```lipi
//@lipi=2
indicator("font Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Mono", text_font_family=font.family_monospace, size=size.small)
}
```

### id

type:font

## font (enum)

Font family constants for text drawn on boxes, labels, and table cells.

Pass them to `text_font_family` on `box.new` and `label.new`, to `table.cell`, or to the matching `*.set_text_font_family` setter. The parameter type is `font`, not `string`.

### fields

- `family_default`
  Default proportional font for drawing text.
- `family_monospace`
  Fixed-width font for drawing text.

### example

```lipi
//@lipi=2
indicator("font Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Mono", text_font_family=font.family_monospace, size=size.small)
}
```

### id

enum:font

## for in (keyword)

Loops over each element of an array. The name after `in` must be a variable that holds an array; the loop variable is assigned the current element on every pass.

`break` leaves the loop and `continue` starts the next element. Like `while` and `for ... to`, the loop body is a braced block.

### syntax

```
for <identifier> in <identifier> {
	...
	break
	...
	continue
	...
}
```

### example

```lipi
//@lipi=2
indicator("for in Example", overlay=false)
values = array.from(1, 2, 3, 4, 5)
sum = 0
for v in values {
    sum += v
}
plot(sum, title="Sum of array", color=color.blue)
```

### id

keyword:for in

## for to (keyword)

Counts from a start value to an end value, using a counter variable. The end value is included (for `1 to 5` the counter takes 1, 2, 3, 4 and 5), except when the start and the end are equal: then the body does not run at all. Both bounds are expressions; the counter is a simple identifier assigned on each pass.

An optional `step` expression changes the increment (negative steps count down). `break` leaves the loop and `continue` starts the next iteration.

### syntax

```
for <identifier> = <expression> to <expression> [step <expression>] {
	...
	break
	...
	continue
	...
}
```

### example

```lipi
//@lipi=2
indicator("for to Example", overlay=false)
total = 0
for i = 1 to 5 {
    total += i
}
// Same total with an explicit step
for j = 0 to 10 step 2 {
    total += 1
}
plot(total, title="Running total", color=color.orange)
```

### id

keyword:for to

## func (keyword)

Declares an ordinary user function (not a type method). The parameter list may be empty, e.g. `func pi() => 3.14159`.

Use `def` when the first parameter is a typed receiver for a type function; use `func` for everything else.

A body is either a braced block or a single expression after an arrow; the arrow form may return a tuple for multiple values.

### syntax

```
func <function_name>(<data_type> <param_name> [= <default_value>], ...) {
	<function_body>
}
		
func <function_name>(<data_type> <param_name> [= <default_value>], ...) => <expression>
```

### notes

- A function body may call a drawing function such as `label.new`; it compiles. The chart-output calls listed under `if`, for example `plot`, are rejected inside a function.
- A braced body with no `return` is valid: the function returns nothing. A function that returns a value must end every path in a `return`; otherwise the compiler says "The `<name>()` function is missing return statement."

### example

```lipi
//@lipi=2
indicator("func Example", overlay=true)
// A braced body
func spread(float h, float l) {
    return h - l
}
// An arrow body returning two values
func bounds(int len) => [talib.highest(high, len), talib.lowest(low, len)]
[upper, lower] = bounds(20)
plot(upper, title="Upper", color=color.green)
plot(lower, title="Lower", color=color.red)
plot(lower + spread(upper, lower) / 2, title="Middle", color=color.gray)
```

### id

keyword:func

## high (variable)

The bar's highest traded price.

Pair it with `low` when you want the bar's range; the difference between the two is a series like its parts.

### type

series float

### example

```lipi
//@lipi=2
indicator("High Example", overlay=true)
plot(high, color=color.green, title="High Price")
```

### id

variable:high

## hl2 (variable)

The bar's high and low, averaged: its midpoint. Supplied so you need not write the arithmetic.

Four of these averaged prices exist. Each is a float series like the values it averages, so one can stand anywhere a price is wanted.

### type

series float

### example

```lipi
//@lipi=2
indicator("HL2 Example", overlay=true)
plot(hl2, color=color.orange, title="HL2 (Midpoint of High & Low)")
```

### id

variable:hl2

## hlc3 (variable)

The bar's high, low and close, averaged.

### type

series float

### example

```lipi
//@lipi=2
indicator("HL2 Example", overlay=true)
plot(hlc3, color=color.orange, title="HLC3 (Midpoint of High, Low and Close)")
```

### id

variable:hlc3

## hlcc4 (variable)

The bar's high, low and close with the close counted twice, averaged.

The name records the weighting: four components, of which two are the close.

### type

series float

### example

```lipi
//@lipi=2
indicator("HL2 Example", overlay=true)
plot(hlcc4, color=color.orange, title="HLCC4 (Midpoint of High, Low, Close and Close)")
```

### id

variable:hlcc4

## hline (type)

The value `hline` gives back once it has drawn a horizontal level.

It plays the same part as a plot value in the other `fill` form: two hline values shade the band between two levels. Mixing one with a plot is not accepted — the two forms of `fill` are separate. No fields.

### example

```lipi
//@lipi=2
indicator("hline Example", overlay=true)
// Draw a horizontal line at 100
hline(100, title="Static Line", color=color.red, linewidth=2, style=hlineStyle.dotted)
```

### id

type:hline

## hline (function)

Draws a horizontal line at a fixed price.

The price is input-form, so it cannot follow the data — a line that has to move is a plot, not a level. `hline` returns a value, which is what lets you pass two levels to `fill`.

### syntax

```
hline(input float price, const string title, input color color, input int linewidth, input hlineStyle style, input display display, input string format) → series hline
```

### args

- `price`: input float
  Price value at which the object will be rendered. Required argument.
  types: input float, input int, const int, literal int, const float, literal float
- `title?`: const string
  Title of the object.
  types: const string, literal string
  default: na
- `color?`: input color
  Color of the rendered line. Must be an `input.color` value or a constant expression; a series color is refused ("An argument of `series color` type was used but a `input color` is expected."). Optional argument.
  types: input color, const color, literal color
  default: na
- `linewidth?`: input int
  Width of the rendered line. Default value is 1.
  types: input int, const int, literal int
  default: 1
- `style?`: input hlineStyle
  Style of the rendered line. Possible values are: hlineStyle.solid, hlineStyle.dotted, hlineStyle.dashed. Optional argument.
  types: input hlineStyle, const hlineStyle, literal hlineStyle
  values: hlineStyle.solid, hlineStyle.dashed, hlineStyle.dotted
  default: hlineStyle.solid
- `display?`: input display
  Controls where the hline is shown (pane, price scale, status line, data window). Use display.* constants; combine with +. Default is display.all.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all
- `format?`: input string
  Format of the displayed values: `format.price`, `format.percent` or `format.volume`. The default is an empty string, which uses the script's format. `format.inherit` and `format.mintick` pass the editor's check but are refused when the script is added to the chart.
  types: input string, const string, literal string
  values: format.percent, format.price, format.volume
  default: ""

### returnedType

series hline

### example

```lipi
//@lipi=2
indicator("Horizontal Line Example", overlay=true)
// Draw a horizontal line at 4000
hline(4000, "Support Level", color=color.blue, linewidth=2, style=hlineStyle.dashed)
```

### id

function:hline

## hlineStyle (type)

Three line styles for a horizontal level: `solid`, `dashed` and `dotted`.

The smallest of the sets, and the only one used by `hline`. It is not interchangeable with `plotStyle`.

### fields

- `solid`
  A solid line (default).
- `dashed`
  A dashed line.
- `dotted`
  A dotted line.

### example

```lipi
//@lipi=2
indicator("hlineStyle Example", overlay=false)
hline(70, title="Overbought", color=color.red, style=hlineStyle.dashed)
hline(50, title="Middle", color=color.gray, style=hlineStyle.dotted)
hline(30, title="Oversold", color=color.green, style=hlineStyle.solid)
plot(talib.rsi(close, 14), title="RSI", color=color.blue)
```

### id

type:hlineStyle

## hlineStyle (enum)

Three line styles for a horizontal level: `solid`, `dashed` and `dotted`.

The smallest of the sets, and the only one used by `hline`. It is not interchangeable with `plotStyle`.

### fields

- `solid`
  A solid line (default).
- `dashed`
  A dashed line.
- `dotted`
  A dotted line.

### example

```lipi
//@lipi=2
indicator("hlineStyle Example", overlay=false)
hline(70, title="Overbought", color=color.red, style=hlineStyle.dashed)
hline(50, title="Middle", color=color.gray, style=hlineStyle.dotted)
hline(30, title="Oversold", color=color.green, style=hlineStyle.solid)
plot(talib.rsi(close, 14), title="RSI", color=color.blue)
```

### id

enum:hlineStyle

## hour (variable)

The hour of the bar being evaluated.

### type

series int

### example

```lipi
//@lipi=2
indicator("hour Example", overlay=true)
// Highlight the first trading hour
bgcolor(hour == 9 ? color.new(color.blue, 0.15) : na)
```

### id

variable:hour

## hour (function)

The hour of a time you supply.

Because the timezone is an argument rather than an assumption, a script can ask the same question in two zones.

### syntax

```
hour(series int time, series string timezone) → series int
```

### args

- `time`: series int
  UNIX time, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `timezone?`: series string
  The time zone the value is read in: an IANA time zone database name (for example "America/New_York") or "UTC". Unlike `timestamp`, `time` and `str.format_time`, this function does not accept offset notation such as "UTC-5" or "GMT+0530": a name that cannot be loaded gives 0, not `na`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Hour Function Example", overlay=true)
// Get current bar hour
currentHour = hour(time)
// Plot hour in Data Window
plot(currentHour, title="Current Hour")
```

### id

function:hour

## if (keyword)

Chooses which block of statements runs. Any number of `else if` arms may follow, and one `else` arm may close it; both are optional.

It is a statement, not an expression: it decides which block runs rather than producing a value. And it opens a scope of its own, which is why a chart-output call placed inside one is rejected — put the condition in an argument instead, and leave the call at the top level.

### syntax

```
if <condition> {
	<true_block>
} else if <condition> {
	<true_block>
} else {
	<false_block>
}
```

### notes

- A drawing call such as `label.new` compiles inside an `if` block. The chart-output calls `plot`, `plotshape`, `plotchar`, `plotarrow`, `plotbar`, `plotcandle`, `bgcolor`, `barcolor`, `hline`, `fill` and `alertcondition` are rejected there; `alert` is accepted.
- `switch <value> { case <value>: ... default: ... }` also chooses a block and compiles.

### example

```lipi
//@lipi=2
indicator("If Function Example - Moving Average Strategy", overlay=true)
// Define Moving Averages
shortMA = talib.sma(close, 10)
longMA = talib.sma(close, 50)
// Function to determine signal color
func getSignalColor() {
    if shortMA > longMA {
        return color.green
    } else {
        return color.blue
    }
}
// Plot Moving Averages
plot(shortMA, title="Short MA (10)", color=color.blue)
plot(longMA, title="Long MA (50)", color=color.orange)
bgcolor(getSignalColor())
```

### id

keyword:if

## indicator (function)

Declares the script and names it. Put it first.

Only `title` is required, and every parameter is const-form, so none of them can be built from series data or handed a value that came out of an input.

### syntax

```
indicator(const string title, const string shorttitle, const bool overlay, const string format, const int precision, const scale scale, const bool calc_on_every_tick, const int max_lines_count, const int max_labels_count, const int max_boxes_count, const int calc_bars_count, const int max_polylines_count, const bool behind_chart) → void
```

### args

- `title`: const string
  The title of the script. It is displayed on the chart when no shorttitle argument is used, and becomes the script's default title when you publish it.
  types: const string, literal string
- `shorttitle?`: const string
  The script's display name on charts. If specified, it will replace the title argument in most chart-related windows. Optional. The default is the argument used for title. At most 128 characters: a longer name passes the editor's check but is refused when the script is added to the chart.
  types: const string, literal string
- `overlay?`: const bool
  If true, the indicator will be displayed over the chart. If false, it will be added in a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `format?`: const string
  How the script's values are formatted on the price scale and in the status line: `format.inherit` (the default: as the chart's symbol), `format.price`, `format.volume` or `format.percent`. Any other `format.*` constant passes the editor's check but is refused when the script is added to the chart.
  types: const string, literal string
  values: format.inherit, format.percent, format.price, format.volume
  default: format.inherit
- `precision?`: const int
  Number of digits after the decimal point in the script's displayed values. Accepted, but the current compiler does not pass it on, so it has no effect yet.
  types: const int, literal int
  default: 0
- `scale?`: const scale
  Which price scale the script uses: `scale.left`, `scale.right`, or `scale.none`. Optional. Default is `scale.none`.
  types: const scale, literal scale
  default: scale.none
- `calc_on_every_tick?`: const bool
  If true, the indicator recalculates on every realtime tick update of the last bar. If false, it recalculates only when the bar is confirmed. Optional. The default is true.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: true
- `max_lines_count?`: const int
  Maximum lines the script may keep. Default is 50, and the highest accepted value is 500. Past the limit, the oldest lines are trimmed.
  types: const int, literal int
  default: 50
- `max_labels_count?`: const int
  Maximum labels the script may keep. Default is 50, and the highest accepted value is 500. Past the limit, the oldest labels are trimmed.
  types: const int, literal int
  default: 50
- `max_boxes_count?`: const int
  Maximum boxes the script may keep. Default is 50, and the highest accepted value is 500. Past the limit, the oldest boxes are trimmed.
  types: const int, literal int
  default: 50
- `calc_bars_count?`: const int
  Limits how many historical bars are calculated (0 means no limit). Must be 0 or a positive integer; a negative value passes the editor's check but is refused when the script is added to the chart.
  types: const int, literal int
  default: 0
- `max_polylines_count?`: const int
  Maximum polylines the script may keep. Default is 50, and the highest accepted value is 100. Past the limit, the oldest polylines are trimmed.
  types: const int, literal int
  default: 50
- `behind_chart?`: const bool
  If true, plot drawings render behind the chart candles. Optional. Default is true.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: true

### returnedType

void

### example

```lipi
//@lipi=2
indicator(title="Simple Moving Average", overlay=true,shorttitle="SMA")
sma_value = talib.sma(close, 14)
plot(sma_value, title="SMA 14", color=color.blue, linewidth=2)
```

### id

function:indicator

## input (function)

Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.

Six forms exist. Give it a bool and you get a bool back; give it a colour, a float, an int or a string and the same holds. The sixth takes a series and returns a `series float`, which is how you offer a choice of chart data without naming `input.source`. There are no bounds and no step here — for those, use `input.int` or `input.float`.

### syntax

```
input(const color defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input color
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

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input()` cannot be `na`." Any constant expression of type color is accepted, such as `color.red` or `color.new(color.red, 0.5)`.

### example

```lipi
//@lipi=2
indicator("Customizable Moving Average", overlay=true)
length = input(14, title="SMA Length")
sma_value = talib.sma(close, length)
plot(sma_value, title="SMA", color=color.blue, linewidth=2)
```

### id

function:input~1

## input (function)

Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.

Six forms exist. Give it a bool and you get a bool back; give it a colour, a float, an int or a string and the same holds. The sixth takes a series and returns a `series float`, which is how you offer a choice of chart data without naming `input.source`. There are no bounds and no step here — for those, use `input.int` or `input.float`.

### syntax

```
input(const string defval, const string title, [const string...] options, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input string
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

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input()` cannot be `na`." Any constant expression of type string is accepted, such as `"a" + "b"`.

### example

```lipi
//@lipi=2
indicator("Customizable Moving Average", overlay=true)
length = input(14, title="SMA Length")
sma_value = talib.sma(close, length)
plot(sma_value, title="SMA", color=color.blue, linewidth=2)
```

### id

function:input~2

## input (function)

Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.

Six forms exist. Give it a bool and you get a bool back; give it a colour, a float, an int or a string and the same holds. The sixth takes a series and returns a `series float`, which is how you offer a choice of chart data without naming `input.source`. There are no bounds and no step here — for those, use `input.int` or `input.float`.

### syntax

```
input(const int defval, const string title, [const int...] options, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input int
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

input int

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input()` cannot be `na`." Any constant expression of type int is accepted, such as `-5` or `2 * 3`.

### example

```lipi
//@lipi=2
indicator("Customizable Moving Average", overlay=true)
length = input(14, title="SMA Length")
sma_value = talib.sma(close, length)
plot(sma_value, title="SMA", color=color.blue, linewidth=2)
```

### id

function:input~3

## input (function)

Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.

Six forms exist. Give it a bool and you get a bool back; give it a colour, a float, an int or a string and the same holds. The sixth takes a series and returns a `series float`, which is how you offer a choice of chart data without naming `input.source`. There are no bounds and no step here — for those, use `input.int` or `input.float`.

### syntax

```
input(const float defval, const string title, [const float...] options, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input float
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

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input()` cannot be `na`." Any constant expression of type float is accepted, such as `-5.5` or `2.5 * 2`.

### example

```lipi
//@lipi=2
indicator("Customizable Moving Average", overlay=true)
length = input(14, title="SMA Length")
sma_value = talib.sma(close, length)
plot(sma_value, title="SMA", color=color.blue, linewidth=2)
```

### id

function:input~4

## input (function)

Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.

Six forms exist. Give it a bool and you get a bool back; give it a colour, a float, an int or a string and the same holds. The sixth takes a series and returns a `series float`, which is how you offer a choice of chart data without naming `input.source`. There are no bounds and no step here — for those, use `input.int` or `input.float`.

### syntax

```
input(series float defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → series float
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

series float

### notes

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input()` cannot be `na`." A built-in series such as `close` or `hlc3` is accepted.

### example

```lipi
//@lipi=2
indicator("Customizable Moving Average", overlay=true)
length = input(14, title="SMA Length")
sma_value = talib.sma(close, length)
plot(sma_value, title="SMA", color=color.blue, linewidth=2)
```

### id

function:input~5

## input (function)

Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.

Six forms exist. Give it a bool and you get a bool back; give it a colour, a float, an int or a string and the same holds. The sixth takes a series and returns a `series float`, which is how you offer a choice of chart data without naming `input.source`. There are no bounds and no step here — for those, use `input.int` or `input.float`.

### syntax

```
input(const bool defval, const string title, const string tooltip, const string inline, const string group, const bool confirm, const display display) → input bool
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

- The default `defval` must be a value: `na` is rejected with "Argument `defval` of `input()` cannot be `na`." Any constant expression of type bool is accepted, such as `true`.

### example

```lipi
//@lipi=2
indicator("Customizable Moving Average", overlay=true)
length = input(14, title="SMA Length")
sma_value = talib.sma(close, length)
plot(sma_value, title="SMA", color=color.blue, linewidth=2)
```

### id

function:input~6

## int (type)

A whole number. One of the five data types the grammar names directly.

Written as a bare number: `14`. It has no fields.

### example

```lipi
//@lipi=2
indicator("Int Keyword Example", overlay=true)
// Declare an integer variable for moving average length
int maLength = 20
// Calculate the Simple Moving Average (SMA) using the integer variable
smaValue = talib.sma(close, maLength)
// Plot the moving average
plot(smaValue, title="20-period SMA", color=color.blue, linewidth=2)
```

### id

type:int

## int (function)

Converts a value to an `int`.

Four overloads, one per form type; the form you pass in is the form you get back. At compile time the argument may be `int` or `float`; floats are truncated toward zero.

### syntax

```
int(const float value) → const int
```

### args

- `value`: const float
  Value to convert. Accepts `int` or `float` (truncated toward zero). `na` stays `na`.
  types: const float, const int, literal int, literal float

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("int() Example", overlay=true)
// Round down to a whole number, then pass it through int()
int wholeClose = int(math.floor(close))
plot(wholeClose, title="Close Without Decimals", color=color.blue)
```

### id

function:int~1

## int (function)

Converts a value to an `int`.

Four overloads, one per form type; the form you pass in is the form you get back. At compile time the argument may be `int` or `float`; floats are truncated toward zero.

### syntax

```
int(input float value) → input int
```

### args

- `value`: input float
  Value to convert. Accepts `int` or `float` (truncated toward zero). `na` stays `na`.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("int() Example", overlay=true)
// Round down to a whole number, then pass it through int()
int wholeClose = int(math.floor(close))
plot(wholeClose, title="Close Without Decimals", color=color.blue)
```

### id

function:int~2

## int (function)

Converts a value to an `int`.

Four overloads, one per form type; the form you pass in is the form you get back. At compile time the argument may be `int` or `float`; floats are truncated toward zero.

### syntax

```
int(simple float value) → simple int
```

### args

- `value`: simple float
  Value to convert. Accepts `int` or `float` (truncated toward zero). `na` stays `na`.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("int() Example", overlay=true)
// Round down to a whole number, then pass it through int()
int wholeClose = int(math.floor(close))
plot(wholeClose, title="Close Without Decimals", color=color.blue)
```

### id

function:int~3

## int (function)

Converts a value to an `int`.

Four overloads, one per form type; the form you pass in is the form you get back. At compile time the argument may be `int` or `float`; floats are truncated toward zero.

### syntax

```
int(series float value) → series int
```

### args

- `value`: series float
  Value to convert. Accepts `int` or `float` (truncated toward zero). `na` stays `na`.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("int() Example", overlay=true)
// Round down to a whole number, then pass it through int()
int wholeClose = int(math.floor(close))
plot(wholeClose, title="Close Without Decimals", color=color.blue)
```

### id

function:int~4

## intra (keyword)

The second of the two persistence keywords the grammar accepts, and the only other one.

A value declared `intra` is kept across the repeated runs of the bar that is still forming, and is cleared when a new bar starts: the next bar starts from the initializer again. Use it to carry something across recalculations of one bar; use `static` to carry something across bars.

The difference from `static` is when a value is committed, not only how long it lives. A `static` value is stored when a bar is confirmed, so each run of a forming bar starts from the value stored when the last bar closed; an `intra` value is kept between the runs of the same bar and dropped when the next bar starts. On historical bars a bar usually runs once, so `intra` then behaves like an ordinary variable; a strategy with `calc_on_order_fills=true` runs a historical bar again after a fill, and an `intra` value carries across those runs until the bar finishes.

### syntax

```
intra <data_type> <variable_name> = <expression>
```

### example

```lipi
//@lipi=2
indicator("intra Example", overlay=false)
// Declare a persistent variable that resets each new bar
intra int count = 0
// Increase count on each price update within the same bar
count := count + 1
// Plot the intrabar update count as a line
plot(count, title="Intrabar Execution Count", color=color.blue)
```

### id

keyword:intra

## label (function)

Converts `value` to the `label` type. It is used almost only as `label(na)`, to declare a label variable that has no drawing yet, so that its type is known before the first drawing is assigned.

### syntax

```
label(series label value) → series label
```

### args

- `value`: series label
  The value to convert to the specified type, usually na.
  types: series label, simple label, input label, const label, literal label

### returnedType

series label

### example

```lipi
//@lipi=2
indicator("label() Example", overlay=true)
// Keep a single label, moved to the latest bar
static label lbl = label(na)
if barstate.islast {
    if not na(lbl) {
        label.delete(lbl)
    }
    lbl := label.new(bar_index, high, text="Last bar")
}
```

### id

function:label

## last_bar_index (variable)

Bar index of the last bar on the chart (the rightmost bar), including the realtime tip when one is forming.

Unlike `bar_index`, this value is the same on every bar in a run: it always points at the chart's final bar.

### type

series int

### example

```lipi
//@lipi=2
indicator("last_bar_index Example", overlay=true)
isLast = bar_index == last_bar_index
bgcolor(isLast ? color.new(color.orange, 0.85) : na)
```

### id

variable:last_bar_index

## last_bar_time (variable)

Open time of the last bar on the chart, in UNIX milliseconds (same convention as `time`).

Matches the timestamp of the rightmost bar, including the unconfirmed realtime bar when present.

### type

series int

### example

```lipi
//@lipi=2
indicator("last_bar_time Example", overlay=true)
if bar_index == last_bar_index {
    label.new(bar_index, high, text=str.format_time(math.floor(last_bar_time / 1000), "2006-01-02 15:04"), style=label.style_label_down)
}
```

### id

variable:last_bar_time

## line (function)

Converts `value` to the `line` type. It is used almost only as `line(na)`, to declare a line variable that has no drawing yet, so that its type is known before the first drawing is assigned.

### syntax

```
line(series line value) → series line
```

### args

- `value`: series line
  The value to convert to the specified type, usually na.
  types: series line, simple line, input line, const line, literal line

### returnedType

series line

### example

```lipi
//@lipi=2
indicator("line() Example", overlay=true)
static line lastLine = line(na)
if barstate.islast {
    lastLine := line.new(bar_index[20], close[20], bar_index, close, color=color.blue)
}
```

### id

function:line

## linefill (function)

Converts `value` to the `linefill` type. It is used almost only as `linefill(na)`, to declare a linefill variable that has no drawing yet, so that its type is known before the first drawing is assigned.

### syntax

```
linefill(series linefill value) → series linefill
```

### args

- `value`: series linefill
  The value to convert to the specified type, usually na.
  types: series linefill, simple linefill, input linefill, const linefill, literal linefill

### returnedType

series linefill

### example

```lipi
//@lipi=2
indicator("linefill() Example", overlay=true)
static linefill band = linefill(na)
if barstate.islast {
    upper = line.new(bar_index[20], high[20], bar_index, high, color=color.green)
    lower = line.new(bar_index[20], low[20], bar_index, low, color=color.red)
    band := linefill.new(upper, lower, color.new(color.gray, 0.2))
}
```

### id

function:linefill

## location (type)

Five places a marker can sit: `abovebar`, `belowbar`, `top`, `bottom` and `absolute`.

The first two are relative to the bar; `top` and `bottom` are relative to the pane; `absolute` places the mark at a price. It is the `location` parameter of `plotshape` and `plotchar`, and `plotarrow` has no such parameter at all.

### fields

- `abovebar`
  Places the element above the current bar.
- `belowbar`
  Places the element below the current bar.
- `top`
  Places the element at the top of the chart.
- `bottom`
  Places the element at the bottom of the chart.
- `absolute`
  Places the element at a specific price level.

### example

```lipi
//@lipi=2
indicator("location Example", overlay=true)
plotshape(close > open, title="Up Bar", location=location.belowbar, shape=shape.triangleup, color=color.green)
plotshape(close < open, title="Down Bar", location=location.abovebar, shape=shape.triangledown, color=color.red)
```

### id

type:location

## location (enum)

Five places a marker can sit: `abovebar`, `belowbar`, `top`, `bottom` and `absolute`.

The first two are relative to the bar; `top` and `bottom` are relative to the pane; `absolute` places the mark at a price. It is the `location` parameter of `plotshape` and `plotchar`, and `plotarrow` has no such parameter at all.

### fields

- `abovebar`
  Places the element above the current bar.
- `belowbar`
  Places the element below the current bar.
- `top`
  Places the element at the top of the chart.
- `bottom`
  Places the element at the bottom of the chart.
- `absolute`
  Places the element at a specific price level.

### example

```lipi
//@lipi=2
indicator("location Example", overlay=true)
plotshape(close > open, title="Up Bar", location=location.belowbar, shape=shape.triangleup, color=color.green)
plotshape(close < open, title="Down Bar", location=location.abovebar, shape=shape.triangledown, color=color.red)
```

### id

enum:location

## low (variable)

The bar's lowest traded price.

### type

series float

### example

```lipi
//@lipi=2
indicator("Low Price Example", overlay=true)
lowestPrice = talib.lowest(low, 10)
plot(lowestPrice, color=color.red, title="Lowest Price (10 Bars)")
```

### id

variable:low

## minute (variable)

The minute of the bar being evaluated.

### type

series int

### example

```lipi
//@lipi=2
indicator("Minute-Based Signal", overlay=true)
isEvenMinute = (minute % 2 == 0)
plotshape(isEvenMinute, location=location.abovebar, color=color.green, title="Even Minute Signal")
```

### id

variable:minute

## minute (function)

The minute of a time you supply.

### syntax

```
minute(series int time, series string timezone) → series int
```

### args

- `time`: series int
  UNIX time, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `timezone?`: series string
  The time zone the value is read in: an IANA time zone database name (for example "America/New_York") or "UTC". Unlike `timestamp`, `time` and `str.format_time`, this function does not accept offset notation such as "UTC-5" or "GMT+0530": a name that cannot be loaded gives 0, not `na`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Minute Function Example", overlay=true)
// Get current bar minute
currentMinute = minute(time)
// Plot minute in Data Window
plot(currentMinute, title="Current Minute")
```

### id

function:minute

## month (variable)

The month of the bar being evaluated.

As with the other date parts, there is a function of the same name that takes a time and a timezone instead.

### type

series int

### example

```lipi
//@lipi=2
indicator("Monthly Signal Example", overlay=true)
isDecember = (month == 12)
plot(isDecember ? close : na, color=color.blue, title="December Close")
```

### id

variable:month

## month (function)

The month of a time you supply.

Same arguments as `year`: the time is required and the timezone is optional.

### syntax

```
month(series int time, series string timezone) → series int
```

### args

- `time`: series int
  UNIX time, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `timezone?`: series string
  The time zone the value is read in: an IANA time zone database name (for example "America/New_York") or "UTC". Unlike `timestamp`, `time` and `str.format_time`, this function does not accept offset notation such as "UTC-5" or "GMT+0530": a name that cannot be loaded gives 0, not `na`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Month Function Example", overlay=true)
// Get current bar month
currentMonth = month(time)
// Plot month in Data Window
plot(currentMonth, title="Current Month")
```

### id

function:month

## na (constant)

Stands for a missing value. A series is `na` where there is no data yet, for example `close[1]` on the first bar, and a plot or colour that is `na` is simply not drawn.

Test for it with `na(x)`, never with `x == na`, and replace it with `nz(x, alternative)`.

### type

const na

### example

```lipi
//@lipi=2
indicator("na Example", overlay=true)
// Plot only on up bars: na values leave gaps
plot(close > open ? close : na, title="Up Closes", color=color.green, style=plotStyle.linebr)
// na(close[1]) is true on the first bar only
bgcolor(na(close[1]) ? color.new(color.blue, 0.3) : na)
```

### id

constant:na

## na (function)

Tests whether a value is absent. It takes any type and gives back a bool.

This is the test a script needs often, because so much reads `na` when there is nothing behind it: an instrument property that is unknown, an orderflow figure on a bar with no footprint data, a colour function handed an `na`.

### syntax

```
na(series <any_type> value) → series bool
```

### args

- `value`: series <any_type>
  Value to be tested.

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("NA Example", overlay=true)
val = close > open ? close : na
isNa = na(val)
plot(val, color=color.blue, title="Value (May be NA)")
plot(isNa ? 1 : 0, color=color.red, title="Is NA (1 = True, 0 = False)")
```

### id

function:na

## not (keyword)

Negates the expression that follows it.

The third of the three logical operators with two spellings, and the only one that takes a single operand rather than two.

### syntax

```
!expr0 | not expr0
```

### example

```lipi
//@lipi=2
indicator("not Example", overlay=true)
aboveMA = close > talib.sma(close, 50)
// not inverts the condition
bgcolor(not aboveMA ? color.new(color.red, 0.15) : na)
```

### id

keyword:not

## nz (function)

Takes a value and an alternative of the same type, and stands in for the value where it is absent.

Five overloads, one per data type. The alternative is optional. When it is left out, `nz` uses 0 for an int or a float, an empty string for a string, false for a bool and `#483D8B` for a color.

### syntax

```
nz(series int value, series int alt) → series int
```

### args

- `value`: series int
  The value to check.
  types: series int, simple int, input int, const int, literal int
- `alt?`: series int
  The alternative to use in its place. Optional, and of the same type as `value`.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("nz Example", overlay=false)
// On the first bar close[1] is na: use the current close instead
prevClose = nz(close[1], close)
plot(close - prevClose, title="Change", color=color.blue)
```

### id

function:nz~1

## nz (function)

Takes a value and an alternative of the same type, and stands in for the value where it is absent.

Five overloads, one per data type. The alternative is optional. When it is left out, `nz` uses 0 for an int or a float, an empty string for a string, false for a bool and `#483D8B` for a color.

### syntax

```
nz(series float value, series float alt) → series float
```

### args

- `value`: series float
  The value to check.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `alt?`: series float
  The alternative to use in its place. Optional, and of the same type as `value`.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: 0

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("nz Example", overlay=false)
// On the first bar close[1] is na: use the current close instead
prevClose = nz(close[1], close)
plot(close - prevClose, title="Change", color=color.blue)
```

### id

function:nz~2

## nz (function)

Takes a value and an alternative of the same type, and stands in for the value where it is absent.

Five overloads, one per data type. The alternative is optional. When it is left out, `nz` uses 0 for an int or a float, an empty string for a string, false for a bool and `#483D8B` for a color.

### syntax

```
nz(series string value, series string alt) → series string
```

### args

- `value`: series string
  The value to check.
  types: series string, simple string, input string, const string, literal string
- `alt?`: series string
  The alternative to use in its place. Optional, and of the same type as `value`.
  types: series string, simple string, input string, const string, literal string
  default: ""

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("nz Example", overlay=false)
// On the first bar close[1] is na: use the current close instead
prevClose = nz(close[1], close)
plot(close - prevClose, title="Change", color=color.blue)
```

### id

function:nz~3

## nz (function)

Takes a value and an alternative of the same type, and stands in for the value where it is absent.

Five overloads, one per data type. The alternative is optional. When it is left out, `nz` uses 0 for an int or a float, an empty string for a string, false for a bool and `#483D8B` for a color.

### syntax

```
nz(series bool value, series bool alt) → series bool
```

### args

- `value`: series bool
  The value to check.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
- `alt?`: series bool
  The alternative to use in its place. Optional, and of the same type as `value`.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: false

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("nz Example", overlay=false)
// On the first bar close[1] is na: use the current close instead
prevClose = nz(close[1], close)
plot(close - prevClose, title="Change", color=color.blue)
```

### id

function:nz~4

## nz (function)

Takes a value and an alternative of the same type, and stands in for the value where it is absent.

Five overloads, one per data type. The alternative is optional. When it is left out, `nz` uses 0 for an int or a float, an empty string for a string, false for a bool and `#483D8B` for a color.

### syntax

```
nz(series color value, series color alt) → series color
```

### args

- `value`: series color
  The value to check.
  types: series color, simple color, input color, const color, literal color
- `alt?`: series color
  The alternative to use in its place. Optional, and of the same type as `value`.
  types: series color, simple color, input color, const color, literal color
  default: #483D8B

### returnedType

series color

### example

```lipi
//@lipi=2
indicator("nz Example", overlay=false)
// On the first bar close[1] is na: use the current close instead
prevClose = nz(close[1], close)
plot(close - prevClose, title="Change", color=color.blue)
```

### id

function:nz~5

## ohlc4 (variable)

The bar's four values, open, high, low and close, averaged with equal weight.

### type

series float

### example

```lipi
//@lipi=2
indicator("OHLC4 Example", overlay=true)
averagePrice = ohlc4
plot(averagePrice, color=color.orange, title="OHLC4 Price")
```

### id

variable:ohlc4

## oi (variable)

Open interest for the bar. It is 0, not `na`, where the bar carries no open-interest data.

This single name is the whole of the open-interest surface. There is no open-interest namespace and no second name.

### type

series float

### example

```lipi
//@lipi=2
indicator("oi Example", overlay=false)
plot(oi, title="Open Interest", color=color.blue)
```

### id

variable:oi

## open (variable)

The opening price of the bar your script is being evaluated on.

It is a float series, so it moves on as the script advances through the chart.

### type

series float

### example

```lipi
//@lipi=2
indicator("Open Price Example", overlay=true)
openPrice = open
prevOpen = open[1]
plot(openPrice, color=color.blue, title="Current Open Price")
plot(prevOpen, color=color.red, title="Previous Open Price")
```

### id

variable:open

## or (keyword)

True when either of its operands is true.

Like `and`, it has a symbol spelling that lexes to the same token.

### syntax

```
expr0 || expr1 | expr0 or expr1
```

### example

```lipi
//@lipi=2
indicator("or Example", overlay=true)
// Either condition is enough: a new 20-bar high or a new 20-bar low
extreme = high == talib.highest(high, 20) or low == talib.lowest(low, 20)
bgcolor(extreme ? color.new(color.orange, 0.2) : na)
```

### id

keyword:or

## plot (type)

The value `plot` gives back once it has drawn a series.

Its use is to be passed on: hold it in a variable and hand two of them to `fill` to shade the band between the two plots. It exposes no fields of its own.

### example

```lipi
//@lipi=2
indicator("Multi Plot Example", overlay=false)
// Generate a sample sine wave
length = 50
sineWave = math.sin(bar_index * 2 * 3.1415 / length) * 50
// Plot the sine wave as a solid line
plot(sineWave, title="Sine Wave", color=color.blue, linewidth=2, style=plotStyle.line)
// Plot the absolute sine wave as a histogram
plot(math.abs(sineWave), title="Absolute Sine Wave", color=color.green, style=plotStyle.histogram)
// Plot a cross marker at every bar based on sine wave peaks
plot(sineWave > 40 ? sineWave : na, title="Peaks", color=color.orange, style=plotStyle.cross)
// Plot circles at troughs of the sine wave
plot(sineWave < -40 ? sineWave : na, title="Troughs", color=color.purple, style=plotStyle.scatter)
```

### id

type:plot

## plot (function)

Draws a series on the chart, one point per bar. It is the output function you will reach for first.

Eleven parameters, of which only the first is required — every other one carries a default. The call has to sit at the top level of the script: put it inside a branch, a loop or a function of your own and the script is rejected for not being in the global scope. A condition therefore belongs in the `color` argument, not around the call.

### syntax

```
plot(series float series, const string title, series color color, input int linewidth, input plotStyle style, input bool trackprice, input float histbase, input int offset, const bool force_overlay, input display display, input string format) → series plot
```

### args

- `series`: series float
  Series of data to be plotted. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `title?`: const string
  Title of the plot.
  types: const string, literal string
  default: na
- `color?`: series color
  Color of the plot. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `linewidth?`: input int
  Width of the plotted line. Default value is 1. Not applicable to every style.
  types: input int, const int, literal int
  default: 1
- `style?`: input plotStyle
  Type of plot. Possible values are: plotStyle.line, plotStyle.linebr, plotStyle.area, plotStyle.areabr, plotStyle.smoothedArea, plotStyle.stepLine, plotStyle.stepLinebr, plotStyle.stepArea, plotStyle.stepAreabr, plotStyle.bar, plotStyle.histogram, plotStyle.scatter, plotStyle.triangular, plotStyle.cross. Default value is plotStyle.line.
  types: input plotStyle, const plotStyle, literal plotStyle
  values: plotStyle.line, plotStyle.linebr, plotStyle.area, plotStyle.areabr, plotStyle.smoothedArea, plotStyle.stepLine, plotStyle.stepLinebr, plotStyle.stepArea, plotStyle.stepAreabr, plotStyle.bar, plotStyle.histogram, plotStyle.scatter, plotStyle.triangular, plotStyle.cross
  default: plotStyle.line
- `trackprice?`: input bool
  Accepted, but the current compiler does not use it, so it has no effect: no price line is drawn. Default is false.
  types: input bool, input int, const int, literal int, input float, const float, literal float, const bool, literal bool
  default: false
- `histbase?`: input float
  The price value used as the reference level when rendering the plot with the plotStyle.histogram or plotStyle.area style. Default is 0.0.
  types: input float, input int, const int, literal int, const float, literal float
  default: 0.0
- `offset?`: input int
  Shifts the plot to the left or to the right on the given number of bars. Default is 0.
  types: input int, const int, literal int
  default: 0
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Controls where the plot is shown (pane, price scale, status line, data window). Use display.* constants; combine with +. Default is display.all.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all
- `format?`: input string
  Format of the displayed values: `format.price`, `format.percent` or `format.volume`. The default is an empty string, which uses the script's format. `format.inherit` and `format.mintick` pass the editor's check but are refused when the script is added to the chart.
  types: input string, const string, literal string
  values: format.percent, format.price, format.volume
  default: ""

### returnedType

series plot

### example

```lipi
//@lipi=2
indicator("Conditional Plot", overlay=true)
signal = close > talib.sma(close, 14) ? close : na
plot(signal, color=color.green, title="Above SMA Signal", style=plotStyle.scatter)
```

### id

function:plot

## plotStyle (type)

The fourteen ways `plot` can draw a series: `line`, `linebr`, `area`, `areabr`, `smoothedArea`, `stepLine`, `stepLinebr`, `stepArea`, `stepAreabr`, `bar`, `histogram`, `scatter`, `triangular` and `cross`.

Name a member with the set in front of it, as in `plotStyle.histogram`. The `br` endings are separate members, distinct from the plain forms.

### fields

- `line`
  A named constant for the 'Line' style, to be used as an argument for the style parameter in the plot function.
- `linebr`
  A named constant for the 'Line With Breaks' style, to be used as an argument for the style parameter in the plot function. Similar to `plotStyle.line`, except the gaps in the data are not filled.
- `area`
  A named constant for the 'Area' style, to be used as an argument for the style parameter in the plot function.
- `areabr`
  A named constant for the 'Area With Breaks' style, to be used as an argument for the style parameter in the plot function. Similar to `plotStyle.area`, except the gaps in the data are not filled.
- `smoothedArea`
  A name constant used to  used to create a smoothly filled area between the plotted values and the x-axis (zero level or another base value). It provides a gradient-like appearance instead of a sharp, rigid fill.
- `stepLine`
  A named constant for the 'Step Line' style, to be used as an argument for the style parameter in the plot function.
- `stepLinebr`
  A named constant for the 'Step line with Breaks' style, to be used as an argument for the style parameter in the plot function.
- `stepArea`
  A name constant used to create a stepped area chart, where the filled area follows a step-like pattern instead of a smooth curve.
- `stepAreabr`
  A name constant used to create a stepped background area fill. This style is similar to plotStyle.stepArea, but instead of filling the area with a standard overlay, it applies a background-style fill that integrates smoothly with the chart.
- `bar`
  Vertical column bars
- `histogram`
  A named constant for the 'Histogram' style, to be used as an argument for the style parameter in the plot function.
- `scatter`
  A named constant used to plot individual data points as scattered dots on the chart, instead of a continuous line
- `triangular`
  A named constant used to plot a triangular wave-like pattern instead of a standard line.
- `cross`
  A named constant for the 'Cross' style, to be used as an argument for the style parameter in the plot function.

### example

```lipi
//@lipi=2
indicator("plotStyle Example", overlay=false)
plot(close - open, title="Body", color=color.blue, style=plotStyle.histogram)
plot(talib.sma(close - open, 10), title="Average Body", color=color.orange, style=plotStyle.line)
```

### id

type:plotStyle

## plotStyle (enum)

The fourteen ways `plot` can draw a series: `line`, `linebr`, `area`, `areabr`, `smoothedArea`, `stepLine`, `stepLinebr`, `stepArea`, `stepAreabr`, `bar`, `histogram`, `scatter`, `triangular` and `cross`.

Name a member with the set in front of it, as in `plotStyle.histogram`. The `br` endings are separate members, distinct from the plain forms.

### fields

- `line`
  A named constant for the 'Line' style, to be used as an argument for the style parameter in the plot function.
- `linebr`
  A named constant for the 'Line With Breaks' style, to be used as an argument for the style parameter in the plot function. Similar to `plotStyle.line`, except the gaps in the data are not filled.
- `area`
  A named constant for the 'Area' style, to be used as an argument for the style parameter in the plot function.
- `areabr`
  A named constant for the 'Area With Breaks' style, to be used as an argument for the style parameter in the plot function. Similar to `plotStyle.area`, except the gaps in the data are not filled.
- `smoothedArea`
  A name constant used to  used to create a smoothly filled area between the plotted values and the x-axis (zero level or another base value). It provides a gradient-like appearance instead of a sharp, rigid fill.
- `stepLine`
  A named constant for the 'Step Line' style, to be used as an argument for the style parameter in the plot function.
- `stepLinebr`
  A named constant for the 'Step line with Breaks' style, to be used as an argument for the style parameter in the plot function.
- `stepArea`
  A name constant used to create a stepped area chart, where the filled area follows a step-like pattern instead of a smooth curve.
- `stepAreabr`
  A name constant used to create a stepped background area fill. This style is similar to plotStyle.stepArea, but instead of filling the area with a standard overlay, it applies a background-style fill that integrates smoothly with the chart.
- `bar`
  Vertical column bars
- `histogram`
  A named constant for the 'Histogram' style, to be used as an argument for the style parameter in the plot function.
- `scatter`
  A named constant used to plot individual data points as scattered dots on the chart, instead of a continuous line
- `triangular`
  A named constant used to plot a triangular wave-like pattern instead of a standard line.
- `cross`
  A named constant for the 'Cross' style, to be used as an argument for the style parameter in the plot function.

### example

```lipi
//@lipi=2
indicator("plotStyle Example", overlay=false)
plot(close - open, title="Body", color=color.blue, style=plotStyle.histogram)
plot(talib.sma(close - open, 10), title="Average Body", color=color.orange, style=plotStyle.line)
```

### id

enum:plotStyle

## plotarrow (function)

Draws an arrow on each bar, sized from a number you supply.

It is the odd one out among the markers: `plotshape` and `plotchar` take a condition, this takes a value. It also has no location, no shape, no size and no text — where an arrow sits follows from the number.

### syntax

```
plotarrow(series float series, const string title, series color colorup, series color colordown, input int offset, input int minheight, input int maxheight, const bool force_overlay, input display display, input string format) → void
```

### args

- `series`: series float
  Series of data to be plotted as arrows. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `title?`: const string
  Title of the plot.
  types: const string, literal string
  default: na
- `colorup?`: series color
  Color of the up arrows. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `colordown?`: series color
  Color of the down arrows. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `offset?`: input int
  Shifts arrows to the left or to the right on the given number of bars. Default is 0.
  types: input int, const int, literal int
  default: 0
- `minheight?`: input int
  Minimal possible arrow height in pixels. Default is 10.
  types: input int, const int, literal int
  default: 10
- `maxheight?`: input int
  Maximum possible arrow height in pixels. Default is 100.
  types: input int, const int, literal int
  default: 100
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Controls where the plot is shown (pane, price scale, status line, data window). Use display.* constants; combine with +. Default is display.all.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all
- `format?`: input string
  Format of the displayed values: `format.price`, `format.percent` or `format.volume`. The default is an empty string, which uses the script's format. `format.inherit` and `format.mintick` pass the editor's check but are refused when the script is added to the chart.
  types: input string, const string, literal string
  values: format.percent, format.price, format.volume
  default: ""

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Plot Arrow Example", overlay=true)
longCondition = talib.crossover(talib.sma(close, 10), talib.sma(close, 20))
shortCondition = talib.crossunder(talib.sma(close, 10), talib.sma(close, 20))
plotarrow(longCondition ? 1 : shortCondition ? -1 : na, title="Arrow Signals", colorup=color.lime, colordown=color.red,offset=-1)
```

### id

function:plotarrow

## plotbar (function)

Draws bars from the same four required series that `plotcandle` takes.

The difference is the colouring: one colour for the whole bar, with no separate wick or border. Neither function has an offset parameter at all.

### syntax

```
plotbar(series float open, series float high, series float low, series float close, const string title, series color color, input display display, const bool force_overlay) → void
```

### args

- `open`: series float
  Open series of data to be used as open values of bars. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `high`: series float
  High series of data to be used as high values of bars. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `low`: series float
  Low series of data to be used as low values of bars. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `close`: series float
  Close series of data to be used as close values of bars. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `title?`: const string
  Title of the plotbar. Optional argument.
  types: const string, literal string
  default: na
- `color?`: series color
  Color of the ohlc bars. You can use constants like 'color=color.blue' or 'color=#0000FF' as well as complex expressions like 'color = close >= open ? color.yellow : color.black'. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `display?`: input display
  Where the bars are shown: `display.pane`, `display.price_scale`, `display.status_line`, `display.data_window`, `display.all` (the default) or `display.none`. Combine constants with `+`, for example `display.pane + display.status_line`.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Custom Bars Example", overlay=true)
customOpen = open + talib.sma(close, 5) * 0.001
customHigh = high + talib.sma(close, 5) * 0.001
customLow = low - talib.sma(close, 5) * 0.001
customClose = close + talib.sma(close, 5) * 0.001
plotbar(customOpen, customHigh, customLow, customClose, title="Custom Bars")
```

### id

function:plotbar

## plotcandle (function)

Draws candles from four series of your own rather than from the chart's bars.

All four price series are required. The body, the wick and the border take separate colours, and each of the three is series-form.

### syntax

```
plotcandle(series float open, series float high, series float low, series float close, const string title, series color color, series color wickcolor, series color bordercolor, const bool force_overlay, input display display) → void
```

### args

- `open`: series float
  Open series of data to be used as open values of candles. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `high`: series float
  High series of data to be used as high values of candles. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `low`: series float
  Low series of data to be used as low values of candles. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `close`: series float
  Close series of data to be used as close values of candles. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `title?`: const string
  Title of the plotcandles. Optional argument
  types: const string, literal string
  default: na
- `color?`: series color
  Color of the candles. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `wickcolor?`: series color
  The color of the wick of candles. An optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `bordercolor?`: series color
  The border color of candles. An optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Where the candles are shown: `display.pane`, `display.price_scale`, `display.status_line`, `display.data_window`, `display.all` (the default) or `display.none`. Combine constants with `+`, for example `display.pane + display.status_line`.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all

### returnedType

void

### example

```lipi
//@lipi=2
indicator("Plot Candle Example", overlay=true)
openSeries = open
highSeries = high + talib.sma(close, 5) * 0.001
lowSeries = low - talib.sma(close, 5) * 0.001
closeSeries = close + talib.sma(close, 5) * 0.001
upColor = color.new(color.green, 0)
downColor = color.new(color.red, 0)
wickColor = color.new(color.gray, 0)
plotcandle(openSeries, highSeries, lowSeries, closeSeries, title="Custom Candles", color=closeSeries >= openSeries ? upColor : downColor, wickcolor=wickColor)
```

### id

function:plotcandle

## plotchar (function)

The same marker as `plotshape`, with one character in place of a shape from the fixed set.

It draws exactly one character. Pass a longer string and it is cut to the first character, with no warning and no error, so pass the character you want.

`series` is a float price, and the marker is declared to the chart as absolute-position whatever `location` is passed. With a `location` other than `location.absolute` the call is still accepted and the value is read as a condition (non-zero is true); how the chart places such a marker is not established.

### syntax

```
plotchar(series float series, const string title, const string char, input location location, series color color, input int offset, const string text, series color textcolor, input size size, const bool force_overlay, input display display, input string format) → void
```

### args

- `series`: series float
  The price at which to place the marker: a float series. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `title?`: const string
  Title of the plot.
  types: const string, literal string
  default: na
- `char?`: const string
  Character to use as a visual shape.
  types: const string, literal string
  default: na
- `location?`: input location
  Location of shapes on the chart. Possible values are: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute. Default value is location.absolute.
  types: input location, const location, literal location
  values: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute
  default: location.absolute
- `color?`: series color
  Color of the characters. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `offset?`: input int
  Shifts shapes to the left or to the right on the given number of bars. Default is 0.
  types: input int, const int, literal int
  default: 0
- `text?`: const string
  Text to display with the shape. The compiler keeps a `\n` written in the string as the two characters backslash and `n` and does not turn it into a line break; whether the chart draws a line break for it is not established.
  types: const string, literal string
  default: na
- `textcolor?`: series color
  Color of the character text. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `size?`: input size
  Size of characters on the chart. Possible values are: size.auto, size.tiny, size.small, size.normal, size.large, size.huge. Default is size.auto.
  types: input size, const size, literal size
  values: size.auto, size.tiny, size.small, size.normal, size.large, size.huge
  default: size.auto
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Controls where the plot is shown (pane, price scale, status line, data window). Use display.* constants; combine with +. Default is display.all.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all
- `format?`: input string
  Format of the plotted value: `format.price`, `format.percent` or `format.volume`. The default is an empty string, which uses the script's format. Any other value passes the editor's check but is refused when the script is added to the chart.
  types: input string, const string, literal string
  values: format.percent, format.price, format.volume
  default: ""

### returnedType

void

### notes

- The `size` argument takes a `size.*` constant. A string such as "small" still compiles here, with a deprecation warning: write the constant. A string that is not a size name, such as "giant", stops the compiler with the error "internal validator error".

### example

```lipi
//@lipi=2
indicator("PlotChar Example", overlay=true)
conditionUp = close > close[1]
conditionDown = close < close[1]
plotchar(conditionUp, char='▲', location=location.abovebar, size=size.small, color=color.green)
plotchar(conditionDown, char='▼', location=location.belowbar, size=size.small, color=color.red)
```

### id

function:plotchar~1

## plotchar (function)

The same marker as `plotshape`, with one character in place of a shape from the fixed set.

It draws exactly one character. Pass a longer string and it is cut to the first character, with no warning and no error, so pass the character you want.

`series` is a boolean condition. With `location.absolute` the call is also accepted: the value handed to the chart is 1 where the condition is true and 0 where it is false, so the marker is placed at the price 1 or 0, which is rarely wanted; use a float series for an absolute position.

### syntax

```
plotchar(series bool series, const string title, const string char, input location location, series color color, input int offset, const string text, series color textcolor, input size size, const bool force_overlay, input display display, input string format) → void
```

### args

- `series`: series bool
  The condition to mark: a bool series. Required argument.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
- `title?`: const string
  Title of the plot.
  types: const string, literal string
  default: na
- `char?`: const string
  Character to use as a visual shape.
  types: const string, literal string
  default: na
- `location?`: input location
  Location of shapes on the chart. Possible values are: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute. Default value is location.abovebar.
  types: input location, const location, literal location
  values: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute
  default: location.abovebar
- `color?`: series color
  Color of the characters. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `offset?`: input int
  Shifts shapes to the left or to the right on the given number of bars. Default is 0.
  types: input int, const int, literal int
  default: 0
- `text?`: const string
  Text to display with the shape. The compiler keeps a `\n` written in the string as the two characters backslash and `n` and does not turn it into a line break; whether the chart draws a line break for it is not established.
  types: const string, literal string
  default: na
- `textcolor?`: series color
  Color of the character text. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `size?`: input size
  Size of characters on the chart. Possible values are: size.auto, size.tiny, size.small, size.normal, size.large, size.huge. Default is size.auto.
  types: input size, const size, literal size
  values: size.auto, size.tiny, size.small, size.normal, size.large, size.huge
  default: size.auto
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Controls where the plot is shown (pane, price scale, status line, data window). Use display.* constants; combine with +. Default is display.all.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all
- `format?`: input string
  Format of the plotted value: `format.price`, `format.percent` or `format.volume`. The default is an empty string, which uses the script's format. Any other value passes the editor's check but is refused when the script is added to the chart.
  types: input string, const string, literal string
  values: format.percent, format.price, format.volume
  default: ""

### returnedType

void

### notes

- The `size` argument takes a `size.*` constant. A string such as "small" still compiles here, with a deprecation warning: write the constant.

### example

```lipi
//@lipi=2
indicator("PlotChar Example", overlay=true)
conditionUp = close > close[1]
conditionDown = close < close[1]
plotchar(conditionUp, char='▲', location=location.abovebar, size=size.small, color=color.green)
plotchar(conditionDown, char='▼', location=location.belowbar, size=size.small, color=color.red)
```

### id

function:plotchar~2

## plotshape (function)

Marks the bars on which a condition holds, using a shape from a fixed set.

The condition is the first argument, which is how you mark some bars and not others without moving the call: like every chart-output function it must be called at the top level.

`series` is a boolean condition. With `location.absolute` the call is also accepted: the value handed to the chart is 1 where the condition is true and 0 where it is false, so the marker is placed at the price 1 or 0, which is rarely wanted; use a float series for an absolute position.

### syntax

```
plotshape(series bool series, const string title, input shape shape, input location location, series color color, input int offset, const string text, series color textcolor, input size size, const bool force_overlay, input display display, input string format) → void
```

### args

- `series`: series bool
  The condition to mark: a bool series. Required argument.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
- `title?`: const string
  Title of the plot.
  types: const string, literal string
  default: na
- `shape?`: input shape
  Type of plot. Possible values are: shape.xcross, shape.cross, shape.triangleup, shape.triangledown, shape.flag, shape.circle, shape.arrowup, shape.arrowdown, shape.labelup, shape.labeldown, shape.square, shape.diamond. Default value is shape.xcross.
  types: input shape, const shape, literal shape
  values: shape.xcross, shape.cross, shape.triangleup, shape.triangledown, shape.flag, shape.circle, shape.arrowup, shape.arrowdown, shape.labelup, shape.labeldown, shape.square, shape.diamond
  default: shape.xcross
- `location?`: input location
   Location of shapes on the chart. Possible values are: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute. Default value is location.abovebar.
  types: input location, const location, literal location
  values: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute
  default: location.abovebar
- `color?`: series color
  Color of the shapes. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `offset?`: input int
  Shifts shapes to the left or to the right on the given number of bars. Default is 0.
  types: input int, const int, literal int
  default: 0
- `text?`: const string
  Text to display with the shape. The compiler keeps a `\n` written in the string as the two characters backslash and `n` and does not turn it into a line break; whether the chart draws a line break for it is not established.
  types: const string, literal string
  default: na
- `textcolor?`: series color
  Color of the shape label text. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `size?`: input size
  Size of shapes on the chart. Possible values are: size.auto, size.tiny, size.small, size.normal, size.large, size.huge. Default is size.auto.
  types: input size, const size, literal size
  values: size.auto, size.tiny, size.small, size.normal, size.large, size.huge
  default: size.auto
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Controls where the plot is shown (pane, price scale, status line, data window). Use display.* constants; combine with +. Default is display.all.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all
- `format?`: input string
  Format of the plotted value: `format.price`, `format.percent` or `format.volume`. The default is an empty string, which uses the script's format. Any other value passes the editor's check but is refused when the script is added to the chart.
  types: input string, const string, literal string
  values: format.percent, format.price, format.volume
  default: ""

### returnedType

void

### notes

- The `size` argument takes a `size.*` constant. A string such as "small" still compiles here, with a deprecation warning: write the constant.

### example

```lipi
//@lipi=2
indicator("PlotShape Example", overlay=true)
buySignal = talib.crossover(talib.sma(close, 10), talib.sma(close, 20))
sellSignal = talib.crossunder(talib.sma(close, 10), talib.sma(close, 20)) 
plotshape(series=buySignal, location=location.belowbar, shape=shape.triangleup, color=color.green, size=size.small, title="Buy Signal")
plotshape(series=sellSignal, location=location.abovebar, shape=shape.triangledown, color=color.red, size=size.small, title="Sell Signal")
```

### id

function:plotshape~1

## plotshape (function)

Marks the bars on which a condition holds, using a shape from a fixed set.

The condition is the first argument, which is how you mark some bars and not others without moving the call: like every chart-output function it must be called at the top level.

`series` is a float price, and the marker is declared to the chart as absolute-position whatever `location` is passed. With a `location` other than `location.absolute` the call is still accepted and the value is read as a condition (non-zero is true); how the chart places such a marker is not established.

### syntax

```
plotshape(series float series, const string title, input shape shape, input location location, series color color, input int offset, const string text, series color textcolor, input size size, const bool force_overlay, input display display, input string format) → void
```

### args

- `series`: series float
  The price at which to place the marker: a float series. Required argument.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `title?`: const string
  Title of the plot.
  types: const string, literal string
  default: na
- `shape?`: input shape
  Type of plot. Possible values are: shape.xcross, shape.cross, shape.triangleup, shape.triangledown, shape.flag, shape.circle, shape.arrowup, shape.arrowdown, shape.labelup, shape.labeldown, shape.square, shape.diamond. Default value is shape.xcross.
  types: input shape, const shape, literal shape
  values: shape.xcross, shape.cross, shape.triangleup, shape.triangledown, shape.flag, shape.circle, shape.arrowup, shape.arrowdown, shape.labelup, shape.labeldown, shape.square, shape.diamond
  default: shape.xcross
- `location?`: input location
   Location of shapes on the chart. Possible values are: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute. Default value is location.absolute.
  types: input location, const location, literal location
  values: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute
  default: location.absolute
- `color?`: series color
  Color of the shapes. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `offset?`: input int
  Shifts shapes to the left or to the right on the given number of bars. Default is 0.
  types: input int, const int, literal int
  default: 0
- `text?`: const string
  Text to display with the shape. The compiler keeps a `\n` written in the string as the two characters backslash and `n` and does not turn it into a line break; whether the chart draws a line break for it is not established.
  types: const string, literal string
  default: na
- `textcolor?`: series color
  Color of the shape label text. Optional argument.
  types: series color, simple color, input color, const color, literal color
  default: na
- `size?`: input size
  Size of shapes on the chart. Possible values are: size.auto, size.tiny, size.small, size.normal, size.large, size.huge. Default is size.auto.
  types: input size, const size, literal size
  values: size.auto, size.tiny, size.small, size.normal, size.large, size.huge
  default: size.auto
- `force_overlay?`: const bool
  If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `display?`: input display
  Controls where the plot is shown (pane, price scale, status line, data window). Use display.* constants; combine with +. Default is display.all.
  types: input display, const display, literal display
  values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all
  default: display.all
- `format?`: input string
  Format of the plotted value: `format.price`, `format.percent` or `format.volume`. The default is an empty string, which uses the script's format. Any other value passes the editor's check but is refused when the script is added to the chart.
  types: input string, const string, literal string
  values: format.percent, format.price, format.volume
  default: ""

### returnedType

void

### notes

- The `size` argument takes a `size.*` constant. A string such as "small" still compiles here, with a deprecation warning: write the constant.

### example

```lipi
//@lipi=2
indicator("PlotShape Example", overlay=true)
buySignal = talib.crossover(talib.sma(close, 10), talib.sma(close, 20))
sellSignal = talib.crossunder(talib.sma(close, 10), talib.sma(close, 20)) 
plotshape(series=buySignal, location=location.belowbar, shape=shape.triangleup, color=color.green, size=size.small, title="Buy Signal")
plotshape(series=sellSignal, location=location.abovebar, shape=shape.triangledown, color=color.red, size=size.small, title="Sell Signal")
```

### id

function:plotshape~2

## polyline (function)

Converts `value` to the `polyline` type. It is used almost only as `polyline(na)`, to declare a polyline variable that has no drawing yet, so that its type is known before the first drawing is assigned.

### syntax

```
polyline(series polyline value) → series polyline
```

### args

- `value`: series polyline
  The value to convert to the specified type, usually na.
  types: series polyline, simple polyline, input polyline, const polyline, literal polyline

### returnedType

series polyline

### example

```lipi
//@lipi=2
indicator("polyline() Example", overlay=true)
static polyline path = polyline(na)
if barstate.islast {
    pts = array.new<chartPoint>(0)
    array.push(pts, chartPoint.from_index(bar_index[10], close[10]))
    array.push(pts, chartPoint.from_index(bar_index, close))
    path := polyline.new(pts, line_color=color.orange)
}
```

### id

function:polyline

## return (keyword)

Hands a value back from a braced function body. It takes an expression, which may be left out: a bare `return` ends a function that returns no value, and the result of such a function cannot be assigned ("Cannot assign void value.").

A tuple is written as a bracketed list, so a function can return several values at once. The arrow body form needs no `return` — the expression after the arrow is the result.

### syntax

```
return [<expression>]
```

### example

```lipi
//@lipi=2
indicator("Return Example", overlay=true)
func getSquare(float x) {
    // Returns the square of x
    return x * x
}
plot(getSquare(close), title="Squared Close Price", color=color.blue)
```

### id

keyword:return

## scale (type)

Price-scale placement for scripts declared with `indicator()` or `strategy()`.

Use the `scale` argument on those declarations. Default is `scale.none`.

### fields

- `left`
  Attach the script to the left price scale.
- `right`
  Attach the script to the right price scale.
- `none`
  Use the default scale for the script (separate pane when `overlay` is false).

### example

```lipi
//@lipi=2
indicator("scale Example", overlay=true, scale=scale.right)
plot(close)
```

### id

type:scale

## scale (enum)

Price-scale placement for scripts declared with `indicator()` or `strategy()`.

Use the `scale` argument on those declarations. Default is `scale.none`.

### fields

- `left`
  Attach the script to the left price scale.
- `right`
  Attach the script to the right price scale.
- `none`
  Use the default scale for the script (separate pane when `overlay` is false).

### example

```lipi
//@lipi=2
indicator("scale Example", overlay=true, scale=scale.right)
plot(close)
```

### id

enum:scale

## second (variable)

The second of the bar being evaluated.

Seven date parts are available as variables. `weekofyear` is not among them: it exists as a function only.

### type

series int

### example

```lipi
//@lipi=2
indicator("Second-Based Signal", overlay=true)
isHalfMinute = (second >= 30)
plotshape(isHalfMinute, location=location.abovebar, color=color.purple, title="Half-Minute Signal")
```

### id

variable:second

## second (function)

The second of a time you supply.

### syntax

```
second(series int time, series string timezone) → series int
```

### args

- `time`: series int
  UNIX time, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `timezone?`: series string
  The time zone the value is read in: an IANA time zone database name (for example "America/New_York") or "UTC". Unlike `timestamp`, `time` and `str.format_time`, this function does not accept offset notation such as "UTC-5" or "GMT+0530": a name that cannot be loaded gives 0, not `na`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Second Function Example", overlay=true)
// Get current bar second
currentSecond = second(time)
// Plot second in Data Window
plot(currentSecond, title="Current Second")
```

### id

function:second

## series (keyword)

A qualifier written before the type of a parameter of your own function. A `series` parameter takes a value that may change from bar to bar, and any value of the other qualifiers.

A parameter written with no qualifier is `series`: `func passthru(float k) => k` returns a `series float`, which a `plot(linewidth=...)` argument refuses. The word is not allowed before a variable declaration.

### syntax

```
func <name>(series <data_type> <parameter_name>) => <expression>
```

### example

```lipi
//@lipi=2
indicator("series Example")
func change2(series float x, series int n) => x - x[n]
plot(change2(close, bar_index % 3 + 1))
```

### id

keyword:series

## shape (type)

The twelve markers `plotshape` can draw: `xcross`, `cross`, `triangleup`, `triangledown`, `flag`, `circle`, `arrowup`, `arrowdown`, `labelup`, `labeldown`, `square` and `diamond`.

Written `shape.triangleup` and so on.

### fields

- `xcross`
  Shape style for plotshape function.
- `cross`
  Shape style for plotshape function.
- `triangleup`
  Shape style for plotshape function.
- `triangledown`
  Shape style for plotshape function.
- `flag`
  Shape style for plotshape function.
- `circle`
  Shape style for plotshape function.
- `arrowup`
  Shape style for plotshape function.
- `arrowdown`
  Shape style for plotshape function.
- `labelup`
  Shape style for plotshape function.
- `labeldown`
  Shape style for plotshape function.
- `square`
  Shape style for plotshape function.
- `diamond`
  Shape style for plotshape function.

### example

```lipi
//@lipi=2
indicator("Shape Example", overlay=true)
// Define bullish and bearish engulfing conditions
bullishEngulfing = close > open and close[1] < open[1] and close > close[1] and open < open[1]
bearishEngulfing = close < open and close[1] > open[1] and close < close[1] and open > open[1]
// Plot a triangle up for bullish engulfing
plotshape(series=bullishEngulfing, location=location.belowbar, shape=shape.triangleup, color=color.green, title="Bullish Engulfing")
// Plot a triangle down for bearish engulfing
plotshape(series=bearishEngulfing, location=location.abovebar, shape=shape.triangledown, color=color.red, title="Bearish Engulfing")
// Plot a cross at every bar where the close is equal to the open (Doji)
doji = close == open
plotshape(series=doji, location=location.abovebar, shape=shape.cross, color=color.blue, title="Doji")
```

### id

type:shape

## shape (enum)

The twelve markers `plotshape` can draw: `xcross`, `cross`, `triangleup`, `triangledown`, `flag`, `circle`, `arrowup`, `arrowdown`, `labelup`, `labeldown`, `square` and `diamond`.

Written `shape.triangleup` and so on.

### fields

- `xcross`
  Shape style for plotshape function.
- `cross`
  Shape style for plotshape function.
- `triangleup`
  Shape style for plotshape function.
- `triangledown`
  Shape style for plotshape function.
- `flag`
  Shape style for plotshape function.
- `circle`
  Shape style for plotshape function.
- `arrowup`
  Shape style for plotshape function.
- `arrowdown`
  Shape style for plotshape function.
- `labelup`
  Shape style for plotshape function.
- `labeldown`
  Shape style for plotshape function.
- `square`
  Shape style for plotshape function.
- `diamond`
  Shape style for plotshape function.

### example

```lipi
//@lipi=2
indicator("Shape Example", overlay=true)
// Define bullish and bearish engulfing conditions
bullishEngulfing = close > open and close[1] < open[1] and close > close[1] and open < open[1]
bearishEngulfing = close < open and close[1] > open[1] and close < close[1] and open > open[1]
// Plot a triangle up for bullish engulfing
plotshape(series=bullishEngulfing, location=location.belowbar, shape=shape.triangleup, color=color.green, title="Bullish Engulfing")
// Plot a triangle down for bearish engulfing
plotshape(series=bearishEngulfing, location=location.abovebar, shape=shape.triangledown, color=color.red, title="Bearish Engulfing")
// Plot a cross at every bar where the close is equal to the open (Doji)
doji = close == open
plotshape(series=doji, location=location.abovebar, shape=shape.cross, color=color.blue, title="Doji")
```

### id

enum:shape

## simple (keyword)

A qualifier written before the type of a parameter of your own function. A `simple` parameter takes a value that is known on the first bar and stays fixed, such as `syminfo.mintick`, and any `const` or `input` value.

A value that changes from bar to bar, such as `close`, is refused with "Cannot call `<function>` with argument `<name>`=`<value>`. An argument of `series float` type was used but a `simple float` is expected." The word is not allowed before a variable declaration.

### syntax

```
func <name>(simple <data_type> <parameter_name>) => <expression>
```

### example

```lipi
//@lipi=2
indicator("simple Example")
func ticks(series float x, simple float tickSize) => x / tickSize
plot(ticks(close, syminfo.mintick))
```

### id

keyword:simple

## size (type)

Six sizes for a marker: `auto`, `tiny`, `small`, `normal`, `large` and `huge`.

Used by the `size` parameter of `plotshape` and `plotchar`. `auto` is a member like the rest, not the absence of a choice.

### fields

- `auto`
  Allows automatic size adjustment based on the chart's zoom level and resolution.
- `tiny`
  Smallest size
- `small`
  Small size
- `normal`
  Default (medium) size
- `large`
  Large size
- `huge`
  Largest size

### example

```lipi
//@lipi=2
indicator("size Example", overlay=true)
plotshape(talib.crossover(close, talib.sma(close, 20)), title="Cross Up", location=location.belowbar, shape=shape.triangleup, color=color.green, size=size.small)
plotshape(talib.crossunder(close, talib.sma(close, 20)), title="Cross Down", location=location.abovebar, shape=shape.triangledown, color=color.red, size=size.large)
```

### id

type:size

## size (enum)

Six sizes for a marker: `auto`, `tiny`, `small`, `normal`, `large` and `huge`.

Used by the `size` parameter of `plotshape` and `plotchar`. `auto` is a member like the rest, not the absence of a choice.

### fields

- `auto`
  Allows automatic size adjustment based on the chart's zoom level and resolution.
- `tiny`
  Smallest size
- `small`
  Small size
- `normal`
  Default (medium) size
- `large`
  Large size
- `huge`
  Largest size

### example

```lipi
//@lipi=2
indicator("size Example", overlay=true)
plotshape(talib.crossover(close, talib.sma(close, 20)), title="Cross Up", location=location.belowbar, shape=shape.triangleup, color=color.green, size=size.small)
plotshape(talib.crossunder(close, talib.sma(close, 20)), title="Cross Down", location=location.abovebar, shape=shape.triangledown, color=color.red, size=size.large)
```

### id

enum:size

## static (keyword)

Declares a value that survives from one bar to the next. Without it, a declaration is made again on every bar, because your script is evaluated once per bar.

The initializer runs when execution first reaches the declaration and no value has been stored for it, which is ordinarily the first bar. Reassign a `static` value with `:=` and the new value carries forward, but a change is kept only when the bar is confirmed: while a bar is still forming and the script runs again on each update, every run starts from the value stored when the last bar closed, and what the earlier runs of that bar changed is discarded. Its store is never cleared while the script runs, which is what separates it from `intra`.

### syntax

```
static <data_type> <variable_name> = <expression>
```

### example

```lipi
//@lipi=2
indicator("static Example - First Close", overlay=true)
// Store the first close price only once
static float firstClose = close
// Plot the first close price as a horizontal line
plot(firstClose, "First Close", color=color.blue)
```

### id

keyword:static

## step (keyword)

The optional increment of a counted `for` loop: `for i = 0 to 10 step 2`.

`step` is a reserved word. It cannot be used as the name of a variable.

### syntax

```
for <identifier> = <expression> to <expression> step <expression> {
	...
}
```

### example

```lipi
//@lipi=2
indicator("step Example")
float s = 0
for i = 0 to 10 step 2 {
    s += i
}
plot(s)
```

### id

keyword:step

## strategy (function)

Declares the script as a strategy: a script that places simulated orders and reports their performance. It is used in place of `indicator`, as the first statement of the script.

Besides the display settings it shares with `indicator`, it sets how orders are sized and filled: `initial_capital`, `default_qty_type` and `default_qty_value` for position size, `commission_type` and `commission_value` for costs, `pyramiding` for how many entries in the same direction are allowed, and `process_orders_on_close`, `calc_on_order_fills` and `calc_on_every_tick` for when orders are evaluated.

### syntax

```
strategy(const string title, const string shorttitle, const bool overlay, const string format, const int precision, const scale scale, const int pyramiding, const bool calc_on_order_fills, const bool calc_on_every_tick, const string default_qty_type, const float default_qty_value, const float initial_capital, const string commission_type, const float commission_value, const bool process_orders_on_close, const int max_lines_count, const int max_labels_count, const int max_boxes_count, const int max_polylines_count, const bool behind_chart) → void
```

### args

- `title`: const string
  Strategy name shown in the UI and used as the default publication title.
  types: const string, literal string
- `shorttitle?`: const string
  Short name shown on the chart when set; otherwise `title` is used.
  types: const string, literal string
- `overlay?`: const bool
  If true, the strategy is drawn over the price chart; otherwise it uses a separate pane. Default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `format?`: const string
  How the script's values are formatted on the price scale and in the status line: `format.inherit` (the default: as the chart's symbol), `format.price`, `format.volume` or `format.percent`. Any other `format.*` constant passes the editor's check but is refused when the script is added to the chart.
  types: const string, literal string
  values: format.inherit, format.percent, format.price, format.volume
  default: format.inherit
- `precision?`: const int
  Number of digits after the decimal point in the script's displayed values. Accepted, but the current compiler does not pass it on, so it has no effect yet.
  types: const int, literal int
  default: 0
- `scale?`: const scale
  Which price scale the strategy uses: `scale.left`, `scale.right`, or `scale.none`. Optional. Default is `scale.none`.
  types: const scale, literal scale
  default: scale.none
- `pyramiding?`: const int
  Maximum number of entries allowed in the same direction (0 disables adding to a position). An entry that would add to a position that already holds that many open entries in its direction is ignored, with no error. With 0 the first entry from a flat position still opens, so 0 and 1 behave alike.
  types: const int, literal int
  default: 1
- `calc_on_order_fills?`: const bool
  If true, the strategy recalculates when an order fills. Optional.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `calc_on_every_tick?`: const bool
  If true, the strategy recalculates on every realtime tick of the last bar. Optional.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `default_qty_type?`: const string
  How `default_qty_value` is read when an order gives no `qty`: `strategy.fixed` (the default: a number of contracts), the string "cash" (an amount of money, divided by the order's price) or the string "percent_of_equity" (a percentage of the current equity, divided by the order's price). "cash" and "percent_of_equity" need a price: an order with a `limit` or `stop` uses that price, but a market `strategy.entry` or `strategy.order`, and a `strategy.exit` without `qty`, stop the script with the error "Invalid order quantity". Only `strategy.fixed` works for market orders. The constants `strategy.cash` and `strategy.percent_of_equity` do not exist: pass the strings.
  types: const string, literal string
  values: strategy.fixed, "cash", "percent_of_equity"
  default: strategy.fixed
- `default_qty_value?`: const float
  Default order size used with `default_qty_type`.
  types: const float, const int, literal int, literal float
  default: 1
- `initial_capital?`: const float
  Starting equity for the simulation.
  types: const float, const int, literal int, literal float
  default: 1000000
- `commission_type?`: const string
  How commission is charged: `strategy.commission_percent` (a percentage of each order's value), `strategy.commission_cash_per_order` (a fixed amount for each trade opened and for each trade closed) or `strategy.commission_cash_per_contract` (an amount per contract traded).
  types: const string, literal string
  values: strategy.commission_cash_per_contract, strategy.commission_cash_per_order, strategy.commission_percent
  default: strategy.commission_percent
- `commission_value?`: const float
  Commission amount according to `commission_type`.
  types: const float, const int, literal int, literal float
  default: 0
- `process_orders_on_close?`: const bool
  If true, orders are processed on bar close instead of on the next bar open.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false
- `max_lines_count?`: const int
  Maximum line drawings allowed. Default is 50.
  types: const int, literal int
  default: 50
- `max_labels_count?`: const int
  Maximum label drawings allowed. Default is 50.
  types: const int, literal int
  default: 50
- `max_boxes_count?`: const int
  Maximum box drawings allowed. Default is 50.
  types: const int, literal int
  default: 50
- `max_polylines_count?`: const int
  Maximum polyline drawings allowed. Default is 50.
  types: const int, literal int
  default: 50
- `behind_chart?`: const bool
  If true, plot drawings render behind the chart candles. Optional. Default is true.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: true

### returnedType

void

### example

```lipi
//@lipi=2
strategy("MA Cross Strategy", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1, commission_type=strategy.commission_percent, commission_value=0.1)
fast = talib.sma(close, 10)
slow = talib.sma(close, 30)
if talib.crossover(fast, slow) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(fast, slow) {
    strategy.close("Long")
}
plot(fast, title="Fast MA", color=color.green)
plot(slow, title="Slow MA", color=color.red)
```

### id

function:strategy

## string (type)

A piece of text, written between double quotes: `"length"`.

Titles, messages and instrument details are strings. The `str` namespace holds the functions that work on them. No fields.

### example

```lipi
//@lipi=2
indicator("string Example", overlay=true)
string trend = close > talib.sma(close, 20) ? "Up" : "Down"
if barstate.islast {
    label.new(bar_index, high, text="Trend: " + trend)
}
```

### id

type:string

## string (function)

Converts a value to a string.

It accepts a string only, so it changes the form and not the data type. To render a number as text, look to the `str` namespace.

### syntax

```
string(const string value) → const string
```

### args

- `value`: const string
  The value to convert to the specified type, usually na.
  types: const string, literal string

### returnedType

const string

### example

```lipi
//@lipi=2
indicator("String Upper Example", overlay=false)
lowerStr = "gocharting"
upperStr = str.upper(lowerStr)
plot(close, title=upperStr)
```

### id

function:string~1

## string (function)

Converts a value to a string.

It accepts a string only, so it changes the form and not the data type. To render a number as text, look to the `str` namespace.

### syntax

```
string(input string value) → input string
```

### args

- `value`: input string
  The value to convert to the specified type, usually na.
  types: input string, const string, literal string

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("String Upper Example", overlay=false)
lowerStr = "gocharting"
upperStr = str.upper(lowerStr)
plot(close, title=upperStr)
```

### id

function:string~2

## string (function)

Converts a value to a string.

It accepts a string only, so it changes the form and not the data type. To render a number as text, look to the `str` namespace.

### syntax

```
string(simple string value) → simple string
```

### args

- `value`: simple string
  The value to convert to the specified type, usually na.
  types: simple string, input string, const string, literal string

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator("String Upper Example", overlay=false)
lowerStr = "gocharting"
upperStr = str.upper(lowerStr)
plot(close, title=upperStr)
```

### id

function:string~3

## string (function)

Converts a value to a string.

It accepts a string only, so it changes the form and not the data type. To render a number as text, look to the `str` namespace.

### syntax

```
string(series string value) → series string
```

### args

- `value`: series string
  The value to convert to the specified type, usually na.
  types: series string, simple string, input string, const string, literal string

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("String Upper Example", overlay=false)
lowerStr = "gocharting"
upperStr = str.upper(lowerStr)
plot(close, title=upperStr)
```

### id

function:string~4

## switch (keyword)

Chooses one block by the value of an expression.

Each `case <value>:` starts a block, and `default:` runs when no case matches.

`switch` is a statement. It does not produce a value, so it cannot be assigned.

Do not use it inside a function body. A `switch` there passes the editor's check but is refused when the script is added to the chart, with the bare message `Not Implemented`; a function that holds a `switch` but is never called compiles. Use `if` and `else if` inside functions. A function whose `switch` returns in every `case` and in `default`, with no `return` after it, fails both checks with "The `f()` function is missing return statement.", and adding a `return` after it only brings back `Not Implemented` on the chart.

### syntax

```
switch <value> {
	case <value>: ...
	default: ...
}
```

### example

```lipi
//@lipi=2
indicator("switch Example")
int k = 2
float x = 0
switch k {
    case 1: x := 10
    case 2: x := 20
    default: x := 0
}
plot(x)
```

### id

keyword:switch

## table (function)

Converts `value` to the `table` type. It is used almost only as `table(na)`, to declare a table variable that has no drawing yet, so that its type is known before the first drawing is assigned.

### syntax

```
table(series table value) → series table
```

### args

- `value`: series table
  The value to convert to the specified type, usually na.
  types: series table, simple table, input table, const table, literal table

### returnedType

series table

### example

```lipi
//@lipi=2
indicator("table() Example", overlay=true)
static table info = table(na)
if barstate.islast {
    info := table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(info, 0, 0, text="Bars: " + str.tostring(bar_index + 1))
}
```

### id

function:table

## time (variable)

The bar's opening time, as an int series.

It counts milliseconds from the Unix epoch. Note the unit: it is milliseconds, not seconds, so anything expecting seconds needs the value divided by a thousand first.

Hand it to one of the date functions - `year`, `month`, `hour` and the rest - together with a timezone to take it apart.

### type

series int

### example

```lipi
//@lipi=2
indicator(title="Time Example", overlay=true)
plot(time, title="Bar Time", color=color.blue)
```

### id

variable:time

## time (function)

Returns the opening time of the current bar in UNIX milliseconds, measured on `interval` rather than on the chart's own bars.

With `session`, it returns `na` when the opening time of the `interval` bar is outside that session. The session is tested against the start of the `interval` bar, not against the opening time of the chart bar: with `interval` "1D" the tested time is the start of the day, so a session that does not contain midnight, such as "0930-1600", gives `na` on every bar of an intraday chart. Interval bars are cut on the clock in that time zone, not aligned to the chart's bars: with `interval` "1h", a chart bar opening at 09:30 is tested as 09:00, so an `interval` equal to the chart's own interval tests the chart bar's own time only when the chart's bars start on those clock boundaries. `timezone` sets the time zone the interval and the session are read in. `bars_back` and `interval_bars_back` look back a number of chart bars or interval bars respectively.

### syntax

```
time(series string interval, series string session, series int bars_back, series int interval_bars_back) → series int
```

### args

- `interval?`: series string
  The interval the time is measured on: a count and a unit, such as "15m", "4h" or "1D", with the units `s`, `m`, `h`, `D`, `W` and `M`. For `D`, `W` and `M` the count must be 1. Any other string compiles and gives `na`.
  types: series string, simple string, input string, const string, literal string
  default: interval.interval
- `session?`: series string
  A session. Bars outside it return `na`.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `bars_back?`: series int
  Number of chart bars to look back.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `interval_bars_back?`: series int
  Number of interval bars to look back.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("time() Example", overlay=true)
// Highlight bars between 09:30 and 11:00 in the exchange's time zone
inWindow = not na(time(interval.interval, "0930-1100"))
bgcolor(inWindow ? color.new(color.orange, 0.15) : na)
```

### id

function:time~1

## time (function)

Returns the opening time of the current bar in UNIX milliseconds, measured on `interval` rather than on the chart's own bars.

With `session`, it returns `na` when the opening time of the `interval` bar is outside that session. The session is tested against the start of the `interval` bar, not against the opening time of the chart bar: with `interval` "1D" the tested time is the start of the day, so a session that does not contain midnight, such as "0930-1600", gives `na` on every bar of an intraday chart. Interval bars are cut on the clock in that time zone, not aligned to the chart's bars: with `interval` "1h", a chart bar opening at 09:30 is tested as 09:00, so an `interval` equal to the chart's own interval tests the chart bar's own time only when the chart's bars start on those clock boundaries. `timezone` sets the time zone the interval and the session are read in. `bars_back` and `interval_bars_back` look back a number of chart bars or interval bars respectively.

### syntax

```
time(series string interval, series string session, series string timezone, series int bars_back, series int interval_bars_back) → series int
```

### args

- `interval?`: series string
  The interval the time is measured on: a count and a unit, such as "15m", "4h" or "1D", with the units `s`, `m`, `h`, `D`, `W` and `M`. For `D`, `W` and `M` the count must be 1. Any other string compiles and gives `na`.
  types: series string, simple string, input string, const string, literal string
  default: interval.interval
- `session?`: series string
  A session. Bars outside it return `na`.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `timezone?`: series string
  The time zone the session is read in.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone
- `bars_back?`: series int
  Number of chart bars to look back.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `interval_bars_back?`: series int
  Number of interval bars to look back.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series int

### notes

- `timezone` takes UTC/GMT notation such as "UTC-5" or "GMT+0530", or an IANA time zone name. A name that cannot be read is ignored and the exchange's time zone is used, with no error.

### example

```lipi
//@lipi=2
indicator("time() Example", overlay=true)
// Highlight bars between 09:30 and 11:00 in the exchange's time zone
inWindow = not na(time(interval.interval, "0930-1100"))
bgcolor(inWindow ? color.new(color.orange, 0.15) : na)
```

### id

function:time~2

## time_close (variable)

The bar's closing time, distinct from `time`.

It is the opening time advanced by one interval, in the same unit: milliseconds from the Unix epoch. Both are int series, so a script can compare the two or pass either to a date function.

### type

series int

### example

```lipi
//@lipi=2
indicator(title="Time Close Example", overlay=true)
plot(time_close, title="Bar Close Time", color=color.blue)
```

### id

variable:time_close

## time_close (function)

Returns the closing time of the current bar in UNIX milliseconds, measured on `interval`. It takes the same arguments as `time`. With `session` it returns `na` when the opening time of the `interval` bar is outside the session, tested as for `time`: against the start of the `interval` bar, not the opening time of the chart bar.

### syntax

```
time_close(series string interval, series string session, series int bars_back, series int interval_bars_back) → series int
```

### args

- `interval?`: series string
  The interval the time is measured on: a count and a unit, such as "15m", "4h" or "1D", with the units `s`, `m`, `h`, `D`, `W` and `M`. For `D`, `W` and `M` the count must be 1. Any other string compiles and gives `na`.
  types: series string, simple string, input string, const string, literal string
  default: interval.interval
- `session?`: series string
  A session. Bars outside it return `na`.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `bars_back?`: series int
  Number of chart bars to look back.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `interval_bars_back?`: series int
  Number of interval bars to look back.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("time_close Example", overlay=false)
// Minutes left until the daily bar closes
minutesLeft = (time_close("1D") - time) / 60000
plot(minutesLeft, title="Minutes to Daily Close", color=color.blue)
```

### id

function:time_close~1

## time_close (function)

Returns the closing time of the current bar in UNIX milliseconds, measured on `interval`. It takes the same arguments as `time`. With `session` it returns `na` when the opening time of the `interval` bar is outside the session, tested as for `time`: against the start of the `interval` bar, not the opening time of the chart bar.

### syntax

```
time_close(series string interval, series string session, series string timezone, series int bars_back, series int interval_bars_back) → series int
```

### args

- `interval?`: series string
  The interval the time is measured on: a count and a unit, such as "15m", "4h" or "1D", with the units `s`, `m`, `h`, `D`, `W` and `M`. For `D`, `W` and `M` the count must be 1. Any other string compiles and gives `na`.
  types: series string, simple string, input string, const string, literal string
  default: interval.interval
- `session?`: series string
  A session. Bars outside it return `na`.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `timezone?`: series string
  The time zone the session is read in.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone
- `bars_back?`: series int
  Number of chart bars to look back.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `interval_bars_back?`: series int
  Number of interval bars to look back.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series int

### notes

- `timezone` takes UTC/GMT notation such as "UTC-5" or "GMT+0530", or an IANA time zone name. A name that cannot be read is ignored and the exchange's time zone is used, with no error.

### example

```lipi
//@lipi=2
indicator("time_close Example", overlay=false)
// Minutes left until the daily bar closes
minutesLeft = (time_close("1D") - time) / 60000
plot(minutesLeft, title="Minutes to Daily Close", color=color.blue)
```

### id

function:time_close~2

## time_sessionday (variable)

The UNIX time, in milliseconds, of the trading day the current bar belongs to. For instruments whose session starts the evening before, it gives the date the session is traded for rather than the calendar date of the bar.

### type

series int

### example

```lipi
//@lipi=2
indicator("time_sessionday Example", overlay=true)
newTradingDay = time_sessionday != time_sessionday[1]
bgcolor(newTradingDay ? color.new(color.blue, 0.3) : na)
```

### id

variable:time_sessionday

## timenow (variable)

The current time, rather than a time taken from the bar.

It is the instant the script ran, in milliseconds from the Unix epoch, and it is typed as a series like the bar's own time values.

### type

series int

### example

```lipi
//@lipi=2
indicator(title="Time Now Example", overlay=true)
plot(timenow, title="Current Time", color=color.blue)
```

### id

variable:timenow

## timestamp (function)

Assembles a time from its parts - the other direction from the eight functions that take a time apart.

The parts are read as a wall-clock time in the exchange's own timezone, and the result is milliseconds from the Unix epoch, matching `time` and `timenow`.

Two forms. Pass series arguments and you get a series int; pass simple arguments and you get a simple int. In both forms the year, the month and the day are required, and the hour, the minute and the second may be left out, each defaulting to zero. A date string, as in `timestamp("2024-01-01")`, is also accepted, and so is a leading `timezone` string, as in `timestamp("UTC", 2024, 1, 1)`. A date string is read as UTC unless it carries its own zone (`"2024-01-01T09:30:00-05:00"`), not in the exchange's timezone, and a string that cannot be read gives `na`.

### syntax

```
timestamp(const string dateString) → const int
```

### args

- `dateString`: const string
  The date to convert, as a string.
  types: const string, literal string

### returnedType

const int

### notes

- The result is worked out when the script runs. Where a value is needed when the script is compiled, such as the default of `input.time`, a `timestamp` call gives `na`, and adding the script to the chart fails with "Argument `defval` of `input.time()` cannot be `na`.": write the time as a number of milliseconds instead.

### example

```lipi
//@lipi=2
indicator("timestamp")
plot(timestamp(2025, 03, 11, 09, 30), linewidth=3, color=color.green)
plot(timestamp(2025, 03, 11, 09, 30), color=color.yellow)
plot(timestamp(2025, 03, 11, 09, 30, 15), color=color.lime)
```

### id

function:timestamp~1

## timestamp (function)

Assembles a time from its parts - the other direction from the eight functions that take a time apart.

The parts are read as a wall-clock time in the exchange's own timezone, and the result is milliseconds from the Unix epoch, matching `time` and `timenow`.

Two forms. Pass series arguments and you get a series int; pass simple arguments and you get a simple int. In both forms the year, the month and the day are required, and the hour, the minute and the second may be left out, each defaulting to zero. A date string, as in `timestamp("2024-01-01")`, is also accepted, and so is a leading `timezone` string, as in `timestamp("UTC", 2024, 1, 1)`. A date string is read as UTC unless it carries its own zone (`"2024-01-01T09:30:00-05:00"`), not in the exchange's timezone, and a string that cannot be read gives `na`.

### syntax

```
timestamp(series string dateString) → series int
```

### args

- `dateString`: series string
  The date to convert, as a string.
  types: series string, simple string, input string, const string, literal string

### returnedType

series int

### notes

- The result is worked out when the script runs. Where a value is needed when the script is compiled, such as the default of `input.time`, a `timestamp` call gives `na`, and adding the script to the chart fails with "Argument `defval` of `input.time()` cannot be `na`.": write the time as a number of milliseconds instead.

### example

```lipi
//@lipi=2
indicator("timestamp")
plot(timestamp(2025, 03, 11, 09, 30), linewidth=3, color=color.green)
plot(timestamp(2025, 03, 11, 09, 30), color=color.yellow)
plot(timestamp(2025, 03, 11, 09, 30, 15), color=color.lime)
```

### id

function:timestamp~2

## timestamp (function)

Assembles a time from its parts - the other direction from the eight functions that take a time apart.

The parts are read as a wall-clock time in the exchange's own timezone, and the result is milliseconds from the Unix epoch, matching `time` and `timenow`.

Two forms. Pass series arguments and you get a series int; pass simple arguments and you get a simple int. In both forms the year, the month and the day are required, and the hour, the minute and the second may be left out, each defaulting to zero. A date string, as in `timestamp("2024-01-01")`, is also accepted, and so is a leading `timezone` string, as in `timestamp("UTC", 2024, 1, 1)`. A date string is read as UTC unless it carries its own zone (`"2024-01-01T09:30:00-05:00"`), not in the exchange's timezone, and a string that cannot be read gives `na`.

### syntax

```
timestamp(simple int year, simple int month, simple int day, simple int hour, simple int minute, simple int second) → simple int
```

### args

- `year`: simple int
  Year.
  types: simple int, input int, const int, literal int
- `month`: simple int
  Month.
  types: simple int, input int, const int, literal int
- `day`: simple int
  Day.
  types: simple int, input int, const int, literal int
- `hour?`: simple int
  (Optional argument) Hour. Default is 0.
  types: simple int, input int, const int, literal int
  default: 0
- `minute?`: simple int
  (Optional argument) Minute. Default is 0.
  types: simple int, input int, const int, literal int
  default: 0
- `second?`: simple int
  (Optional argument) Second. Default is 0.
  types: simple int, input int, const int, literal int
  default: 0

### returnedType

simple int

### notes

- The result is worked out when the script runs. Where a value is needed when the script is compiled, such as the default of `input.time`, a `timestamp` call gives `na`, and adding the script to the chart fails with "Argument `defval` of `input.time()` cannot be `na`.": write the time as a number of milliseconds instead.

### example

```lipi
//@lipi=2
indicator("timestamp")
plot(timestamp(2025, 03, 11, 09, 30), linewidth=3, color=color.green)
plot(timestamp(2025, 03, 11, 09, 30), color=color.yellow)
plot(timestamp(2025, 03, 11, 09, 30, 15), color=color.lime)
```

### id

function:timestamp~3

## timestamp (function)

Assembles a time from its parts - the other direction from the eight functions that take a time apart.

The parts are read as a wall-clock time in the exchange's own timezone, and the result is milliseconds from the Unix epoch, matching `time` and `timenow`.

Two forms. Pass series arguments and you get a series int; pass simple arguments and you get a simple int. In both forms the year, the month and the day are required, and the hour, the minute and the second may be left out, each defaulting to zero. A date string, as in `timestamp("2024-01-01")`, is also accepted, and so is a leading `timezone` string, as in `timestamp("UTC", 2024, 1, 1)`. A date string is read as UTC unless it carries its own zone (`"2024-01-01T09:30:00-05:00"`), not in the exchange's timezone, and a string that cannot be read gives `na`.

### syntax

```
timestamp(series int year, series int month, series int day, series int hour, series int minute, series int second) → series int
```

### args

- `year`: series int
  Year.
  types: series int, simple int, input int, const int, literal int
- `month`: series int
  Month.
  types: series int, simple int, input int, const int, literal int
- `day`: series int
  Day.
  types: series int, simple int, input int, const int, literal int
- `hour?`: series int
  (Optional argument) Hour. Default is 0.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `minute?`: series int
  (Optional argument) Minute. Default is 0.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `second?`: series int
  (Optional argument) Second. Default is 0.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series int

### notes

- The result is worked out when the script runs. Where a value is needed when the script is compiled, such as the default of `input.time`, a `timestamp` call gives `na`, and adding the script to the chart fails with "Argument `defval` of `input.time()` cannot be `na`.": write the time as a number of milliseconds instead.

### example

```lipi
//@lipi=2
indicator("timestamp")
plot(timestamp(2025, 03, 11, 09, 30), linewidth=3, color=color.green)
plot(timestamp(2025, 03, 11, 09, 30), color=color.yellow)
plot(timestamp(2025, 03, 11, 09, 30, 15), color=color.lime)
```

### id

function:timestamp~4

## timestamp (function)

Assembles a time from its parts - the other direction from the eight functions that take a time apart.

The parts are read as a wall-clock time in the exchange's own timezone, and the result is milliseconds from the Unix epoch, matching `time` and `timenow`.

Two forms. Pass series arguments and you get a series int; pass simple arguments and you get a simple int. In both forms the year, the month and the day are required, and the hour, the minute and the second may be left out, each defaulting to zero. A date string, as in `timestamp("2024-01-01")`, is also accepted, and so is a leading `timezone` string, as in `timestamp("UTC", 2024, 1, 1)`. A date string is read as UTC unless it carries its own zone (`"2024-01-01T09:30:00-05:00"`), not in the exchange's timezone, and a string that cannot be read gives `na`.

### syntax

```
timestamp(simple string timezone, simple int year, simple int month, simple int day, simple int hour, simple int minute, simple int second) → simple int
```

### args

- `timezone?`: simple string
  The time zone, in UTC/GMT notation (e.g., "UTC-5", "GMT+0530") or as an IANA time zone database name (e.g., "America/New_York"). A name that cannot be read stops the script with the runtime error `invalid timezone: <name>`.
  types: simple string, input string, const string, literal string
  default: syminfo.timezone
- `year`: simple int
  Year.
  types: simple int, input int, const int, literal int
- `month`: simple int
  Month.
  types: simple int, input int, const int, literal int
- `day`: simple int
  Day.
  types: simple int, input int, const int, literal int
- `hour?`: simple int
  (Optional argument) Hour. Default is 0.
  types: simple int, input int, const int, literal int
  default: 0
- `minute?`: simple int
  (Optional argument) Minute. Default is 0.
  types: simple int, input int, const int, literal int
  default: 0
- `second?`: simple int
  (Optional argument) Second. Default is 0.
  types: simple int, input int, const int, literal int
  default: 0

### returnedType

simple int

### notes

- The result is worked out when the script runs. Where a value is needed when the script is compiled, such as the default of `input.time`, a `timestamp` call gives `na`, and adding the script to the chart fails with "Argument `defval` of `input.time()` cannot be `na`.": write the time as a number of milliseconds instead.

### example

```lipi
//@lipi=2
indicator("timestamp")
plot(timestamp(2025, 03, 11, 09, 30), linewidth=3, color=color.green)
plot(timestamp(2025, 03, 11, 09, 30), color=color.yellow)
plot(timestamp(2025, 03, 11, 09, 30, 15), color=color.lime)
```

### id

function:timestamp~5

## timestamp (function)

Assembles a time from its parts - the other direction from the eight functions that take a time apart.

The parts are read as a wall-clock time in the exchange's own timezone, and the result is milliseconds from the Unix epoch, matching `time` and `timenow`.

Two forms. Pass series arguments and you get a series int; pass simple arguments and you get a simple int. In both forms the year, the month and the day are required, and the hour, the minute and the second may be left out, each defaulting to zero. A date string, as in `timestamp("2024-01-01")`, is also accepted, and so is a leading `timezone` string, as in `timestamp("UTC", 2024, 1, 1)`. A date string is read as UTC unless it carries its own zone (`"2024-01-01T09:30:00-05:00"`), not in the exchange's timezone, and a string that cannot be read gives `na`.

### syntax

```
timestamp(series string timezone, series int year, series int month, series int day, series int hour, series int minute, series int second) → series int
```

### args

- `timezone?`: series string
  The time zone, in UTC/GMT notation (e.g., "UTC-5", "GMT+0530") or as an IANA time zone database name (e.g., "America/New_York"). A name that cannot be read stops the script with the runtime error `invalid timezone: <name>`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone
- `year`: series int
  Year.
  types: series int, simple int, input int, const int, literal int
- `month`: series int
  Month.
  types: series int, simple int, input int, const int, literal int
- `day`: series int
  Day.
  types: series int, simple int, input int, const int, literal int
- `hour?`: series int
  (Optional argument) Hour. Default is 0.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `minute?`: series int
  (Optional argument) Minute. Default is 0.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `second?`: series int
  (Optional argument) Second. Default is 0.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series int

### notes

- The result is worked out when the script runs. Where a value is needed when the script is compiled, such as the default of `input.time`, a `timestamp` call gives `na`, and adding the script to the chart fails with "Argument `defval` of `input.time()` cannot be `na`.": write the time as a number of milliseconds instead.

### example

```lipi
//@lipi=2
indicator("timestamp")
plot(timestamp(2025, 03, 11, 09, 30), linewidth=3, color=color.green)
plot(timestamp(2025, 03, 11, 09, 30), color=color.yellow)
plot(timestamp(2025, 03, 11, 09, 30, 15), color=color.lime)
```

### id

function:timestamp~6

## true (constant)

The bool value true. Comparisons and conditions produce it; it can also be written directly, as a default value or a constant.

### type

const bool

### example

```lipi
//@lipi=2
indicator("true Example", overlay=true)
showMA = true
plot(showMA ? talib.sma(close, 20) : na, title="SMA", color=color.blue)
```

### id

constant:true

## type (keyword)

Declares an object type of your own: a name, then a braced block with one typed field per line. A field may carry a default value, and at least one field is required.

A field's data type may carry type arguments in angle brackets, as in `array<float> xs`.

### syntax

```
type <type_name> {
	<data_type> <field_name> [= <default_value>]
	...
}
```

### notes

- A user-defined type can be the type argument of an array: `array.new<Zone>()` compiles when `Zone` is declared with `type`.
- A `type` block with no field is rejected.
- Create an instance with `<type_name>.new(...)`, giving the arguments by position or by field name: `Zone.new(high, 0)` and `Zone.new(top=high, touches=0)` are both accepted. Calling the type name without `.new`, as in `Zone(high, low)`, is rejected.
- A field is read as `z.top` and written with `:=`, as in `z.touches := z.touches + 1`.

### example

```lipi
//@lipi=2
indicator("type Example", overlay=true)
// An object type with two typed fields, one with a default
type Swing {
    float price
    int barIndex = 0
}
static Swing lastHigh = Swing.new(high, bar_index)
if high > lastHigh.price {
    lastHigh := Swing.new(high, bar_index)
}
plot(lastHigh.price, title="Highest High So Far", color=color.green)
```

### id

keyword:type

## volume (variable)

The volume traded in the bar.

It is a float rather than an int, so it carries fractional volumes without a conversion.

### type

series float

### example

```lipi
//@lipi=2
indicator(title="Average Volume Example", overlay=true)
length = 20
average_volume = talib.sma(volume, length)
plot(volume, title="Volume", color=color.blue)
plot(average_volume, title="Average Volume", color=color.red)
```

### id

variable:volume

## weekofyear (function)

The week of the year of a time you supply.

It is the one member of this family with no variable form: to get the current bar's week, pass the bar's `time`.

### syntax

```
weekofyear(series int time, series string timezone) → series int
```

### args

- `time`: series int
  UNIX time, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `timezone?`: series string
  The time zone the value is read in: an IANA time zone database name (for example "America/New_York") or "UTC". Unlike `timestamp`, `time` and `str.format_time`, this function does not accept offset notation such as "UTC-5" or "GMT+0530": a name that cannot be loaded gives 0, not `na`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Week of Year Example", overlay=true)
// Current bar time
currentWeek = weekofyear(time)
// Plot week number in Data Window
plot(currentWeek, title="Week Number")
```

### id

function:weekofyear

## while (keyword)

Repeats a block for as long as a condition holds. `break` leaves the loop and `continue` starts the next pass.

Give it an exit you control. A loop that passes the script's resource limits stops with a diagnostic rather than a partial result, and a `break` outside a loop is rejected.

### syntax

```
while <condition> {
	...
	break
	...
	continue
	...
}
```

### notes

- The counted loop `for i = 0 to <n> { ... }`, with an optional `step <m>`, and the iteration loop `for x in <array> { ... }` also compile.

### example

```lipi
//@lipi=2
indicator("While Loop Example", overlay=true)
// Initialize a counter variable
static int count = 0
// Run while loop until count reaches 5
while count < 5 {
    count := count + 1
}
// Plot the final count
plot(count, title="Counter", color=color.blue)
```

### id

keyword:while

## year (variable)

The year of the bar being evaluated.

A function of the same name also exists. The variable reads the current bar; the function reads whatever time you hand it.

### type

series int

### example

```lipi
//@lipi=2
indicator(title="Year Example", overlay=true)
currentYear = year
plot(currentYear, title="Year", color=color.blue)
```

### id

variable:year

## year (function)

The year of a time you supply.

Eight functions of this shape exist, each taking a time and an optional timezone, so only the time is required. The variable of the same name reads the current bar instead.

### syntax

```
year(series int time, series string timezone) → series int
```

### args

- `time`: series int
  UNIX time, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `timezone?`: series string
  The time zone the value is read in: an IANA time zone database name (for example "America/New_York") or "UTC". Unlike `timestamp`, `time` and `str.format_time`, this function does not accept offset notation such as "UTC-5" or "GMT+0530": a name that cannot be loaded gives 0, not `na`.
  types: series string, simple string, input string, const string, literal string
  default: syminfo.timezone

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Year Function Example", overlay=true)
// Get current bar year
currentYear = year(time)
// Plot year in Data Window
plot(currentYear, title="Current Year")
```

### id

function:year

## || (operator)

 It evaluates two Boolean expressions and returns true if at least one of them is true.

### syntax

```
expr0 || expr1 | expr0 or expr1
```

### example

```lipi
//@lipi=2
indicator("Logical OR Example", overlay=true)
// || is the symbol spelling of or
gap = open > high[1] || open < low[1]
bgcolor(gap ? color.new(color.orange, 0.2) : na)
```

### id

operator:||
