Contents: What a variable is on each bar · Order inside a run · History, then the live bar · What the previous value of a variable is · The index · The 500-bar reach · static · intra · What a tick starts from · The barstate variables · calc_on_every_tick · Where a call is skipped · Call it on every bar, then choose · The same holds for your own functions · Index · The parts · Top level only · What a script cannot contain · The first line · One statement to a line · Blocks · Continuing a long statement · Literals · na · Declaring and typing a variable · Whole numbers · Converting · The four qualifiers · Where each is required · A const that becomes series · Precedence · Arithmetic · Comparison and logic · The conditional expression · The history operator · if, else if, else · switch · What may go inside a branch · for i = a to b · for x in array · while, break, continue · The word step · Declaring · Returning several values · What a function may change · Declare a type · Create an instance and use its fields · Instances are shared, not copied · Keep instances in an array · Types in functions · Enums · Create an array · Add, read and remove · Keep an array across bars · Loop over an array · Arrays of drawings · Arrays are shared, not copied · ta and talib · Rules for names · Parts of a time · Testing a session · The chart's interval · What a script can read · What a script cannot read · When an instrument lacks the data · Top level only · plot · Where a plot is shown: display and format · Marks on bars · Your own bars and a level · Constants and hex · Opacity · Colors that change by bar · Gradients · Reading a color · Matching the chart's theme · Levels · Fill between two plots · Fill between two levels · Gradient fills · What fill does not accept · barcolor and bgcolor · display accepts only all and none · Fixed text on a mark · Text from data: label.new · Create · Change and delete · Chart points and polylines · How many a script keeps · Create and fill · Change a table · Limits · The refused forms · What to use instead · The declaration · When orders fill · The order calls · One trade at a time · Common arguments · Options · Time · Enum · input.source accepts names, not expressions · alert · alertcondition · One spelling · Layout · Names · Messages · Drawings and tables · Not limited · Syntax · Names · Types and qualifiers · Arguments and scope · Compile-path-only rules · Runtime errors

<!-- /docs/scripting/evaluation/bar-by-bar -->

# Bar-by-bar evaluation

Lipi has no loop over the chart. The chart runs your whole script from the first line to the last once for each bar, starting
with the oldest bar that is loaded and ending with the newest. In every run `close`, `high`, `bar_index` and the other built-in
series hold the values of that one bar; the script cannot see later bars.

## What a variable is on each bar

A variable you declare with `=` is created again on every bar, so it starts from its initial value each time. Earlier values stay
reachable through the history operator (`x[1]`, see [Referencing previous bars](/scripting/evaluation/referencing-past-bars)). To
carry a value from one bar to the next, declare it `static` (see [Values that persist across bars](/scripting/evaluation/persistence)).

```lipi
//@lipi=2
indicator("Variables per bar")
int fresh = 0
static int kept = 0
fresh += 1
kept += 1
plot(fresh, title="Fresh each bar")
plot(kept, title="Kept across bars")
```

`fresh` is 1 on every bar; `kept` is 1, 2, 3, ...

## Order inside a run

Statements run top to bottom. A function runs when it is called, and a block only when its condition holds on that bar. A top-level
`plot` is evaluated on every bar and draws nothing where its value is `na`.

## History, then the live bar

Each historical bar runs once. The newest bar of a live chart is still forming, so it runs again on every price tick (see
[Recalculation and confirmation](/scripting/evaluation/recalculation)). The first bars give `na` for anything that needs earlier
bars, such as a 20-bar average on bar 5.

<!-- /docs/scripting/evaluation/referencing-past-bars -->

# Referencing previous bars

`x[n]` is the value that `x` had `n` bars ago. `x[0]` is the current value and `x[1]` the previous bar's. The operator is written
after the value and works on built-in series (`close[1]`), on your own variables, on function results (`talib.sma(close, 5)[1]`)
and on parenthesised expressions. It does not work on a literal or on `na`: History Indexing cannot be used on literal or built-in
non series values.

```lipi
//@lipi=2
indicator("Close change and range", overlay=false)
float change = close - nz(close[1])
float high3 = math.max(high, high[1], high[2])
float range3 = high3 - math.min(low, low[1], low[2])
plot(change, title="Change")
plot(range3, title="3-bar range")
```

## What the previous value of a variable is

`x[1]` is the value `x` had when the previous bar's run finished, after all its `:=` assignments. A variable you do not
index keeps no history. For a value that must be updated from its own previous value, use `static` instead of `x[1]` (see
[Values that persist across bars](/scripting/evaluation/persistence)).

When the bars do not reach far enough back, the result is `na` (`close[1]` on the first bar). Wrap it in `nz(close[1])` to get 0, or
`nz(close[1], close)` to get another default.

## The index

- It is a number; a series value is accepted (`close[bar_index % 3]`), and a fraction is rounded down.
- A string is refused: History Index must be a number. Got string.
- A negative literal is refused by the editor: History index must be >= 0. Got -1. There is no way to read a later bar.

## The 500-bar reach

The index, and the length of any `talib` window, may be at most 500. A larger value passes the editor's check, and the script stops when
it runs with an error on the chart. `talib.ema` (and `macd`, `bbw`, `kc`, `kcw`, which use it) is refused already when the script is added to
the chart, with the same message:

```text
The script is trying to access historical data outside allowed range (501). The allowed range is 0 to 500.
```

A computed index that is negative stops the script the same way. For a longer look-back keep the values in a `static` variable or
an array (see [Arrays](/scripting/language/arrays); on an array, `a[1]` is the array one bar ago, not its second element).

<!-- /docs/scripting/evaluation/persistence -->

# Values that persist across bars

A variable declared with `=` starts over on every bar (see [Bar-by-bar evaluation](/scripting/evaluation/bar-by-bar)). Two keywords
before the declaration keep a value: `static` across bars and `intra` across the repeated runs of one forming bar.

## static

`static type name = initial` runs the initialiser when execution first reaches the declaration with no committed value: on the
first bar, or on a later bar for a declaration inside a branch or function not reached before. After that the declaration is skipped
and the variable starts with the value committed at the end of the previous bar. Change it with `:=` or a compound assignment.

```lipi
//@lipi=2
indicator("Running volume")
static float total = 0
total += volume
plot(total, title="Running volume")
```

- On a forming bar the script runs on every tick, and each run starts from the value committed when the last bar closed, so
  `total += volume` adds the bar once, not once per tick.
- `static` works for any type: `static label last = na` keeps a drawing handle; a line, label, box or linefill held directly by a
  `static` variable is never trimmed for being over the drawing limit (one in an array, or a polyline, is not).
- An array or object in a `static` variable is restored the same way on a forming bar, so `array.push(window, close)` adds the bar
  once, not once per tick. Objects nested inside it are shared with the committed copy: change a field of an element of a
  `static array<Swing>` only under `barstate.isconfirmed`.
- It works inside blocks and functions. In a function it belongs to the call site: two calls keep two values.

## intra

`intra` keeps a value across the repeated runs of one forming bar and forgets it when the bar closes, so the next bar starts from
the initialiser again.

```lipi
//@lipi=2
indicator("Runs of this bar")
intra int runs = 0
runs += 1
plot(runs, title="Runs of this bar")
```

On a live chart `runs` counts the ticks of the forming bar (1, 2, 3, ...) and returns to 1 on the next bar; with `calc_on_every_tick=false` the forming bar runs once, when it closes, so it shows 1. On history every bar runs
once, so `intra` behaves like an ordinary variable and shows 1; a strategy with `calc_on_order_fills=true` is the exception, because it
reruns a bar after a fill and `intra` values carry over the reruns. Use it for what must accumulate during a bar but not across bars.

Use a plain variable for a value recomputed from the bar's own data, `static` for a running total, counter, last signal or drawing
handle, and `x[1]` for the value a variable had one bar ago (see [Referencing previous bars](/scripting/evaluation/referencing-past-bars)).

<!-- /docs/scripting/evaluation/recalculation -->

# Recalculation and confirmation

On history each bar runs once, after it has closed. The newest bar of a live chart has not closed, so its price keeps changing and
the script runs again on every tick; the result for that bar can change until it closes. A closed bar is confirmed and never
recalculated.

## What a tick starts from

Before each run on the forming bar the chart restores the state of the last confirmed bar:

- series history (`x[1]`) and `talib` state have not advanced;
- `static` variables have the value committed at the last close (see [Values that persist across bars](/scripting/evaluation/persistence));
- drawings are those of the last confirmed bar, so a label made on an earlier tick of this bar is gone;
- only `intra` variables keep what the previous tick left.

When the bar closes, the script runs once more with `barstate.isconfirmed` true and that result is committed.

## The barstate variables

All are `bool` series values.

| Variable | True when |
|---|---|
| `barstate.isconfirmed` | the bar has closed: every historical bar and the last run of a live bar. False on earlier ticks of a forming bar and on the last historical bar while the market is open |
| `barstate.isnew` | the first run of the bar (every historical bar) |
| `barstate.isrealtime`, `barstate.ishistory` | the bar is live (on every run of it, the closing run too), or was loaded as history |
| `barstate.islast`, `barstate.isfirst` | the newest bar, the first bar of the chart |
| `barstate.islastconfirmedhistory` | the last loaded bar, when the market is closed |

A signal built on the `close` of a forming bar can switch on and off as the price moves; guard it with `barstate.isconfirmed`:

```lipi
//@lipi=2
indicator("Confirmed up bar", overlay=true)
bool signal = close > open and barstate.isconfirmed
plotshape(signal, title="Up bar", shape=shape.triangleup, location=location.belowbar)
```

## calc_on_every_tick

The argument of `indicator()` and `strategy()` decides whether the forming bar runs at all before it closes.

| Script | Default | `true` | `false` |
|---|---|---|---|
| `indicator()` | `true` | runs on every tick | runs only when the bar closes; nothing is shown for the forming bar until then |
| `strategy()` | `false` | runs on every tick | runs when the bar closes (and after an order fill when `calc_on_order_fills=true`) |

`calc_on_every_tick` does not change history: every closed bar runs once, plus a rerun after each fill in a strategy with `calc_on_order_fills=true`. `alert()` fires at most once per bar and only on live bars.

<!-- /docs/scripting/evaluation/call-contract -->

# Calls that must run on every bar

A function that looks at earlier bars, such as `talib.sma`, `talib.ema` or `talib.rsi`, does not read the chart's bars. It keeps
its own history, one per place in your script where you call it (the call site), and that history grows by one entry only on the bars
where the call actually runs. Its "previous bar" is the previous time the call ran.

So a `talib` call is correct only when it runs once on every bar. A call that is skipped on some bars gives wrong numbers and no error.

## Where a call is skipped

A call does not run on a bar when it sits in an `if` or `switch` block whose condition is false, in the unchosen side of `c ? a : b`
(only one side runs; both sides of `and` and `or` always run), or in a function that is itself called on some bars only.

A call in a loop body is one call site run several times a bar: the passes overwrite each other and only the last is kept. Do not
call `talib` functions inside a loop.

## Call it on every bar, then choose

Make the call at the top level, then use its result in the condition:

```lipi
//@lipi=2
indicator("Average on up bars", overlay=true)
float avg = talib.sma(close, 20)
float shown = close > open ? avg : na
plot(shown, title="Average")
```

This is the opposite of the following script, which compiles but averages the last 20 up bars only, because the call runs on up bars only:

```lipi
//@lipi=2
indicator("Average of up bars", overlay=true)
float shown = na
if close > open {
    shown := talib.sma(close, 20)
}
plot(shown, title="Average")
```

## The same holds for your own functions

A history reference inside a function (`x[1]`), a `talib` call and a `static` variable all belong to the call site: two calls of one
function keep separate histories, and a call skipped on some bars sees only the bars it ran on.

```lipi
//@lipi=2
indicator("Smoothed change")
func smooth(float x) => (x + nz(x[1])) / 2
plot(smooth(close - open), title="Smoothed body")
```

`smooth` runs on every bar, so `x[1]` is the previous bar.

## Index

A history index counts recorded entries back. For a built-in series (`close[1]`) every bar is recorded; for your own variable, every
bar on which the line that sets it ran (a top-level variable is set on every bar). The reach is 500 entries (see
[Referencing previous bars](/scripting/evaluation/referencing-past-bars)).

<!-- /docs/scripting/language/anatomy -->

# Script anatomy

A script is a list of lines that the chart runs once for every bar (see [Bar-by-bar evaluation](/scripting/evaluation/bar-by-bar)): a
header, one declaration, then statements and declarations in any order.

```lipi
//@lipi=2
indicator("Anatomy", overlay=true)
length = input.int(20, "Length", minval=1)
func spread(float a, float b) => a - b
mid = talib.sma(close, length)
if barstate.islast {
    label.new(bar_index, mid, "Spread " + str.tostring(spread(high, low)))
}
plot(mid, title="Average")
```

## The parts

| Part | Rule |
|---|---|
| `//@lipi=2` | A directive that selects the language version, not an ordinary comment. Put it at the top, before any code (see [Statements and lines](/scripting/language/statements-and-lines)). |
| `indicator(...)` or `strategy(...)` | Exactly one, at the top level, with every argument `const` (see [qualifiers](/scripting/language/qualifiers)). Put it first. The arguments are in the [reference](/scripting/reference/global). |
| Statements | Assignments, calls, `if`, `switch`, `for`, `while`. |
| `func`, `def`; `type`, `enum` | Declarations: [functions](/scripting/language/custom-functions), [types and enums](/scripting/language/custom-types). |

## Top level only

These may not appear inside a function, `if`, loop or `switch`:

- `indicator`, `strategy`;
- `func`, `def`, `type` and `enum` declarations (a syntax error elsewhere);
- the calls that put output on the chart: `plot`, `plotshape`, `plotchar`, `plotarrow`, `plotbar`, `plotcandle`, `hline`, `fill`,
  `bgcolor`, `barcolor`, `alertcondition`. Inside a block they fail with `` `plot()` must be called in the global scope. `` (the name
  of the call you wrote). To draw only on some bars, put the condition in an argument instead (see [Branching](/scripting/language/branching)).

Variables, `input.*`, `talib` calls, drawings, `alert` and `strategy.*` orders may be used anywhere.

## What a script cannot contain

- `import`, `export`, `method` and `library()`: there are no libraries or modules.
- `request.*`: a script reads only the symbol and interval of its chart.
- Block comments: only `//` to the end of the line.
- `var` and `varip`: use `static` (see [Values that persist across bars](/scripting/evaluation/persistence)).

Drawings, arrays, history and run time have fixed limits (see [Limits](/scripting/distribution/limits)).

<!-- /docs/scripting/language/statements-and-lines -->

# Statements and lines

A Lipi statement ends at the end of its line. There is no statement separator character, and a block with statements is always
written over several lines (an empty `{}` is accepted). This page lists where a statement may continue on the next line and the layouts the compiler refuses, with the
message it gives for each.

## The first line

Every Lipi v2 script starts with the line `//@lipi=2`. A script without it is read as a Lipi v1 script, an older language with
other rules, so it may fail or behave differently. The next statement declares the script, once: `indicator(...)` for an
indicator, `strategy(...)` for a strategy (see [Strategies and backtesting](/scripting/strategies/overview)).

```lipi
//@lipi=2
indicator("Close")
plot(close)
```

A script with no declaration, or with two, is refused: Script must declare exactly one of `indicator()`, `strategy()`, or
`library()`; found 0 ((none)).

## One statement to a line

Put each statement on its own line. A semicolon does not separate statements:

```lipi-invalid
//@lipi=2
indicator("Two statements")
a = close; b = open
plot(a - b)
```

The compiler says: extraneous input ';' expecting {<EOF>, NEWLINE}. Write `a = close` and `b = open` on two lines. When several
lines are joined this way, the compiler reports only one of them, so fix them all before checking again.

Indentation does not matter to the compiler; indent blocks by four spaces for readers. Names are case-sensitive: `x` and `X` are
two variables. A comment starts with `//` and runs to the end of the line, on a line of its own or after a statement.

## Blocks

`if`, `else`, loops, `switch`, function bodies, `type` and `enum` use braces. The opening brace stays on the line that starts the
block, and the block's statements go on the lines after it, never on the same line as a brace:

```lipi-invalid
//@lipi=2
indicator("One-line block")
float x = 0
if close > open { x := 1 }
plot(x)
```

The compiler says: mismatched input 'x' expecting {'}', NEWLINE}. Write it over three lines:

```lipi
//@lipi=2
indicator("Block over three lines")
float x = 0
if close > open {
    x := 1
} else {
    x := -1
}
plot(x)
```

`else` may follow the closing brace on the same line, as above, or start the next line. The opening brace may not move to the
next line: `if close > open` followed by `{` on its own line is refused with extraneous input '\n' expecting '{'.

## Continuing a long statement

A statement may continue on the next line where the line clearly cannot end:

- after a comma or an opening parenthesis, inside the arguments of a call;
- after an operator (`+`, `-`, `*`, `/`, `and`, `or`, a comparison), at the end of the line;
- after `=`, `:=` or `=>`;
- after the `?` and the `:` of a conditional expression.

```lipi
//@lipi=2
indicator("Long statements", overlay=true)
rising = close > open and
  volume > talib.sma(volume, 20)
level = rising ?
  high :
  low
label.new(bar_index, level,
  text="Level",
  color=color.blue)
```

A line may not **start** with an operator: the line before it is then a complete statement, and the operator has nothing on
its left.

```lipi-invalid
//@lipi=2
indicator("Leading operator")
c = close
  + open
plot(c)
```

The compiler says: no viable alternative at input '\n+'. Move the operator to the end of the line before.

<!-- /docs/scripting/language/values-and-types -->

# Values and types

The basic types are `int`, `float`, `bool`, `string` and `color`. Arrays, drawings (`label`, `line`, ...) and your own types and enums
are covered in [Arrays](/scripting/language/arrays) and [Custom types and enums](/scripting/language/custom-types).

## Literals

| Type | Written as |
|---|---|
| `int` | `42` (no hexadecimal, no `1_000`). |
| `float` | `3.14`, `.5`, `2.`, `1e3`, `1.5e-2`. |
| `bool` | `true`, `false`. |
| `string` | `"text"` or `'text'`, on one line. Put a quote inside by using the other kind: `"say 'hi'"`. `+` joins two strings. |
| `color` | `#RRGGBB` or `#RRGGBBAA` (the last byte is the alpha, `FF` opaque), or a constant such as `color.red`. |

`color.new(color.red, 0.5)` sets an opacity from 0 (invisible) to 1 (solid); a value outside that range is clamped, with a warning.

## na

`na` means "no value": the first bars of a moving average, or history that does not reach back far enough. Arithmetic with an `na`
operand gives `na`, and so does a division by zero.

- Test with `na(x)` (not `x == na`, which warns); replace with `nz(x)` (0) or `nz(x, 5)`.
- A variable needs a type to start as `na`: `float x = na`. Without one: Value with NA type cannot be assigned to a variable that was
  defined without type keyword.

## Declaring and typing a variable

`name = value` declares a variable, and its type is the type of the first value: `x = 0` is an `int`. Write the type to choose another:
`float x = 0`. A typed declaration takes a compatible value: `float` takes an `int`, `bool` takes a number, `int` takes neither a
`float` nor a `bool`.

`:=` gives an existing variable a new value of its type; `+=`, `-=`, `*=`, `/=`, `%=` do the same with the result of the operation
(`+=` also joins strings).

```lipi-invalid
//@lipi=2
indicator("Wrong type")
x = 0
x := close
plot(x)
```

The compiler says: Variable `x` was declared with `const int` type. Declared type `int` is not compatible with assigned type `series float`. Use math.floor(), math.round(), or math.ceil() if you need a whole number.
Declare `float x = 0` instead.

## Whole numbers

`/` always gives a `float`, even for two integers, so `int half = length / 2` is refused with the message above (Declared type `int` is not compatible with
assigned type `input float`). Write `int half = math.floor(length / 2)`; those functions return an `int`. `/=` is refused on an `int` variable for the same reason.

## Converting

- `int(x)` drops the fraction toward zero (`int(-2.9)` is `-2`) and gives a typed `na` for `na`.
- `bool(x)` turns a number into `false` when it is zero and `true` otherwise; most bool arguments take a number the same way
  (`alertcondition` does not). `float(x)` turns an int into a float. `string(5)` and `int("5")` are refused.
- Number to text: `str.tostring(x)`. Text to number: `str.tonumber(s)`.

<!-- /docs/scripting/language/qualifiers -->

# const, input, simple and series

Besides its type, every value has a qualifier that says when it is known. It matters when a function demands a value that cannot
change from bar to bar and you give it one that can.

## The four qualifiers

From weakest to strongest:

| Qualifier | Known | Examples |
|---|---|---|
| `const` | when the script is compiled | `5`, `"Title"`, `color.red`, `10 * 2` |
| `input` | when the user sets the settings | the results of `input.int`, `input.float`, ... |
| `simple` | on the first bar, then fixed | `syminfo.mintick`, `interval.multiplier` |
| `series` | on every bar | `close`, `bar_index`, `talib.sma(close, 5)` |

A value fits a parameter whose qualifier is the same as its own or stronger: a `const` fits every parameter, a `series` only a
`series` one, and an `input` value does not fit a `const` parameter. An expression takes the strongest qualifier of its parts: `10 * 2` is `const`, `input.int(5) * 2` is `input`, `close * 2`
is `series`. `math.floor(x)` keeps the qualifier of `x`.

## Where each is required

- **`const`**: every argument of `indicator()` and `strategy()`; the `title` of `plot`, `plotshape`, `bgcolor`, `hline`,
  `alertcondition` and the other output calls; the default, `title`, `group` and `tooltip` of every `input.*`.
- **`input`**: `plot(linewidth=...)`, `hline(price, ...)`.
- **`series`**: nearly everything else, so `close` can go to `talib.sma`, `label.new` and your own functions, and a moving-average
  length may change from bar to bar.

```lipi-invalid
//@lipi=2
indicator("Dynamic title")
plot(close, title=str.tostring(close))
```

The compiler says: Cannot call `plot` with argument `title`=`str.tostring(close)`. An argument of `series string` type was used but a `const string` is expected.
The same message, with the other qualifier names, covers every mismatch; the editor's check raises it. A parameter of your own
function may start with `const`, `simple` or `series` (none means `series`; see [Your own functions](/scripting/language/custom-functions)).
A variable declaration takes no such word: `const int x = 5` is a syntax error.

## A const that becomes series

A variable reassigned inside a `for` or `switch` becomes `series` for the rest of the script, even if every value assigned is a
constant; inside an `if` it takes the qualifier of the condition: under `if true` it stays `const`, under an `input.bool` it is `input`, under `close > open` it is `series`.
So `int width = 1`, then `if close > open { width := 3 }`, then `plot(close, linewidth=width)` fails: Cannot call `plot` with argument `linewidth`=`width`. An argument of `series int` type was used but a `input int` is expected.
`c ? a : b` takes the strongest of `c`, `a` and `b` (`true ? 1 : 2` is `const`; `close > open ? 1 : 2` is `series` and fails the same way).
Use a literal or an `input.int` width, or draw one `plot` per case
with `na` on the bars where it does not apply: `plot(close > open ? close : na, linewidth=3)`.

<!-- /docs/scripting/language/expressions -->

# Operators and expressions

An expression combines values with operators. Use parentheses whenever two operators of different kinds meet.

## Precedence

| Level | Operators |
|---|---|
| 1 | unary `-`, unary `+`, `not` or `!` |
| 2 | `*` `/` `%`, left to right |
| 3 | `+` `-` |
| 4 to 7 | `>=`, then `<=`, then `>`, then `<`: each is a level of its own |
| 8, 9 | `==`, then `!=` |
| 10 | `and` or `&&` |
| 11 | `or` or `\|\|` |
| 12 | `c ? a : b`, right to left |

`not` binds tighter than a comparison: `not a > b` is `(not a) > b`, so write `not (a > b)`. Comparisons do not chain, because `a < b` is
a `bool` and the next `<` wants a number:

```lipi-invalid
//@lipi=2
indicator("Chained comparison")
plot(low < close < high ? 1 : 0)
```

The compiler says: Cannot call `operator <` with argument `expr0`=`low<close`. An argument of `series bool` type was used but a `series int` is expected.
Write `low < close and close < high`.

## Arithmetic

- `int` with `int` gives an `int`, except `/`, which always gives a `float` (see [Values and types](/scripting/language/values-and-types)).
  Any `float` operand gives a `float`. `bool` and `string` take no part in arithmetic.
- `%` is the remainder. There is no power operator: `x = close ^ 2` gives extraneous input '^' expecting {<EOF>, NEWLINE}. Write
  `math.pow(x, 2)`.
- An operand that is `na`, or a division by zero, gives `na`.

## Comparison and logic

- `==` and `!=` work on numbers, strings and enum members; `<` `>` `<=` `>=` on numbers.
- `and`, `or`, `not` are the same as `&&`, `||`, `!`. Both sides of `and` and `or` are always evaluated (no short-circuit), and if
  either side is `na` the result is `na`, which an `if` treats as false.
- An `if` or `while` condition is a `bool` or a number (zero is false); a string is refused.

## The conditional expression

`condition ? a : b` is `a` when the condition is true and `b` otherwise (`na` counts as false). Only the chosen branch runs, which
matters when it calls a `talib` function (see [Calls that must run on every bar](/scripting/evaluation/call-contract)). It nests to the right:
`x > 0 ? 1 : x < 0 ? -1 : 0`. The branches must have compatible types.

## The history operator

`x[n]` is the value `x` had `n` bars ago; `x[0]` is the current value. It works on series values, your own variables, call results
and parenthesised expressions, not on a literal or `na`. The index rules and the 500-bar reach are in [Referencing previous bars](/scripting/evaluation/referencing-past-bars).

```lipi-fragment
float change = close - nz(close[1])
float lagged = talib.sma(close, 5)[1]
```

`"Bar " + bar_index` is refused: `+` joins two strings, so write `"Bar " + str.tostring(bar_index)`.

<!-- /docs/scripting/language/branching -->

# Branching

`if` and `switch` choose which statements run on a bar. Both are statements with no value, so `x = if ...` is a syntax error; to choose
a value use `c ? a : b` (see [Operators and expressions](/scripting/language/expressions)).

## if, else if, else

```lipi
//@lipi=2
indicator("Candle label", overlay=true)
if barstate.islast {
    if close > open {
        label.new(bar_index, high, "Up", color=color.green)
    } else if close < open {
        label.new(bar_index, low, "Down", color=color.red)
    } else {
        label.new(bar_index, high, "Flat")
    }
}
```

The condition is a `bool` or a number (zero is false, and so is `na`). A string is refused: `if` conditional expression must be of a bool
type!. Braces and line breaks follow [Statements and lines](/scripting/language/statements-and-lines). A variable declared inside a
block is not visible after it, so declare it before the `if` and assign it with `:=`.

## switch

`switch value {` is followed by `case x:` lines and an optional `default:`.

```lipi
//@lipi=2
indicator("Color by phase")
int phase = bar_index % 3
color c = color.gray
switch phase {
    case 0:
        c := color.red
    case 1:
        c := color.green
    default:
        c := color.blue
}
plot(close, color=c)
```

- The first matching case runs and the `switch` ends: there is no fall-through and no `break` is needed.
- A `case` takes exactly one value (`case 0, 1:` is a syntax error). Strings and enum members work as values; the value must have the
  type of the subject (a `float` subject takes an `int` case).
- At most one `default`: Only one `default` case is allowed in a switch statement.

## What may go inside a branch

| Call | Inside `if`, `switch`, loops, functions |
|---|---|
| `label.new`, `line.new`, `box.new` and the other drawings | allowed |
| `alert(message)` | allowed |
| `strategy.entry`, `strategy.exit`, `strategy.close`, ... | allowed |
| `plot`, `hline`, `fill`, `bgcolor` and the rest of the plot family (listed in [Script anatomy](/scripting/language/anatomy)) | refused |

The refused calls draw one series for the whole script, so they belong at the top level:

```lipi-invalid
//@lipi=2
indicator("Plot in a branch")
if close > open {
    plot(close)
}
```

The compiler says: `plot()` must be called in the global scope. The editor's check reports it, and the name in the message is the call you wrote.
Put the condition into an argument and give `na` for the bars you want empty: `plot(close > open ? close : na, title="Up close")`.

<!-- /docs/scripting/language/repetition -->

# Loops

A loop repeats a block within one bar's run. Use `talib` functions for rolling statistics and loops for work that has no built-in,
such as scanning an array.

## for i = a to b

```lipi
//@lipi=2
indicator("Mean of five closes")
float total = 0
for i = 0 to 4 {
    total += nz(close[i])
}
plot(total / 5, title="Mean of 5")
```

- The counter takes the values `a`, `a + 1`, ..., `b`, so `0 to 4` runs five times.
- When `a` is larger than `b` the loop counts down by 1: `for i = 10 to 0`.
- When `a` equals `b` the body does not run at all. So `0 to n - 1` visits `n` positions only for `n` of 2 or more: for `n = 1` it
  runs zero times, and for `n = 0` it counts down through 0 and -1. For an array use `for x in a`.
- `step` sets the increment (`for i = 10 to 0 step -2`); its sign must point from `a` toward `b`, or the script stops when it runs
  with `Step value should be less than 0` or `Step value should be greater than 0`.
- `a`, `b` and `step` are numbers, evaluated once before the first pass; they may be series values. The counter has the type of `a`, so
  a loop with whole-number bounds cannot have a fractional step. The counter exists only inside the loop.

```lipi-invalid
//@lipi=2
indicator("Fractional step")
float s = 0
for i = 0 to 10 step 0.5 {
    s += i
}
plot(s)
```

The compiler says: The step value type (`literal float`) for the `for` loop is not compatible with counter `i` type (`literal int`).
Start the loop at `0.0` to count in floats.

## for x in array

`for x in a` visits the elements of the array variable `a` in order and does nothing for an empty array. After `in` comes the name of
an array variable, not an expression (anything else gives The `for ... in` loop can only iterate over an array.). `x` is a copy:
assigning to it does not change the array.

## while, break, continue

`while condition {` repeats while the condition (a `bool` or a number) holds. `break` leaves the innermost loop and `continue` skips
to its next pass; outside a loop both are refused: Break statement can only be used inside a loop.

```lipi-fragment
int i = 0
float s = 0
while i < 10 {
    i += 1
    if i % 2 == 0 {
        continue
    }
    s += i
}
```

No loop has an iteration limit; the 45-second run limit is the only stop (see [Limits](/scripting/distribution/limits)).

## The word step

`step` is reserved, so `int step = 2` is refused (no viable alternative at input 'intstep'), but it is allowed as a named argument:
`input.float(2.0, "Factor", step=0.5)`.

<!-- /docs/scripting/language/custom-functions -->

# Your own functions

A function names a calculation you use more than once. Declare it at the top level, above the first line that calls it.

## Declaring

```lipi
//@lipi=2
indicator("Scaled range")
func scaled(float x, float k = 2.0) => x * k
func midpoint(float a, float b) {
    float m = (a + b) / 2
    return m
}
plot(midpoint(high, low) + scaled(1, k=0.5), title="Middle")
```

- `func name(params) => expression` returns the expression. `func name(params) {` with a body and `return value` is the long form.
  With no keyword, `name(params) => expr` declares the same kind of function; use `func`. `def` declares something else (below).
- Each parameter has a type: `func f(x) => x` is a syntax error. A `const`, `simple` or `series` word may come first (see
  [qualifiers](/scripting/language/qualifiers)); with none it is `series`. `const` and `simple` only go with `int`, `float`, `bool`,
  `string` and `color`: for an array, object or drawing write `series` or nothing (Cannot use the `const` keyword when declaring a variable or parameter that accepts a non fundamental type.). A default is a literal or a built-in such as `close`, not
  a calculation.
- Functions of one name may differ in their parameters (`f(float x)` and `f(string s)`); two with the same parameter types are
  refused: The `f` function has overloads with the same parameters.
- Call with positional arguments, then named ones. A long-form function that returns a value must return on every path, and all
  returns must agree on type: The `f()` function is missing return statement. A `switch` does not help: with a `return` in every
  case and the `default` it is still missing, and a `switch` in a called function passes the editor's check but is refused on Add to chart
  (Not Implemented). Use `if` and `else`. A body with no `return` returns nothing: call it as a
  statement; assigning it is refused (Cannot assign void value.).
- A function may call functions declared above it, not itself and not one below it, so there is no recursion: a call to itself gives
  Function `fact` is not available here. Functions must be defined before use, and cannot call themselves. Use a loop instead.

## Returning several values

Return a tuple in brackets and unpack it with a bracketed declaration; the counts must match and the types may differ.

```lipi-fragment
func spread(float a, float b) => [math.min(a, b), math.max(a, b)]
[lo, hi] = spread(open, close)
```

`[lo, hi] := spread(...)` assigns existing variables. A tuple cannot go into a single variable, and the names take no types:
`[float lo, float hi] = ...` gives no viable alternative at input '[float'.

## What a function may change

A function reads global variables freely. What it may change is limited:

| Inside a function | Result |
|---|---|
| `:=`, `+=` and the like on a global variable | refused: Cannot modify global variable `hits` in function. |
| `hits = 1` where `hits` is global | declares a new local `hits`, with a warning |
| `array.push(arr, x)` or `arr.set(...)` on a global or passed array | works |
| `p.price := v` on a global or passed object | works |
| `plot`, `hline`, `fill`, `bgcolor` and the rest of the plot family | refused (see [Branching](/scripting/language/branching)) |

```lipi-invalid
//@lipi=2
indicator("Counter")
static int hits = 0
func bump() {
    hits += 1
    return hits
}
plot(bump())
```

The compiler says: Cannot modify global variable `hits` in function. Return the value and assign it outside:

```lipi
//@lipi=2
indicator("Rising bars")
static int hits = 0
func bumped(int n, bool up) => up ? n + 1 : n
hits := bumped(hits, close > open)
plot(hits)
```

An object or array is shared, not copied, so the caller sees a change to its contents.

`def name(Type x, ...)` declares a type function, not an ordinary one: `x` is the receiver, so it is also called as `value.name(...)`.
It needs at least one parameter (`def one() => 1` gives Type Function should have at least one parameter.), and a `func` cannot be
called with the dot.

History used inside a function (`x[1]`, `talib.*`) belongs to its call site, so call the function on every bar (see
[Calls that must run on every bar](/scripting/evaluation/call-contract)).

<!-- /docs/scripting/language/custom-types -->

# Custom types and enums

A `type` groups values that belong together, such as a price and the bar it was seen on, into one object you can store, pass to a
function and keep in an array. An `enum` names a fixed set of choices. Both are declared at the top level of the script.

## Declare a type

Write `type`, a name, and a braced block with one field per line. Each field is a data type and a name, and may have a default.

```lipi-fragment
type Swing {
    float price
    int barIndex = 0
}
```

A type needs at least one field. A default must be a plain value: a number, a string, `true` or `false`, a color constant, `na` or a built-in variable such as `close`.
A calculation or an ordinary variable is refused, even `-1` or `2 * 3`:

```lipi-invalid
//@lipi=2
indicator("Defaults")
type Counter {
    int start = 2 * 3
}
plot(close)
```

The compiler says: Default value of property `start` of object `Counter` cannot be a function, variable or calculation.

A field may hold any type: a fundamental type, a drawing such as `box` or `label`, an `array<...>`, `chartPoint`, or another type of
your own.

## Create an instance and use its fields

`<Type>.new(...)` creates an instance. Pass the fields in declaration order, or by name. A field you leave out takes its default,
or `na` when it has none.

```lipi
//@lipi=2
indicator("Last swing high", overlay=true)
type Swing {
    float price
    int barIndex = 0
}
static Swing lastHigh = Swing.new(high, bar_index)
if high > lastHigh.price {
    lastHigh := Swing.new(high, bar_index)
}
plot(lastHigh.price, title="Swing high")
```

- Read a field with a dot: `lastHigh.price`.
- Change a field with `:=`, or with a compound assignment: `lastHigh.price := high`, `counter.hits += 1`.
- `static` keeps the instance from one bar to the next, like any other value (see [Values that persist across bars](/scripting/evaluation/persistence)).
- Named arguments work too: `Swing.new(price=high)` leaves `barIndex` at its default.

## Instances are shared, not copied

Assigning an instance to another name does not copy it: both names refer to the same object, so a change through one is seen
through the other. To get an independent object, call `copy`, which copies the fields (a field that holds an array or a drawing
still refers to the same array or drawing).

```lipi-fragment
type Level {
    float price
}
a = Level.new(close)
b = a
c = a.copy()
b.price := 1.0
```

After this, `a.price` is 1.0, because `b` is the same object, and `c.price` is still the close.

## Keep instances in an array

An array can hold a type of your own. Declare it as `array<Swing>` and create it with `array.new<Swing>(0)`. To use a field of an
element, take the element into a variable first: a dot straight after a call is not accepted.

```lipi
//@lipi=2
indicator("Recent swing highs", overlay=true)
type Swing {
    float price
    int barIndex
}
static array<Swing> swings = array.new<Swing>(0)
if high == talib.highest(high, 10) {
    array.push(swings, Swing.new(high, bar_index))
    if array.length(swings) > 5 {
        array.shift(swings)
    }
}
if barstate.islast and array.length(swings) > 0 {
    Swing newest = array.get(swings, array.length(swings) - 1)
    label.new(newest.barIndex, newest.price, text="Last swing")
}
```

Writing `array.get(swings, 0).price` is refused (messages in [Names and conventions](/scripting/language/names-and-conventions)); assign the element first, as above.

## Types in functions

A function may take an instance as a parameter and change its fields; the caller sees the change, because the instance is
shared. A function may also change the fields of an instance declared outside it. What a function may not do is reassign a
variable declared outside it (see [Your own functions](/scripting/language/custom-functions)). `func countIf(Tally t, bool rising)` with
`t.count += 1` in its body is such a function.

## Enums

An `enum` lists named members, one per line. A member may carry a title after `=`; the title is the text the settings show for it
in `input.enum`, not a value. A member without a title shows its own name.

```lipi
//@lipi=2
indicator("Moving average by mode", overlay=true)
enum Speed {
    Fast = "Fast (10)"
    Slow = "Slow (50)"
}
speed = input.enum(Speed.Fast, "Speed")
length = speed == Speed.Fast ? 10 : 50
plot(talib.sma(close, length), title="Average")
```

- Refer to a member as `Speed.Fast`. Members compare with `==` and `!=`, and work as `case` values in a `switch`.
- A name that is not a member is refused: Enum `Speed` has no member `Medium`.
- A member is not a number or a string: pass it to functions that take its enum type, and compare it, but do not give it to
  `str.tostring`.

<!-- /docs/scripting/language/arrays -->

# Arrays

An array is a list of values of one type that can grow and shrink while the script runs. Use one when you need to keep a varying
number of values: the last N prices, the swing points found so far, the labels you have drawn. The `array` namespace holds the
functions (see [array](/scripting/reference/array)); this page shows how they fit together.

## Create an array

`array.new<type>(size, initial)` creates an array of `size` elements, each set to `initial`; both arguments are optional, so
`array.new<float>(0)` is an empty list. The type in angle brackets may be any fundamental type (`int`, `float`, `bool`, `string`,
`color`), a drawing type (`label`, `line`, `box`, `linefill`, `polyline`, `table`), `chartPoint`, or a type of your own.

```lipi-fragment
prices = array.new<float>(0)
names = array.new<string>(3, "none")
marks = array.new<label>(0)
fromValues = array.from(1, 2, 3)
```

`array.new_float(0)`, `array.new_int(...)`, `array.new_label(...)` and their siblings are the same as the angle-bracket form, except that
`array.new_bool(3)` holds `false` where `array.new<bool>(3)` holds `na`; every other type holds `na` until set. To
declare the type of a variable, write `array<float>`:

```lipi-fragment
array<float> window = array.new<float>(0)
```

## Add, read and remove

- `array.push(a, x)` adds at the end; `array.unshift(a, x)` at the start.
- `array.get(a, i)` reads the element at index `i`; the first element is index 0 and the last is `array.length(a) - 1`.
  An index outside that range, including a negative one, stops the script when it runs with an error from `array.get`.
- `array.set(a, i, x)` replaces an element.
- `array.pop(a)` removes and returns the last element; `array.shift(a)` the first.
- `array.length(a)` is the number of elements. There is no `array.size`.
- An array holds at most 10,000 elements; growing it past that stops the script when it runs.

The functions can also be called on the array itself: `a.push(close)` is `array.push(a, close)`, and `a.length()` is
`array.length(a)`. A name the array namespace does not have is refused either way, for example `a.size()`: Could not find any
type function `size` for `a`.

`a[1]` is not the element at index 1: `[]` on an array is the history operator, so `a[1]` is the array as it was on the previous
bar. Use `array.get(a, 1)` for an element.

## Keep an array across bars

A plain declaration creates a new array on every bar. Declare it `static` to create it once and keep adding to it:

```lipi
//@lipi=2
indicator("Average of the last 5 closes")
static array<float> window = array.new<float>(0)
array.push(window, close)
if array.length(window) > 5 {
    array.shift(window)
}
plot(array.avg(window), title="Average of last 5")
```

## Loop over an array

`for x in a` visits each element in order; `a` must be an array variable, not an expression. Changing `x` inside the loop does
not change the element: use `array.set` for that. Prefer `for x in a` to a counted loop over the indexes: a counted loop does not
run its body when the start and the end are equal (see [Loops](/scripting/language/repetition)), so `for i = 0 to
array.length(a) - 1` skips a one-element array.

```lipi
//@lipi=2
indicator("Sum by loop")
static array<float> moves = array.new<float>(0)
array.push(moves, close - open)
float total = 0
for m in moves {
    total += m
}
plot(total, title="Sum of moves")
```

## Arrays of drawings

An array of drawings lets a script keep a fixed number of them and delete the oldest:

```lipi
//@lipi=2
indicator("Last three marks", overlay=true)
static array<label> marks = array.new<label>(0)
if barstate.isconfirmed and close > open {
    array.push(marks, label.new(bar_index, high, "Up"))
    if array.length(marks) > 3 {
        label.delete(array.shift(marks))
    }
}
```

For arrays of your own types, see [Custom types and enums](/scripting/language/custom-types).

## Arrays are shared, not copied

Assigning an array to another name gives a second name for the same array: `b = a` and then `array.set(b, 0, x)` changes `a`
too. `array.copy(a)` returns an independent array with the same elements.

<!-- /docs/scripting/language/names-and-conventions -->

# Names and conventions

If you know another scripting language, some of what you type from habit does not exist in Lipi. Each row was compiled; the right
column is the editor's message for the form on the left.

| You may expect | Lipi has | The compiler says to the other form |
|---|---|---|
| Transparency 0 to 100: `color.new(c, 50)`, `transp=50` | Opacity 0 to 1: `color.new(c, 0.5)`, argument `alpha` | Warning: opacity 50 is outside 0–1; 1 is solid. For `transp=`, two errors: The `color.new()` function is missing required argument(s): `alpha`. and The `color.new()` function does not accept a named argument `transp`. |
| `array.size(a)`, `a.size()` | `array.length(a)`, `a.length()` | Namespace `array` has no function `size`. Did you mean `slice()`? and Could not find any type function `size` for `a`. |
| `chart.point.now(...)` | `chartPoint.now(...)`, `chartPoint.new(...)` | Namespace `chart` has no variable `point`. |
| `var x = 0` | `static x = 0` | `var` is not a valid type in variable declaration. |
| `int n = len / 2` | `int n = math.floor(len / 2)` | Declared type `int` is not compatible with assigned type `input float`. Use math.floor(), math.round(), or math.ceil() if you need a whole number. |
| A variable called `step` | another name; `step` stays valid as a named argument | no viable alternative at input 'intstep' |
| `timeframe.period` | `interval.interval`, `interval.isdaily`, `interval.multiplier` | No variable with name `timeframe` found. |
| `array.get(a, 0).price` | `P p = array.get(a, 0)` then `p.price` | inside a call: mismatched input '.' expecting ')'; as a statement: extraneous input '.' expecting {<EOF>, NEWLINE} |
| A function that sets a global variable | return the value and assign it at the top level | Cannot modify global variable `g` in function. |
| `force_overlay=true` on `line.new` | `forceOverlay=true` on `line.new` only; other calls use `force_overlay` | The `line.new()` function does not accept a named argument `force_overlay`. Did you mean `forceOverlay`? |
| `x ^ 2` | `math.pow(x, 2)` | extraneous input '^' expecting {<EOF>, NEWLINE} |
| `a = 1; b = 2` | one statement per line | extraneous input ';' expecting {<EOF>, NEWLINE} |
| `x = if c { ... }` | `x = c ? a : b`, or assign inside an `if` statement | extraneous input '{' expecting {<EOF>, NEWLINE} |
| `close == na` | `na(close)` | Warning: Do not use the `na` variable to compare other values to 'na', use the `na()` function instead |
| `plot(close, style=plot.style_line)`, `hline.style_dashed` | `style=plotStyle.line`, `hlineStyle.dashed` | No variable with name `plot` found. (`hline` likewise) |
| `color.pink`, any other colour name | the 17 constants (`color.lime`, ...), `color.rgb(255, 192, 203)` or `#FFC0CB` | Namespace `color` has no variable `pink`. Did you mean `lime`? |
| `str.format("{0}", x)` | `"text " + str.tostring(x)` | Namespace `str` has no function `format`. |
| `request.security(...)` | nothing (no other symbol or interval) | No variable with name `request` found. |

## ta and talib

`ta` and `talib` are two names for one namespace with the same 62 functions: `ta.sma` is `talib.sma`. Messages always say `talib`, and so
do the examples here.

## Rules for names

- A name is ASCII letters, digits and `_`, not starting with a digit, and case-sensitive: `Close` is a new variable, `CLOSE` does not exist.
- Reserved words, which no variable or parameter may be called: `static intra func type enum def if else for while switch break continue
  return to step in case default and or not true false na const simple series`.
- A built-in variable (`close`, `volume`, `bar_index`, ...) cannot be redeclared or assigned: `` `close` is a built-in name and cannot be redeclared. ``
- A variable may be named like a namespace (`array`, `math`) or a function; the compiler warns about a namespace name. Avoid both.

<!-- /docs/scripting/market-data/price-and-volume -->

# Price and volume

The bar being evaluated is available through built-in series; nothing is imported or requested.

| Name | Type | Value |
|---|---|---|
| `open`, `high`, `low`, `close`, `volume` | series float | The bar's prices and volume. |
| `hl2`, `hlc3`, `ohlc4` | series float | (high + low) / 2; (high + low + close) / 3; (open + high + low + close) / 4. |
| `hlcc4` | series float | (high + low + 2 x close) / 4. |
| `bar_index` | series int | Index of the bar, 0 for the first. |
| `last_bar_index` | series int | Index of the last bar, including a forming one. |

These names cannot be redeclared. For `time`, `year` and the rest see [Sessions and intervals](/scripting/market-data/sessions-and-intervals).

`close[1]` is the previous close and `close[0]` the current one; the index may be a series expression. History reaches back 500 bars, and a larger index stops the script when it runs (see [Limits](/scripting/distribution/limits)).

`input.source` lets the chart user pick the price. Its default must be one of `open`, `high`, `low`, `close`, `hl2`, `hlc3`, `ohlc4`, `hlcc4`; `volume` is refused: `volume` is not a valid source variable. Expected: open/high/low/close/hl2/hlc3/ohlc4/hlcc4.

```lipi
//@lipi=2
indicator("Average of a chosen price", overlay=true)
src = input.source(close, "Source")
plot(talib.sma(src, 20), title="Average")
```

`chart.is_standard` is true on candles, bars, line and area charts; `chart.is_heikinashi`, `is_renko`, `is_kagi`, `is_linebreak`, `is_pnf`, `is_range` flag the other types.

<!-- /docs/scripting/market-data/orderflow -->

# Orderflow: buying, selling and delta

The `orderflow` namespace gives each bar's trade counts and buying and selling volume, from the bar's footprint data (its trades grouped by price and by buy or sell side). All ten values and the one function are series ints.

| Name | Value for the bar |
|---|---|
| `orderflow.trades` | All trades. |
| `orderflow.buy`, `orderflow.sell` | Number of buy trades, number of sell trades (counts, not volume). |
| `orderflow.buyvolume`, `orderflow.sellvolume` | Volume bought, volume sold. |
| `orderflow.delta` | Delta at the bar's close: buy volume minus sell volume. |
| `orderflow.maxdelta`, `orderflow.mindelta` | Highest and lowest delta reached while the bar formed. |
| `orderflow.cothigh`, `orderflow.cotlow` | Net buying (buy minus sell volume) since the bar last traded at its high, and at its low. |
| `orderflow.cvd()` | Cumulative delta: each bar's `orderflow.delta` added to a running total that restarts from 0 on the first bar of every session (`session.isfirst`). A bar whose delta is `na` leaves the total unchanged. It takes no arguments. |

`orderflow.*` values exist only on bars with footprint data. A bar without it has all ten as `na`; no value carries over from an earlier bar. So a script can test `na(orderflow.delta)` and run on every instrument (see [Data availability by market](/scripting/market-data/availability)).

```lipi
//@lipi=2
indicator("Delta and session cumulative delta")
plot(orderflow.delta, title="Delta", style=plotStyle.histogram, color=orderflow.delta >= 0 ? color.green : color.red)
plot(orderflow.cvd(), title="Session CVD")
```

<!-- /docs/scripting/market-data/open-interest -->

# Open interest

`oi` is a series float holding the open interest of the bar. It is the only open-interest name: there is no `oi` namespace and no other function.

```lipi
//@lipi=2
indicator("Open interest change")
plot(oi - oi[1], title="Change in open interest", style=plotStyle.histogram)
```

Where the instrument has no open-interest data, the bar carries none and `oi` is 0, not `na`. Test `oi > 0` rather than `na(oi)` to find out whether there is data.

<!-- /docs/scripting/market-data/sessions-and-intervals -->

# Sessions and intervals

Times are integers in milliseconds since the Unix epoch.

| Name | Value |
|---|---|
| `time` | Opening time of the bar. |
| `time_close` | Closing time: opening time plus one interval. |
| `time_sessionday` | The trading day of the bar. |
| `last_bar_time` | Opening time of the chart's last bar. |
| `timenow` | The wall clock when the script ran, not a bar time. |

There is no `time.now()` and no `timeframe` namespace (`timeframe.period` fails with No variable with name `timeframe` found): use `interval.interval`.

## Parts of a time

`year`, `month`, `dayofmonth`, `dayofweek`, `hour`, `minute`, `second` are series ints for the current bar. Each is also a function of a time and an optional zone: `hour(time, "America/New_York")`. The zone is an IANA name; the default is the exchange's (`syminfo.timezone`). A name it cannot load, `"UTC-5"` included, gives 0. `weekofyear(time)` exists only as a function. `dayofweek` counts Sunday as 1 to Saturday as 7; compare with `dayofweek.sunday` ... `dayofweek.saturday`.

`timestamp(2024, 3, 1)` builds a time (hour, minute, second optional; the exchange's zone), `timestamp("UTC", 2024, 3, 1, 9, 30, 0)` names the zone (an IANA name, or an offset such as `"UTC-5"` or `"GMT+0530"`, as in `time` and `str.format_time`), and `timestamp("2024-03-01")` reads a date string (UTC without a zone; `na` if unreadable). When the script is added to the chart `timestamp()` is `na`, so it cannot be the default of `input.time`; give milliseconds.

## Testing a session

`time(interval, session)` returns the opening time of the `interval` period that holds the bar, or `na` when that opening time is outside `session`. Periods are cut on the clock (a 1-hour period holding a 09:30 bar opens at 09:00), so `time("1D", "0930-1600")` is always `na`. A session is `"0930-1600"`, with ranges joined by commas (`"1000-1100,1400-1500"`) and optionally `:` and days, Sunday as 1 (`"0930-1600:23456"`). A range that ends before it starts wraps past midnight; `"0000-0000"` is the whole day. Times are read in the exchange's zone; a `timezone` argument between `session` and `bars_back` changes that. `time_close` takes the same arguments.

```lipi
//@lipi=2
indicator("Volume in the window today")
inWindow = not na(time(interval.interval, "0930-1600"))
static float total = 0.0
if interval.change("1D") {
    total := 0.0
}
if inWindow {
    total += volume
}
plot(total, title="Window volume")
```

`session.isfirst` is true on a session's first bar; `session.date` is its date string. There is no `session.islast`: Namespace `session` has no variable `islast`. Did you mean `isfirst`?

## The chart's interval

An interval string is a number and a unit: `s`, `m`, `h`, `D`, `W`, `M` (`"30s"`, `"5m"`, `"1h"`, `"1D"`).

- `interval.interval` is the chart's interval string, `interval.multiplier` its number, `interval.timeframe_minutes` its length in minutes.
- `interval.isintraday`, `isseconds`, `isminutes`, `ishourly`, `isdaily`, `isweekly`, `ismonthly`, `iseod` are simple bools.
- `interval.change("1D")` is true on the first bar of each new day (or other period).
- `interval.in_seconds("1D")` is 86400 (no argument: the chart's interval); `interval.from_seconds(86400)` is `"1D"`. A month is 2628003 seconds; tick and range intervals give `na`.

<!-- /docs/scripting/market-data/instrument -->

# Instrument properties

The `syminfo` namespace describes the instrument the script is running on. Every value is the same on every bar.

| Name | Type | Meaning |
|---|---|---|
| `syminfo.ticker` | string | Exchange, segment and symbol joined by colons: `exchange:segment:symbol`. |
| `syminfo.symbol` | string | The symbol alone. |
| `syminfo.root` | string | The symbol; for futures and options, the root symbol of the contract. |
| `syminfo.exchange` | string | The exchange. |
| `syminfo.segment` | string | The exchange segment. |
| `syminfo.asset_type` | string | The asset type. |
| `syminfo.currency` | string | The quote currency. |
| `syminfo.timezone` | string | The exchange's time zone: pass it to `hour(time, syminfo.timezone)` and the other date functions. |
| `syminfo.isindex` | bool | True for an index. |
| `syminfo.minmove` | float | The tick size, the smallest price step. `strategy.exit` measures `profit` and `loss` in ticks of this size. |
| `syminfo.pricescale` | int | The instrument's maximum tick precision. |
| `syminfo.mintick` | float | `syminfo.minmove` divided by `syminfo.pricescale`. |
| `syminfo.sizescale` | int | The instrument's maximum volume precision. |
| `syminfo.mincontract` | int | The contract size. |

These fourteen are the whole namespace. `syminfo.tickerid` fails with Namespace `syminfo` has no variable `tickerid`. Did you mean `ticker`? There is no `syminfo.type` either (`type` is a keyword: no viable alternative at input 'plot(syminfo.type'); the asset type is `syminfo.asset_type`. To convert a price distance to ticks, divide by `syminfo.minmove`, not by `syminfo.mintick`. Another instrument's data cannot be read (see [Data availability by market](/scripting/market-data/availability)).

```lipi
//@lipi=2
indicator("Bar range in ticks")
plot((high - low) / syminfo.minmove, title="Range in ticks")
```

<!-- /docs/scripting/market-data/availability -->

# Data availability by market

A script reads the bars of the chart it runs on, and nothing else. This page lists what is there and how a script finds out that an instrument lacks some of it.

## What a script can read

The bars at the chart's interval (`open`, `high`, `low`, `close`, `volume`), the `syminfo` and `interval` namespaces, open interest (`oi`) and the `orderflow` series.

## What a script cannot read

There is no request for another instrument or another interval: no `request` namespace exists, and `request.security(...)` is refused with No variable with name `request` found. A script cannot read a second symbol's price, nor the same symbol at a higher interval. `timeframe.*` does not exist either. Nothing in the language or the compiler states which markets carry open-interest or footprint data, so the manual does not either.

## When an instrument lacks the data

| Data | Where the instrument has none |
|---|---|
| `orderflow.*` | `na` on every bar. Test with `na(orderflow.delta)`. |
| `oi` | 0 on every bar. Test with `oi > 0`. |

Write for both cases and the same script runs on every instrument:

```lipi
//@lipi=2
indicator("Delta where it exists")
hasFlow = not na(orderflow.delta)
plot(hasFlow ? orderflow.delta : na, title="Delta", style=plotStyle.histogram)
```

<!-- /docs/scripting/chart-output/plotting -->

# Plotting

`plot` draws one value per bar. Its relatives mark bars (`plotshape`, `plotchar`, `plotarrow`), draw candles or bars of your own
(`plotcandle`, `plotbar`) or draw a level (`hline`). For anything that is not one value on every bar, see
[Plots or drawings](/scripting/chart-output/plots-or-drawings).

## Top level only

Every one of these calls, and `fill`, `bgcolor`, `barcolor` and `alertcondition`, must stand at the top level of the script: not in
an `if`, a loop, a `switch` or a function of yours. The editor refuses it:

```lipi-invalid
//@lipi=2
indicator("Conditional plot")
if close > open {
    plot(close)
}
```

The compiler says: `plot()` must be called in the global scope.

Put the condition in the arguments instead. A plotted `na` leaves a gap, and a `na` colour draws nothing:

```lipi
//@lipi=2
indicator("Up closes", overlay=true)
plot(close > open ? close : na, title="Up closes", style=plotStyle.cross)
```

## plot

`plot(series, title, color, linewidth, style, trackprice, histbase, offset, force_overlay, display, format)`. Only `series` is
required.

| Argument | Rule |
|---|---|
| `title` | `const string`: a literal or a constant expression, never text built from data |
| `color` | any `color`, may change on every bar; `na` draws nothing |
| `linewidth`, `style`, `histbase`, `offset` | `input` qualifier: fixed for the run, not computed per bar |
| `style` | `plotStyle.line`, `linebr`, `area`, `areabr`, `smoothedArea`, `stepLine`, `stepLinebr`, `stepArea`, `stepAreabr`, `bar`, `histogram`, `scatter`, `triangular`, `cross` |
| `force_overlay` | `const bool`: draw this plot on the price pane although the script is not an overlay |
| `trackprice` | accepted and has no effect |

A computed `linewidth` is refused (`An argument of `series int` type was used but a `input int` is expected.`). To vary a plot's look by bar, vary its `color`, or plot twice with different arguments.

```lipi
//@lipi=2
indicator("Close and average", overlay=true)
avg = talib.sma(close, 20)
plot(close, title="Close", color=color.gray)
plot(avg, title="Average", color=close > avg ? color.green : color.red, linewidth=2)
```

`plot` returns a plot value that [`fill`](/scripting/chart-output/fills-and-levels) accepts.

## Where a plot is shown: display and format

`display` takes `display.none`, `pane`, `data_window`, `price_scale`, `status_line` or `all` (the default); add constants with `+`:
`display=display.pane + display.price_scale`. It is an argument of every call on this page and of `fill`, `bgcolor`, `barcolor` and
the inputs; the terminal decides what each place shows. `fill`, `barcolor` and `bgcolor` take only `display.none` and `display.all`
(see [Fills and levels](/scripting/chart-output/fills-and-levels)).

`format` on `plot`, `plotshape`, `plotchar`, `plotarrow` and `hline` takes `format.price`, `format.percent` or `format.volume`. The
editor accepts `format.mintick` and `format.inherit`; adding the script to the chart refuses them:

```lipi-invalid
//@lipi=2
indicator("Format")
plot(close, format=format.mintick)
```

The compiler says (when added to the chart): The `format` argument only accepts format.price, format.percent, or format.volume. Got `format.mintick`.

## Marks on bars

- `plotshape(series, title, shape, location, color, offset, text, textcolor, size, force_overlay, display, format)` draws a shape on
  each bar where the `bool` series is true. `shape` is `shape.xcross`, `cross`, `triangleup`, `triangledown`, `flag`, `circle`,
  `arrowup`, `arrowdown`, `labelup`, `labeldown`, `square` or `diamond`; `location` is `location.abovebar`, `belowbar`, `top`,
  `bottom` or `absolute`; `size` is `size.auto`, `tiny`, `small`, `normal`, `large` or `huge`. Given a `float` series instead, it
  draws at that price, and a `na` draws nothing.
- `plotchar` is the same with `char`, one character (`const string`) instead of `shape`; a longer string is cut to its first
  character.
- `plotarrow(series, title, colorup, colordown, offset, minheight, maxheight, force_overlay, display, format)` draws an arrow up for a
  positive value and down for a negative one, sized by the value.
- `text` is a `const string`; see [Text and markers](/scripting/chart-output/text-and-markers).

```lipi
//@lipi=2
indicator("Marks", overlay=true)
plotshape(close > open and volume > talib.sma(volume, 20), title="Strong up", shape=shape.triangleup, location=location.belowbar, color=color.green, size=size.small)
plotarrow(close - open, colorup=color.green, colordown=color.red)
```

## Your own bars and a level

`plotcandle(open, high, low, close, title, color, wickcolor, bordercolor, force_overlay, display)` and `plotbar(open, high, low,
close, title, color, display, force_overlay)` draw bars from four series; all four are required. `hline(price, title, color,
linewidth, style, display, format)` draws a horizontal line; `price` is an `input` value (see
[Fills and levels](/scripting/chart-output/fills-and-levels)): `plotcandle(talib.sma(open, 3), talib.sma(high, 3), talib.sma(low, 3), talib.sma(close, 3))`.

<!-- /docs/scripting/chart-output/colour -->

# Colour and transparency

A color is a value of type `color`. You write one as a constant, a hex literal or a call, and every drawing and plot takes one.

## Constants and hex

The constants are `color.aqua`, `black`, `blue`, `fuchsia`, `gray`, `green`, `lime`, `maroon`, `navy`, `olive`, `orange`, `purple`,
`red`, `silver`, `teal`, `white` and `yellow`. A plot without a `color` is `#483D8B`.

A hex literal is `#RRGGBB` or `#RRGGBBAA`, where the last pair is the alpha: `FF` is solid, `00` invisible. `#F00` (three digits) is
not a color:

```lipi-invalid
//@lipi=2
indicator("Short hex")
plot(close, color=#F00)
```

The compiler says: token recognition error at: '#F00)'. Write `#FF0000`.

## Opacity

`color.new(color, alpha)` returns the color with a new opacity. **`alpha` runs from 0 to 1, and 1 is solid.** There is no
`transp` argument and no 0 to 100 scale. A value outside 0..1 is clamped when the script runs; a literal or `const` one also gives a
warning when you check the script, for example `color.new(color.red, 80)`: opacity 80 is outside 0–1; 1 is solid.

`color.rgb(r, g, b, a)` builds a color from integers 0 to 255 for `r`, `g`, `b` and, optionally, an opacity `a` from 0 to 1
(default solid). A literal component outside 0..255 warns: component r value 300 is outside 0–255.

```lipi
//@lipi=2
indicator("Opacity", overlay=true)
plot(close, title="Close", color=color.new(color.blue, 0.3), linewidth=3)
plot(open, title="Open", color=color.rgb(255, 165, 0, 0.6))
plot(hl2, title="Midpoint", color=color.new(#00FF0080, 0.5))
```

## Colors that change by bar

A color argument that is `series` may differ on every bar, so a condition decides the color:

```lipi
//@lipi=2
indicator("Trend color", overlay=true)
avg = talib.sma(close, 20)
plot(avg, title="Average", color=close > avg ? color.green : color.red)
bgcolor(close > open ? color.new(color.green, 0.9) : na)
```

`na` as a color means no color. The opacity of `color.new` may itself be a series.

## Gradients

`color.from_gradient(value, bottom_value, top_value, bottom_color, top_color)` blends the two colors by where `value` lies between
the two bounds (clamped to them). It returns `na` when the bounds are equal. All five arguments are required.

```lipi
//@lipi=2
indicator("RSI gradient")
rsi = talib.rsi(close, 14)
plot(rsi, title="RSI", color=color.from_gradient(rsi, 30, 70, color.red, color.green), linewidth=2)
```

## Reading a color

`color.r(c)`, `color.g(c)` and `color.b(c)` return 0 to 255; `color.a(c)` returns the opacity from 0 to 1.

## Matching the chart's theme

`chart.bg_color` is the chart's background and `chart.fg_color` a color that contrasts with it, so text and lines stay readable on a light or a dark chart. Both are `input` colors: use them where a fixed value is required, such as `plot(color=...)`.

<!-- /docs/scripting/chart-output/fills-and-levels -->

# Fills and levels

`hline` draws a horizontal line at a price that is fixed for the whole run. `fill` shades the space between two plots or two
levels. Both stand at the top level of the script (see [Plotting](/scripting/chart-output/plotting)).

## Levels

`hline(price, title, color, linewidth, style, display, format)`: `price` is required and is an `input` value, so a number, an
`input.*` result or a constant, never a series. `color` is `input` too, so a level cannot change color by bar. `style` is
`hlineStyle.solid`, `dashed` or `dotted`. `hline` has no `force_overlay`.

```lipi-invalid
//@lipi=2
indicator("Moving level")
hline(close)
```

The compiler says: Cannot call `hline` with argument `price`=`close`. An argument of `series float` type was used but a `input float` is expected.

A line that follows the data is a `plot`, or a `line` drawing (see [Plots or drawings](/scripting/chart-output/plots-or-drawings)).
`hline` returns an hline value that `fill` accepts. For a level that starts at a bar and runs on, draw `line.new(..., extend=extend.right)`, and shade between two such lines with `linefill.new` (see [Lines, labels, boxes and polylines](/scripting/chart-output/drawings)).

## Fill between two plots

Keep both `plot` results in variables and pass them to `fill`. The arguments are `fill(p1, p2, title, color, fillgaps, display)`.

```lipi
//@lipi=2
indicator("Range band")
top = plot(high, title="High", color=color.new(color.blue, 0.8))
bottom = plot(low, title="Low", color=color.new(color.blue, 0.8))
fill(top, bottom, title="Range", color=color.new(color.blue, 0.85))
```

The `color` may be a series, so the band changes color by bar. A fill keeps a plot offset only when both plots have the same one. It follows its plots into their pane and has no `force_overlay`.

## Fill between two levels

The two-level form puts the color third and the title fourth: `fill(h1, h2, color, title, fillgaps, display)`. Name the arguments
and the order stops mattering.

```lipi
//@lipi=2
indicator("Overbought zone")
rsi = talib.rsi(close, 14)
plot(rsi, title="RSI")
upper = hline(70, title="Upper", color=color.red, style=hlineStyle.dashed)
lower = hline(30, title="Lower", color=color.green, style=hlineStyle.dashed)
fill(upper, lower, color=color.new(color.gray, 0.9), title="Band")
```

## Gradient fills

Both forms have a gradient version: `fill(p1, p2, top_value, bottom_value, top_color, bottom_color, title, display, fillgaps,
editable)` for plots (the first two names are `plot1` and `plot2` if you name them) and the same with `h1`, `h2` for levels. The
four of `top_value`, `bottom_value`, `top_color` and `bottom_color` are required; the values are numbers, the colors are series.
`editable` (default `true`) is stored with the fill. The terminal does the shading.

```lipi
//@lipi=2
indicator("Gradient band")
p = plot(high, title="High")
q = plot(low, title="Low")
fill(plot1=p, plot2=q, top_value=high, bottom_value=low, top_color=color.new(color.green, 0.6), bottom_color=color.new(color.red, 0.6))
```

## What fill does not accept

`fill` joins plot or hline results, never series and never one of each:

```lipi-invalid
//@lipi=2
indicator("Mixed fill")
p = plot(close)
h = hline(50)
fill(p, h)
```

The compiler says: Cannot call `fill` with argument `h1`=`p`. An argument of `series plot` type was used but a `series hline` is expected. For a band between a plot and a price, plot the price with `plot(50)`.

`display` on `fill` takes only `display.none` and `display.all`. The editor accepts `display.pane`; adding the script to the chart
refuses it with: `fill()` display argument only supports display.none and display.all.

<!-- /docs/scripting/chart-output/bars-and-background -->

# Bar colouring and background

`barcolor` recolors the price bars; `bgcolor` shades the background behind a bar. Neither draws a value. Both stand at the top level
and take their condition in the color: a color of `na` means no change.

## barcolor and bgcolor

- `barcolor(color, title, offset, display)`
- `bgcolor(color, title, offset, force_overlay, display)`

`color` may be a series. `title` is a `const string`, `offset` an `input int`. `barcolor` has no `force_overlay`.

```lipi
//@lipi=2
indicator("Trend shading", overlay=true)
avg = talib.sma(close, 20)
up = close > avg
barcolor(up ? color.green : color.red, title="Bars")
bgcolor(up ? color.new(color.green, 0.92) : na, title="Uptrend")
```

A gradient shades the background by a value (see [Colour](/scripting/chart-output/colour)):

```lipi-fragment
rsi = talib.rsi(close, 14)
bgcolor(color.from_gradient(rsi, 30, 70, color.new(color.red, 0.8), color.new(color.green, 0.8)))
```

## display accepts only all and none

`display` takes only `display.none` and `display.all` on both. The editor accepts other constants; adding the script to the chart
refuses them:

```lipi-invalid
//@lipi=2
indicator("Pane only")
bgcolor(color.red, display=display.pane)
```

The compiler says (when added to the chart): `bgcolor()` display argument only supports display.none and display.all. For `barcolor` the message names `barcolor()`.

To own the whole bar rather than recolor it, use `plotcandle` (see [Plotting](/scripting/chart-output/plotting)).

<!-- /docs/scripting/chart-output/text-and-markers -->

# Text and markers

`plotshape` and `plotchar` mark the bars where a condition is true and may carry a fixed text. Text that depends on the data (a
price, a count) is a label.

## Fixed text on a mark

`text` on `plotshape` and `plotchar` is a `const string`: the same text on every mark. `textcolor` may change by bar; `size` and
`location` are `input` values. `plotchar` draws one `char` (a longer string is cut to its first character).

```lipi
//@lipi=2
indicator("Signals", overlay=true)
avg = talib.sma(close, 20)
plotshape(talib.crossover(close, avg), title="Buy", text="Buy", textcolor=color.green, location=location.belowbar, color=color.green, shape=shape.labelup, size=size.small)
plotchar(talib.crossunder(close, avg), title="Sell", char="S", location=location.abovebar, color=color.red)
```

Text built from data is refused:

```lipi-invalid
//@lipi=2
indicator("Price on mark", overlay=true)
plotshape(close > open, text=str.tostring(close))
```

The compiler says: Cannot call `plotshape` with argument `text`=`str.tostring(close)`. An argument of `series string` type was used but a `const string` is expected. The same holds for `title`, and for `char` on `plotchar`.

## Text from data: label.new

`label.new(x, y, text, xloc, yloc, color, style, textcolor, size, textalign, tooltip, text_font_family, force_overlay, text_formatting)`
puts a label at bar `x` and price `y`, with any string. A label is a drawing: it may be created inside `if`, loops and functions,
and the oldest labels are removed past `max_labels_count` (see [Lines, labels, boxes and polylines](/scripting/chart-output/drawings)).

```lipi
//@lipi=2
indicator("Volume labels", overlay=true)
if close > open and volume > talib.sma(volume, 20) * 2 {
    label.new(bar_index, low, "Vol " + str.tostring(volume), style=label.style_label_up, color=color.green, textcolor=color.white, size=size.small)
}
```

Label text is limited to 999 characters, and `yloc` is `yloc.price`, `yloc.abovebar` or `yloc.belowbar`. For a grid of values, see [Tables](/scripting/chart-output/tables).

<!-- /docs/scripting/chart-output/drawings -->

# Lines, labels, boxes and polylines

A drawing is an object placed on the chart: a `line`, `label`, `box`, `polyline` or `linefill` (and a [`table`](/scripting/chart-output/tables)).
Unlike a plot, a drawing can be created on some bars only, inside `if`, loops and functions, at positions you compute.

## Create

| Call | Draws |
|---|---|
| `line.new(x1, y1, x2, y2, xloc, extend, color, style, width, forceOverlay)` | a line segment |
| `label.new(x, y, text, xloc, yloc, color, style, textcolor, size, textalign, tooltip, ...)` | text at a point |
| `box.new(left, top, right, bottom, border_color, border_width, border_style, extend, xloc, bgcolor, text, ...)` | a rectangle |
| `polyline.new(points, curved, closed, xloc, line_color, fill_color, line_style, line_width, force_overlay)` | a path through an `array<chartPoint>` |
| `linefill.new(line1, line2, color)` | the area between two lines |

`x` values are bar indexes (`bar_index`) by default, or times in milliseconds with `xloc=xloc.bar_time`; `y` values are prices.
`extend` is `extend.none`, `left`, `right` or `both`. Styles are constants: `line.style_solid`, `dashed`, `dotted`, `arrow_left`,
`arrow_right`, `arrow_both`; `label.style_label_up`, `label_down`, `label_left`, `label_right`, `label_center`, `arrowup`,
`arrowdown`, `circle`, `square`, `diamond`, `flag`, `cross` and others.

```lipi
//@lipi=2
indicator("Swing high markers", overlay=true)
if high == talib.highest(high, 10) {
    line.new(bar_index, high, bar_index + 10, high, color=color.red, style=line.style_dashed)
    label.new(bar_index, high, str.tostring(high), style=label.style_label_down, textcolor=color.white, color=color.red)
}
```

The overlay argument is `force_overlay` on every call except `line.new`, which spells it `forceOverlay`. The other spelling is refused (The `line.new()` function does not accept a named argument `force_overlay`.).

## Change and delete

Lines, labels and boxes have `set_*` functions (`line.set_xy2`, `label.set_text`, `label.set_style`, `box.set_right`, `line.set_color`, ...) and `get_*` readers
(`line.get_y1`, `label.get_x`, ...); a linefill has `linefill.set_color`. Call them as functions or as methods: `line.set_color(l, c)` and `l.set_color(c)` are the same,
except that `line.set_xloc(l, xloc.bar_time, time, time + 1)` is a function only: the method `l.set_xloc(...)` takes just the `xloc`.
A polyline has no setters or getters: delete it and create a new one. `delete` removes any drawing, and `copy` (`line`, `label` and `box`) makes a new one with the same properties. There is no field
access: `l.x` is refused.

To update one drawing on later bars, keep it in a `static` variable, so it survives from bar to bar:

```lipi
//@lipi=2
indicator("Highest high so far", overlay=true)
static line hiLine = line.new(bar_index, high, bar_index + 1, high, extend=extend.right, color=color.orange)
if high > line.get_y1(hiLine) {
    line.set_xy1(hiLine, bar_index, high)
    line.set_xy2(hiLine, bar_index + 1, high)
}
```

To keep many, push them into an `array<line>` (or `label`, `box`) and delete the oldest, as in [Arrays](/scripting/language/arrays).

`linefill.new` shades between two lines; keep the `talib` calls outside the `if`:

```lipi
//@lipi=2
indicator("Range shading", overlay=true)
hi = talib.highest(high, 20)
lo = talib.lowest(low, 20)
if barstate.islast {
    top = line.new(bar_index - 19, hi, bar_index, hi, color=color.red)
    bottom = line.new(bar_index - 19, lo, bar_index, lo, color=color.green)
    linefill.new(top, bottom, color.new(color.blue, 0.85))
}
```

## Chart points and polylines

A `chartPoint` holds a time, a bar index and a price. Build one with `chartPoint.from_index(index, price)`,
`chartPoint.from_time(time, price)`, `chartPoint.new(time, index, price)` or `chartPoint.now(price)`. `line.new`, `box.new` and
`label.set_point` have forms that take points. `polyline.new` takes an array of at most 1000 of them (more, or none, gives `na`); fill it with `array.push`, because
`array.from` does not accept chart points.

```lipi
//@lipi=2
indicator("Up-close path", overlay=true)
static array<chartPoint> pts = array.new<chartPoint>(0)
if close > open {
    array.push(pts, chartPoint.from_index(bar_index, close))
    if array.length(pts) > 500 {
        array.shift(pts)
    }
}
if barstate.islast and array.length(pts) > 1 {
    polyline.new(pts, line_color=color.blue)
}
```

## How many a script keeps

`indicator()` and `strategy()` take `max_lines_count`, `max_labels_count`, `max_boxes_count` and `max_polylines_count` (`const`
integers): 50 of each kind by default, 500 at most (100 for polylines; see [Limits](/scripting/distribution/limits)). Linefills stay at 50 and tables at 9.

When a kind goes a few above its limit, the oldest drawings of that kind are deleted until the limit is met. A line, label, box or
linefill that a `static` variable holds directly is never deleted this way; drawings held only in an array, and polylines, are, so keep
an array no longer than the limit. Raise the limit when the script needs more drawings on the chart: `indicator("Many levels", overlay=true, max_lines_count=500)`.

<!-- /docs/scripting/chart-output/tables -->

# Tables

A table is a fixed grid of text cells pinned to a corner or edge of the chart, not to a price or bar. Use one for a summary: a
few statistics, a legend, a status.

## Create and fill

`table.new(position, columns, rows, bgcolor, frame_color, frame_width, border_color, border_width, force_overlay)` creates the table.
`position` is `position.top_left`, `top_center`, `top_right`, `middle_left`, `middle_center`, `middle_right`, `bottom_left`,
`bottom_center` or `bottom_right`. `table.cell(table, column, row, text, width, height, textcolor, texthalign, textvalign, size,
bgcolor, tooltip, ...)` sets a cell; columns and rows count from 0. A cell outside the table is ignored.

Create the table once, in a `static` variable, and fill it only on the last bar, where the values are final:

```lipi
//@lipi=2
indicator("Range table", overlay=true)
static table t = table.new(position.top_right, 2, 3, bgcolor=color.new(color.gray, 0.8), border_width=1)
if barstate.islast {
    table.cell(t, 0, 0, "High")
    table.cell(t, 1, 0, str.tostring(high), textcolor=color.green)
    table.cell(t, 0, 1, "Low")
    table.cell(t, 1, 1, str.tostring(low), textcolor=color.red)
    table.cell(t, 0, 2, "Volume")
    table.cell(t, 1, 2, str.tostring(volume))
}
```

Calling `table.cell` again on the same cell replaces its content.

## Change a table

- Cells: `table.cell_set_text`, `cell_set_bgcolor`, `cell_set_text_color`, `cell_set_text_size`, `cell_set_text_halign`,
  `cell_set_text_valign`, `cell_set_width`, `cell_set_height`, `cell_set_tooltip`, each taking the table, the column and the row first.
- Whole table: `table.set_position`, `set_bgcolor`, `set_frame_color`, `set_frame_width`, `set_border_color`, `set_border_width`.
- `table.merge_cells(table, start_column, start_row, end_column, end_row)` joins a block; `table.clear(...)` empties a block of
  cells; `table.delete(table)` removes the table.

The functions work as methods too: `t.cell(0, 0, "x")`.

## Limits

There is room for one table per position: nine in all. A new table at a position that already has one deletes the old one, so a
script that makes a table on every bar keeps only the last. The limit cannot be changed. Cell text is limited to 999 characters.

<!-- /docs/scripting/chart-output/plots-or-drawings -->

# Plots or drawings: which to use

Use a **plot** for a series with a value on every bar that you want drawn as a line, histogram or area: an average, an oscillator.
A plot call stands at the top level and its look (width, style, title) is fixed for the run. Use a **drawing** for everything else:
marks on some bars, text built from data, levels or zones that follow data, anything created in a condition or a loop.

| You want | Refused form | Use |
|---|---|---|
| a plot on some bars only | `plot` inside `if` | `plot(cond ? value : na)`, or a drawing |
| text from data on a mark | `plotshape(..., text=str.tostring(x))` | `label.new` |
| a level that moves with data | `hline(close)` | `plot(value)` for a line on every bar; `line.new` for a segment |
| a zone between two prices | `fill` of series | `box.new`, or `fill` of two `plot`s |
| a title or width from data | non-const `title`, computed `linewidth` | a label; or one plot per case |
| a different shape or size by bar | `shape=` or `size=` from a condition | one `plotshape` per case |

## The refused forms

The messages for most rows are on other pages: a plot in a condition on [Plotting](/scripting/chart-output/plotting), a title from
data on [const, input, simple and series](/scripting/language/qualifiers), a computed `hline` price and a fill of a plot with a level on
[Fills and levels](/scripting/chart-output/fills-and-levels). A mark whose shape or size depends on the data:

```lipi-invalid
//@lipi=2
indicator("Size by bar")
plotshape(close > open, size=close > open ? size.small : size.large)
```

The compiler says: Cannot call `plotshape` with argument `size`=`close>open?size.small:size.large`. An argument of `series size` type was used but a `input size` is expected.

## What to use instead

Text from data, and a zone, as drawings. Both may sit inside a condition:

```lipi
//@lipi=2
indicator("Breakout labels and zone", overlay=true)
top = talib.highest(high, 20)
bottom = talib.lowest(low, 20)
if close > top[1] {
    label.new(bar_index, low, "Breakout " + str.tostring(close), style=label.style_label_up, color=color.green, textcolor=color.white)
}
if barstate.islast {
    box.new(bar_index - 20, top, bar_index, bottom, border_color=color.gray, bgcolor=color.new(color.gray, 0.9))
}
```

A drawing is not a series: it has no value on each bar, cannot be read back by other code as a series and counts against the
limits on [Lines, labels, boxes and polylines](/scripting/chart-output/drawings).

<!-- /docs/scripting/strategies/overview -->

# Strategies and backtesting

A strategy declares itself with `strategy(...)` instead of `indicator(...)` and places orders with the `strategy.*` functions. The orders are simulated: a built-in broker emulator fills them against the chart's bars on a simulated account. Nothing is sent to a real broker.

```lipi
//@lipi=2
strategy("Average cross", overlay=true, initial_capital=10000, default_qty_value=2, commission_value=0.1)
fast = talib.sma(close, 10)
slow = talib.sma(close, 30)
if talib.crossover(fast, slow) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(fast, slow) {
    strategy.close("Long")
}
plot(fast, title="Fast")
plot(slow, title="Slow")
```

The script runs once per bar; order calls may sit in `if`, loops and functions. See [Orders and positions](/scripting/strategies/orders-and-positions) for fills and [Reading a strategy's results](/scripting/strategies/strategy-results) for the account variables. In an `indicator()` script the order calls and `strategy.*` variables compile but do nothing.

## The declaration

`strategy(title, ...)` is called once at the top level; only `title` is required and every argument is `const`. The display arguments (`shorttitle`, `overlay`, `format`, `precision`, `scale`, `max_*_count`, `behind_chart`) are those of `indicator()`. The account arguments:

| Argument | Default | Meaning |
|---|---|---|
| `initial_capital` | 1000000 | Starting equity. |
| `default_qty_type` | `strategy.fixed` | `default_qty_value` as units (`strategy.fixed`), or as money (`"cash"`) or percent of equity (`"percent_of_equity"`) divided by a price. `strategy.cash` does not exist; the strings compile, but the price is the order's `limit` or `stop`, so an order with neither and no `qty` stops the script: `Invalid order quantity`. Use `strategy.fixed`, or pass `qty`. |
| `default_qty_value` | 1 | Size of an order with no `qty`. |
| `commission_type` | `strategy.commission_percent` | Or `strategy.commission_cash_per_order`, `strategy.commission_cash_per_contract`. |
| `commission_value` | 0 | Charged when a trade opens and when it closes; as a percent, 0.1 is 0.1%. |
| `pyramiding` | 1 | Open entries allowed in one direction. |
| `process_orders_on_close` | false | Also fill orders at the close of the bar that placed them. |
| `calc_on_order_fills` | false | Run the script again within the bar after an order fills. |
| `calc_on_every_tick` | false | On a forming realtime bar, run on every tick, not at the close. |

These values are not checked (`pyramiding=0` compiles). There is no slippage, margin or currency argument.

<!-- /docs/scripting/strategies/orders-and-positions -->

# Orders and positions

An order call queues an order; the broker emulator fills it on a later price. The account holds one net position (`strategy.position_size`: positive long, negative short) made of open entries, which close oldest first.

## When orders fill

On historical bars the emulator steps through each bar's prices (open, then high and low, then close; high first when the open is nearer the high), filling queued orders at each step. The script runs once, at the close, so an order placed on bar N is first tested on bar N+1:

- A market order fills at the open of bar N+1. With `process_orders_on_close=true`, an order placed on a confirmed bar also fills at that bar's close.
- A limit order fills at the first step at the limit or better (long: at or below). A stop order fills at the first step at the stop or worse (long: at or above). A stop-limit order arms at the stop, then fills by the limit rule.
- The fill price is that step's price, not the limit or stop level: a long limit at 99 on a bar that opens at 98 fills at 98.

## The order calls

| Call | What it does |
|---|---|
| `strategy.entry(id, direction, qty, limit, stop, oca_name, oca_type, comment)` | Opens or adds to a position. `direction` is `strategy.long` or `strategy.short`. `limit` and/or `stop` make it wait; otherwise market. |
| `strategy.order(id, direction, qty, limit, stop, oca_name, oca_type, comment)` | A raw net order: long adds, short subtracts, whatever the position. Can open, add, reduce or reverse; `pyramiding` does not apply. |
| `strategy.exit(id, from_entry, qty, profit, limit, loss, stop, oca_name, comment)` | Take-profit (`limit`) and stop-loss (`stop`) for the open position or for the entry `from_entry`. `profit` and `loss` are distances in ticks (`syminfo.minmove`) from the entry price; given with a price, the nearer level wins. |
| `strategy.close(id, qty, comment)` | Closes the entry named `id` at market, all or `qty`. |
| `strategy.close_all(comment)` | Closes the whole position at market. |
| `strategy.cancel(id)`, `strategy.cancel_all()` | Remove the queued orders with that `id`, or all; nothing happens if there are none. |

`qty` defaults to `default_qty_value`. For `entry` and `order`, a `qty` of zero or less counts as not given; for `close` it means the entry's whole open quantity; for `exit` it stops the script with `Invalid order quantity`, as does a default size that cannot be worked out.

- **Reversal:** `strategy.entry` against the open position closes it and opens the other side in one fill.
- **Pyramiding:** an entry is ignored, without an error, when `pyramiding` entries are already open in its direction.
- **Same id:** `entry` or `order` with an id still queued replaces that order; flipping its direction stops the script (`Entry order direction cannot be changed...`).
- **Exit:** ignored when the position is flat at the call, or when no `limit`, `stop`, `profit` or `loss` is given, so call it on bars where you are already in the trade, not on the entry bar. It queues two orders and a fill removes the other; a new call with the same `id` replaces both. `qty` defaults to the whole open quantity.
- **OCA:** `oca_name` works only with `oca_type`: `strategy.oca_cancel` removes the group's other orders on a fill, `strategy.oca_reduce` reduces their quantity.
- **Direction** is a plain string: `"buy"` compiles, then stops the script: `invalid strategy direction "buy"`.

```lipi
//@lipi=2
strategy("Breakout with exit", overlay=true)
hh = talib.highest(high, 20)
if close > hh[1] and strategy.position_size == 0 {
    strategy.entry("Long", strategy.long)
}
if strategy.position_size > 0 {
    strategy.exit("Exit", from_entry="Long", stop=strategy.position_avg_price * 0.97, limit=strategy.position_avg_price * 1.06)
}
plot(hh, title="20-bar high")
```

<!-- /docs/scripting/strategies/strategy-results -->

# Reading a strategy's results

A strategy reads its simulated account through `strategy.*` variables, which update as orders fill, and through functions that look at one trade by number. Use them to size orders, plot equity or label results.

| Variable | Meaning |
|---|---|
| `strategy.position_size` | Net quantity: positive long, negative short, 0 flat. |
| `strategy.position_avg_price` | Average entry price of the open entries. |
| `strategy.initial_capital` | The `initial_capital` of `strategy()`. |
| `strategy.equity` | `initial_capital + netprofit + openprofit`. |
| `strategy.netprofit` | Profit of closed trades, after commission on every fill. |
| `strategy.openprofit` | Unrealized profit of the open entries. |
| `strategy.grossprofit`, `strategy.grossloss` | Sum of winning and of losing closed trades (the loss is negative, before commission). |
| `strategy.wintrades`, `strategy.losstrades` | Closed trades with profit above zero, and all others. |
| `strategy.max_drawdown`, `strategy.max_runup` | Largest fall from an equity peak, largest rise from an equity low. |
| `strategy.opentrades`, `strategy.closedtrades` | Counts. Closing part of an entry counts one closed trade. |
| `strategy.account_currency` | The instrument's currency. |

All are series floats except the counts (ints) and `account_currency` (string).

## One trade at a time

Trade functions take a zero-based `trade_num` and return `na` when there is no such trade. Open trades are `0` to `strategy.opentrades - 1`, oldest first. Closed trades are numbered from the first ever closed, so the latest is `strategy.closedtrades - 1`; only the latest 1000 are kept.

- `strategy.opentrades_` followed by `entry_id`, `entry_price`, `size`, `profit`, `entry_bar_index`, `entry_time`, `entry_comment`, `max_drawdown` or `max_runup`: `strategy.opentrades_profit(0)`.
- `strategy.closedtrades_` followed by the same names, plus `exit_price`, `exit_bar_index`, `exit_time` and `commission`.

`_entry_bar_index` is the bar the order was placed on. A default market order fills on the next bar's open, so bars since entry are `bar_index - strategy.opentrades_entry_bar_index(0) - 1` (no `- 1` with `process_orders_on_close=true`). For a closed trade `exit_bar_index`, `max_drawdown` and `max_runup` always return 0 (they are not recorded); only the open-trade excursions are tracked. `_size` is unsigned; the open position's direction is the sign of `strategy.position_size`, and a closed trade's direction you keep yourself. Times are in milliseconds.

```lipi
//@lipi=2
strategy("Equity and last trade", initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
if barstate.islast and strategy.closedtrades > 0 {
    lastTrade = strategy.closedtrades - 1
    label.new(bar_index, close, text="Last trade: " + str.tostring(strategy.closedtrades_profit(lastTrade)))
}
plot(strategy.equity, title="Equity")
```

<!-- /docs/scripting/configuration/inputs -->

# Inputs

An input is a setting the person using your script can change from the chart without editing the code. You call an input function
once; the platform shows a control for it, and the call returns the value chosen. The value is fixed for a run of the script, so it
can be used where an `input` value is required, such as `hline(price)` and `plot(linewidth=...)`.

| Function | Control for | Returns |
|---|---|---|
| `input.int`, `input.float` | a number; `minval`, `maxval`, `step` or `options` | `input int`, `input float` |
| `input.bool` | a switch | `input bool` |
| `input.string` | text; `options` makes a list | `input string` |
| `input.color` | a color | `input color` |
| `input.source` | one of `open`, `high`, `low`, `close`, `hl2`, `hlc3`, `ohlc4`, `hlcc4` | `series float` |
| `input.price` | a price | `input float` |
| `input.time` | a time, in milliseconds | `input int` |
| `input.session`, `input.timeframe` | a session or timeframe string | `input string` |
| `input.text_area` | a long text | `input string` |
| `input.enum` | a member of your own `enum` | `input` enum |

`input(defval, ...)` picks the kind from the type of `defval` (`bool`, `color`, `int`, `float`, `string`, or a series for a source).

## Common arguments

After `defval`, every input takes `title`, `tooltip` (help text), `inline` (inputs with the same string share one row), `group`
(inputs with the same string sit under one heading), `confirm` and `display`. All are `const`. `defval` is `const` too, except for
`input.source`, and it may not be `na`:

```lipi-invalid
//@lipi=2
indicator("No default")
n = input.int(na, "Length")
plot(close)
```

The compiler says: Argument `defval` of `input.int()` cannot be `na`.

```lipi
//@lipi=2
indicator("Moving average", overlay=true)
src = input.source(close, "Source", group="Average")
length = input.int(20, "Length", minval=1, maxval=200, step=5, group="Average", inline="len")
fast = input.bool(true, "Show fast", tooltip="Adds a short average", group="Average")
col = input.color(color.orange, "Color", group="Average", inline="len")
shortAvg = talib.sma(src, 5)
plot(talib.sma(src, length), title="Average", color=col)
plot(fast ? shortAvg : na, title="Fast", color=color.gray)
```

`step` may be named: `input.int(14, "Length", step=5)` works. The compiler does not check that `defval` lies between `minval` and
`maxval`. `input.int` takes only an int default (`5.5` is refused); `input.float` accepts `5`.

`display` takes `display.*` constants, combined with `+`, and only tells the platform where to show the value; the script never
sees it. Its default is `display.none` for `input.bool`, `input.color`, `input.text_area` and `input.time`, and `display.all` for every other input
(`int`, `float`, `string`, `source`, `price`, `session`, `timeframe`, `enum`).

## Options

`options=[...]` turns a number or string input into a list. The default must be one of the options:

```lipi-invalid
//@lipi=2
indicator("Not an option")
n = input.int(10, "Length", options=[7, 14, 21])
plot(close)
```

The compiler says: Argument `defval` of `input.int()` value 10 is not in `options` [7, 14, 21].

## Time

`input.time` takes milliseconds since 1970 (UTC). A default written as `timestamp("2024-01-01")` passes the editor's check and fails
when the script is added to the chart, because `timestamp` is evaluated only when the script runs and is `na` until then:

```lipi-invalid
//@lipi=2
indicator("Start date")
start = input.time(timestamp("2024-01-01"), "Start")
plot(time >= start ? close : na)
```

The compiler says (when added to the chart): Argument `defval` of `input.time()` cannot be `na`. Give the number instead, or build the
date from three integer inputs, which are evaluated when the script runs:

```lipi
//@lipi=2
indicator("Since a date")
start = input.time(1704067200000, "Start (ms)")
day = timestamp(input.int(2024, "Year"), input.int(1, "Month"), input.int(1, "Day"))
plot(time >= start ? close : na, title="Since start")
plot(time >= day ? open : na, title="Since day", color=color.orange)
```

## Enum

`input.enum(defval, title, options, ...)` takes a member of an `enum` you declared (see
[Custom types and enums](/scripting/language/custom-types)); the member's title is the text of the control. `options` lists the
members offered and must contain `defval`.

```lipi
//@lipi=2
indicator("Mode", overlay=true)
enum Mode {
    Fast = "Fast (10)"
    Slow = "Slow (50)"
}
mode = input.enum(Mode.Fast, "Mode")
plot(talib.sma(close, mode == Mode.Fast ? 10 : 50))
```

## input.source accepts names, not expressions

The default of `input.source` must be one of the eight price series above: `input.source(talib.sma(close, 3))` is refused as not a valid source variable.

<!-- /docs/scripting/automation/alerts -->

# Alerts

A script can offer a condition for an alert (`alertcondition`) or raise an alert from its own logic (`alert`). Neither takes a
frequency argument.

| | `alert(message)` | `alertcondition(condition, title, message)` |
|---|---|---|
| Where it may be called | anywhere: top level, `if`, loops, functions | top level only |
| `message` | any `series string`, may change by bar | `const string`, optional, fixed |
| `condition` | none | a `bool` series, required |
| `title` | none | `const string`, optional |
| What it does | raises an alert while the script runs | declares a condition the user can choose when creating an alert |
| When it acts | only on realtime bars, only when the script runs as an alert, at most once per bar | the condition is evaluated on every bar |

## alert

Call `alert` where the event happens. Its message may be built from data. On historical bars it does nothing.

```lipi
//@lipi=2
indicator("Breakout alert", overlay=true)
top = talib.highest(high, 20)
if close > top[1] {
    alert("Breakout at " + str.tostring(close))
}
plot(top, title="20-bar high")
```

`alert` returns no value (`x = alert("a")` is refused: Cannot assign void value.).

On a forming bar the bar's one alert is raised on the first tick that asks for it, with that tick's price. To alert on the closed bar, write `if barstate.isconfirmed and condition` (see [How to avoid a result that changes after the bar closes](/scripting/how-to/avoid-a-result-that-changes-after-the-bar-closes)).

## alertcondition

Declare the condition once, at the top level, with a fixed title and message:

```lipi
//@lipi=2
indicator("Cross condition")
avg = talib.sma(close, 20)
alertcondition(talib.crossover(close, avg), title="Close above average", message="Close crossed above the 20-bar average")
plot(avg, title="Average")
```

The condition must be boolean (`alertcondition(close)` is refused: The `condition` argument of `alertcondition()` must be a boolean series.)
and the message is `const`: a series string there (`str.tostring(close)`) is refused as in [qualifiers](/scripting/language/qualifiers).

Inside an `if`, `alertcondition` is refused like `plot`: `alertcondition()` must be called in the global scope. Put the test in the
`condition` argument.

Use `alert` when the message or the moment depends on what the script worked out on this bar. Use `alertcondition` for a named
condition that the user turns into an alert. For delivery, see [Webhooks](/scripting/automation/webhooks).

<!-- /docs/scripting/automation/webhooks -->

# Webhooks for algo trading

A script cannot address an outside service: Lipi has no webhook function, and no argument names an address. Where an alert goes
and how it is delivered is set on the platform when the alert is created.

What the script controls is the alert's message text:

- `alert(message)` takes a message built on the bar, so it can carry data such as a price.
- `alertcondition(condition, title, message)` takes a fixed message.

The message is the one part of the alert the script writes.

```lipi
//@lipi=2
indicator("Signal message", overlay=true)
avg = talib.sma(close, 50)
if close > avg and close[1] <= avg[1] {
    alert("long " + str.tostring(close))
}
plot(avg, title="Average")
```

A strategy's orders are simulated and send nothing; `strategy.entry` and `strategy.exit` take no alert message. A strategy that must tell another system about a trade calls `alert` beside the order (example: [How to send a webhook when your condition fires](/scripting/how-to/send-a-webhook-when-your-condition-fires)).

See [Alerts](/scripting/automation/alerts) for where each function may be called and when it fires.

<!-- /docs/scripting/distribution/house-style -->

# House style and naming

Lipi accepts several spellings for some things. This page picks one so that scripts read alike. Breaking a rule is never an error.

## One spelling

- **Logic:** `and`, `or`, `not`, not `&&`, `||`, `!` (the same tokens).
- **Functions:** `func spread(float h, float l) => h - l`. The keyword-less form compiles too; `def` declares a method, not another spelling.
- **Body:** an arrow while the body is one expression; braces and `return` from two statements.
- **Parameters:** write the type; add a qualifier (`const`, `simple`) only to restrict. The default is `series`.
- **Analysis:** `talib.sma(...)`; `ta.sma(...)` is the same namespace.
- **Persistence:** `static`, or `intra` for a value kept across the ticks of one forming bar only; declare them after the inputs, assign with `:=`. `var` does not exist.
- **Arrays:** `array.new<float>(0)` and the method form `a.push(x)`.
- **Drawings:** create once into a `static` variable and change it with `set_*`.
- **Strategy ids:** one string constant per order id.
- **Absence:** `na(x)`, not `x == na` (a warning).
- **Enumerated arguments:** `plotStyle.histogram`, `display.pane`, `size.small`, not strings or numbers.
- **Colors:** `color.red` or `#RRGGBB`; fade with `color.new(color.red, 0.7)` (opacity 0 to 1).
- **Arguments:** name every argument after the second: `plot(x, title="Spread", color=color.red)`. `step=` may be named.

## Layout

- Order: `//@lipi=2`, the declaration, inputs, calculations, then `plot` and other output calls.
- One statement per line, four spaces per block level, `else` on the line of the closing `}`. Break a long statement after a comma or an operator, never before one.
- Comparisons do not chain and have unusual precedence: write `a < b and b < c`, and parenthesise mixed conditions.

## Names

- Variables, functions, arguments: lowerCamelCase (`fastLength`).
- Types, enums and their members: UpperCamelCase (`Swing`, `Speed.Fast`).
- Never reuse a built-in name (rules in [Names and conventions](/scripting/language/names-and-conventions)).

```lipi
//@lipi=2
indicator("Range ratio")
length = input.int(14, "Length", minval=1, maxval=200)
func ratio(float a, float b) => b == 0 ? na : a / b
avgRange = talib.sma(high - low, length)
plot(ratio(high - low, avgRange), title="Range ratio", color=color.blue)
hline(1.0, title="Average", color=color.gray)
```

<!-- /docs/scripting/distribution/limits -->

# Limits

Most limits are met while the script runs, so a script can pass every check and then stop on a bar. Only the title limit and the `talib.ema` window (see Messages) are checked earlier.

| Limit | Value | Enforced |
|---|---|---|
| History: `x[n]` and `talib` window lengths | 0 to 500 bars | Runs |
| Elements in an array | 10000 | Runs |
| Arguments of `array.from` | 4000 (999 for strings and other types) | Runs |
| Vertices in one polyline | 1000 | Runs, `polyline.new` gives `na` |
| Text of a label, box or table cell, and its tooltip | 999 characters | Runs |
| `indicator()` title and `shorttitle` | 128 characters | Adding to the chart |
| Drawings of one kind | 50 default, up to 500 (polylines 100) | Runs, by trimming |
| Tables | 9, one per `position.*` | Runs, by replacing |
| Open entries, queued orders, closed-trade detail | 1000, 3000, 1000 | Runs |
| Run time over history | 45 seconds | Runs |

## Messages

- History: The script is trying to access historical data outside allowed range (501). The allowed range is 0 to 500. `close[501]` compiles and then stops; so does `talib.sma(close, 600)`, with the length in the brackets. `talib.ema`, `macd`, `bbw`, `kc` and `kcw` refuse such a length already when the script is added to the chart.
- Arrays: Array size exceeds the maximum allowed length of 10000 (requested 10001). A `static` array grows on every bar unless you trim it. `array.from` with too many arguments stops with Error in `array.from()`: too many arguments: 4001 (max 4000).
- Polylines: a points array of more than 1000 (or none) makes `polyline.new` return `na`, with no error; keep the array at or under 1000 points.
- Text: String is too long (1000 characters). Maximum length is 999. A long literal still compiles.
- Title: String is too long (130 characters). Maximum length is 128. Only `indicator()` checks its title.
- Strategies: Maximum number of open trades (1000) exceeded. Maximum number of pending orders (3000) exceeded. Older closed trades return `na` from the `strategy.closedtrades_*` functions.
- Time: Execution cancelled, after 45 seconds. Loops have no iteration cap; this limit is the only stop.

## Drawings and tables

Set the limit per kind with `max_lines_count`, `max_labels_count`, `max_boxes_count` or `max_polylines_count` on `indicator()` or `strategy()` (constant integers). A larger value is clamped without an error; zero or less gives 50. Linefills are fixed at 50.

Going over is not an error: the oldest drawings of the kind are deleted down to the limit, except those a `static` variable holds directly (see [Lines, labels, boxes and polylines](/scripting/chart-output/drawings)). A table occupies its `position.*` slot: a new table there replaces the old one.

## Not limited

The compiler sets no limit on script length or on the number of variables, inputs or plots.

<!-- /docs/scripting/reference/errors -->

# Compiler messages

A message names the line and column; names in backticks stand for the name in your script. Fix the first error and check again: a script with several syntax errors reports only the last, and after a clean syntax most checks stop at the first error.

The **editor's check** reports syntax, names, types and scope. **Adding to the chart** also applies the compile-only rules below. **Running** raises the runtime errors, on a bar.

## Syntax

| Message | Meaning and fix |
|---|---|
| `no viable alternative at input '\n+'` | A line starts with an operator, so the line before already ended the statement. End that line with the operator. |
| `extraneous input ';' expecting {<EOF>, NEWLINE}` | A token that cannot follow a complete statement: `;`, `^`, a second statement on the line. One statement per line; `math.pow` for a power. |
| `mismatched input 'x' expecting {'}', NEWLINE}` | A block on one line, or a token out of place. Put each statement of a block on its own line. |
| `token recognition error at: '@'` | A character that is not part of Lipi. Remove it. |
| `var` is not a valid type in variable declaration. | `var`, `varip`, `map<...>` and other unknown types. Use `static`, or `array<float>`. |
| Type Function should have at least one parameter. | A `def` with no parameter. Use `func`. |
| Break statement can only be used inside a loop. | Likewise `Continue statement ...` and `Return statement can only be used inside a function.` Move the statement into the loop or function. |
| `if` conditional expression must be of a bool type! | The condition is a string. Use a comparison (`while` has the same message). |
| Script must declare exactly one of `indicator()`, `strategy()`, or `library()`; found 2 (indicator(), indicator()). | No declaration (`found 0 ((none))`), or two. Keep one. |

## Names

| Message | Meaning and fix |
|---|---|
| No variable with name `clsoe` found. | Misspelt, undeclared or out of scope (a block's variables end with the block); or a namespace Lipi lacks (`request`, `timeframe`). |
| Undeclared variable `x`. | `:=` on a name never declared. Declare it with `=`. |
| Variable `x` is already defined. Use `:=` to assign a new value. | `=` on a name already in this scope. |
| Namespace `talib` has no function `foo`. Did you mean `cmo()`? | Not in the namespace; take the hint. Same form for variables: Namespace `color` has no variable `pink`. Did you mean `lime`? |
| Function `g` is not available here. Functions must be defined before use, and cannot call themselves. | Declare a function above its first call; there is no recursion. |

## Types and qualifiers

| Message | Meaning and fix |
|---|---|
| Declared type `int` is not compatible with assigned type `const float`. | The value does not fit the type. Use `math.floor()`, `math.round()` or `math.ceil()` to get an `int`. |
| Cannot call `plot` with argument `linewidth`=`bar_index`. An argument of `series int` type was used but a `input int` is expected. | The parameter wants a fixed value (`const`, `input`, `simple`), the argument changes per bar. Use a literal or an input. |
| Argument `defval` of `input.int()` cannot be `na`. | An input default must be a value. |
| `volume` is not a valid source variable. Expected: open/high/low/close/hl2/hlc3/ohlc4/hlcc4 | The default of `input.source` is one of those eight. |

## Arguments and scope

| Message | Meaning and fix |
|---|---|
| The `plot()` function does not accept a named argument `colour`. Did you mean `color`? | Misspelt argument name. |
| The `talib.sma()` function is missing required argument(s): `length`. | A required argument is missing. |
| Cannot modify global variable `g` in function. | A function cannot reassign a global. Pass it in and return the result; pushing to a global array or setting a field of a global object is allowed. |
| `plot()` must be called in the global scope. | `plot`, `plotshape`, `plotchar`, `plotarrow`, `plotbar`, `plotcandle`, `hline`, `fill`, `bgcolor`, `barcolor`, `alertcondition` cannot sit in a function, `if`, loop or `switch`. Put the condition in an argument: `bgcolor(c ? color.green : na)`. |
| internal validator error | No line: the compiler stopped. Known cause: a size string that is not a size name (`size="enormous"`; `text_size` on `box.new` and `table.cell`) on `label.new`, `box.new`, `table.cell`, `plotchar` or `plotshape`. Use `size.tiny` ... `size.huge`. |
| History Indexing not allowed on tuple expression. | `[]` cannot follow a tuple, a void call or a literal. Assign it to a variable first. |

## Compile-path-only rules

These pass the editor's check and fail when the script is added to the chart (the phases are in [The editor](/scripting/getting-started/editor)).

`indicator("Mintick", format=format.mintick)` gives, when adding to the chart: The `format` argument of `indicator()` only accepts format.inherit, format.price, format.volume, or format.percent. Got `format.mintick`. The same phase refuses a `plot` or `hline` `format` other than `format.price`, `format.percent`, `format.volume`; any `display` but `display.none` and `display.all` on `fill`, `barcolor`, `bgcolor`; an `indicator()` title over 128 characters; and `input.time(timestamp("2024-01-01"))`, since `timestamp()` is `na` there (Argument `defval` of `input.time()` cannot be `na`.): give milliseconds; and a length above 500 in `talib.ema`, `macd`, `bbw`, `kc` or `kcw` (the history message on Limits); and a `switch` inside a called function, which is refused with only Not Implemented (use `if`).

## Runtime errors

These stop the script on a bar. The limit messages (history range 0 to 500, array size 10000, 45 seconds) are on [Limits](/scripting/distribution/limits).

| Message | Cause |
|---|---|
| Index out of bounds: 5, array length: 3. | An array index below 0 or past the last element. Test `array.length` first. |
| Invalid order quantity | `strategy.exit` with `qty` of zero or less, or a default size that cannot be worked out (`default_qty_value` of zero or less; `cash`/`percent_of_equity` with no price). |
