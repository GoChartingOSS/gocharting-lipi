Contents: str (library) · str.contains (function) · str.contains (function) · str.contains (function) · str.contains (function) · str.endswith (function) · str.endswith (function) · str.endswith (function) · str.endswith (function) · str.format_time (function) · str.format_time (function) · str.format_time (function) · str.format_time (function) · str.length (function) · str.length (function) · str.length (function) · str.length (function) · str.lower (function) · str.lower (function) · str.lower (function) · str.lower (function) · str.match (function) · str.match (function) · str.match (function) · str.match (function) · str.pos (function) · str.pos (function) · str.pos (function) · str.pos (function) · str.repeat (function) · str.repeat (function) · str.repeat (function) · str.repeat (function) · str.replace (function) · str.replace (function) · str.replace (function) · str.replace (function) · str.replace_all (function) · str.replace_all (function) · str.replace_all (function) · str.replace_all (function) · str.split (function) · str.split (function) · str.split (function) · str.split (function) · str.startswith (function) · str.startswith (function) · str.startswith (function) · str.startswith (function) · str.substring (function) · str.substring (function) · str.substring (function) · str.substring (function) · str.substring (function) · str.substring (function) · str.substring (function) · str.substring (function) · str.tonumber (function) · str.tonumber (function) · str.tonumber (function) · str.tonumber (function) · str.tostring (function) · str.tostring (function) · str.tostring (function) · str.tostring (function) · str.tostring (function) · str.tostring (function) · str.trim (function) · str.trim (function) · str.trim (function) · str.trim (function) · str.upper (function) · str.upper (function) · str.upper (function) · str.upper (function)

# str

## str (library)

Seventeen functions for working with text: tests such as `str.contains` and `str.startswith`, transformations such as `str.replace` and `str.substring`, conversions in both directions with `str.tonumber` and `str.tostring`, and `str.format_time` for rendering a time.

Use these to build an alert message or a plot's text, not to alter chart data.

### notes

- A string has no method form: `s.length()` is rejected. Call the function with the string as its first argument: `str.length(s)`.

### example

```lipi
//@lipi=2
indicator("str Library Example", overlay=true)
if barstate.islast {
    name = str.upper(syminfo.ticker)
    txt = name + " closed at " + str.tostring(math.round(close, 2))
    label.new(bar_index, high, text=str.contains(name, "USD") ? txt + " (USD pair)" : txt)
}
```

### id

library:str

## str.contains (function)

Tests whether one string occurs inside another.

Both arguments are required, and the function carries one signature per form of them.

### syntax

```
str.contains(const string source, const string str) → const bool
```

### args

- `source`: const string
  Source string.
  types: const string, literal string
- `str`: const string
  The substring to search for.
  types: const string, literal string

### returnedType

const bool

### example

```lipi
//@lipi=2
indicator("String Contains Example", overlay=false)
ticker = syminfo.ticker
isForex = str.contains(ticker, "USD")
plot(isForex ? 1 : 0, title="Contains USD", color=isForex ? color.green : color.red, style=plotStyle.bar)
```

### id

function:str.contains~1

## str.contains (function)

Tests whether one string occurs inside another.

Both arguments are required, and the function carries one signature per form of them.

### syntax

```
str.contains(input string source, input string str) → input bool
```

### args

- `source`: input string
  Source string.
  types: input string, const string, literal string
- `str`: input string
  The substring to search for.
  types: input string, const string, literal string

### returnedType

input bool

### example

```lipi
//@lipi=2
indicator("String Contains Example", overlay=false)
ticker = syminfo.ticker
isForex = str.contains(ticker, "USD")
plot(isForex ? 1 : 0, title="Contains USD", color=isForex ? color.green : color.red, style=plotStyle.bar)
```

### id

function:str.contains~2

## str.contains (function)

Tests whether one string occurs inside another.

Both arguments are required, and the function carries one signature per form of them.

### syntax

```
str.contains(simple string source, simple string str) → simple bool
```

### args

- `source`: simple string
  Source string.
  types: simple string, input string, const string, literal string
- `str`: simple string
  The substring to search for.
  types: simple string, input string, const string, literal string

### returnedType

simple bool

### example

```lipi
//@lipi=2
indicator("String Contains Example", overlay=false)
ticker = syminfo.ticker
isForex = str.contains(ticker, "USD")
plot(isForex ? 1 : 0, title="Contains USD", color=isForex ? color.green : color.red, style=plotStyle.bar)
```

### id

function:str.contains~3

## str.contains (function)

Tests whether one string occurs inside another.

Both arguments are required, and the function carries one signature per form of them.

### syntax

```
str.contains(series string source, series string str) → series bool
```

### args

- `source`: series string
  Source string.
  types: series string, simple string, input string, const string, literal string
- `str`: series string
  The substring to search for.
  types: series string, simple string, input string, const string, literal string

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("String Contains Example", overlay=false)
ticker = syminfo.ticker
isForex = str.contains(ticker, "USD")
plot(isForex ? 1 : 0, title="Contains USD", color=isForex ? color.green : color.red, style=plotStyle.bar)
```

### id

function:str.contains~4

## str.endswith (function)

Asks whether a string finishes with a given ending.

The suffix is a string, not a pattern, and both arguments are required.

### syntax

```
str.endswith(const string source, const string suffix) → const bool
```

### args

- `source`: const string
  Source string.
  types: const string, literal string
- `suffix`: const string
  The substring to search for.
  types: const string, literal string

### returnedType

const bool

### example

```lipi
//@lipi=2
indicator("String Contains Example", overlay=false)
ticker = syminfo.ticker
isForex = str.endswith(ticker, "USD")
plot(isForex ? 1 : 0, title="Contains USD", color=isForex ? color.green : color.red, style=plotStyle.bar)
```

### id

function:str.endswith~1

## str.endswith (function)

Asks whether a string finishes with a given ending.

The suffix is a string, not a pattern, and both arguments are required.

### syntax

```
str.endswith(input string source, input string suffix) → input bool
```

### args

- `source`: input string
  Source string.
  types: input string, const string, literal string
- `suffix`: input string
  The substring to search for.
  types: input string, const string, literal string

### returnedType

input bool

### example

```lipi
//@lipi=2
indicator("String Contains Example", overlay=false)
ticker = syminfo.ticker
isForex = str.endswith(ticker, "USD")
plot(isForex ? 1 : 0, title="Contains USD", color=isForex ? color.green : color.red, style=plotStyle.bar)
```

### id

function:str.endswith~2

## str.endswith (function)

Asks whether a string finishes with a given ending.

The suffix is a string, not a pattern, and both arguments are required.

### syntax

```
str.endswith(simple string source, simple string suffix) → simple bool
```

### args

- `source`: simple string
  Source string.
  types: simple string, input string, const string, literal string
- `suffix`: simple string
  The substring to search for.
  types: simple string, input string, const string, literal string

### returnedType

simple bool

### example

```lipi
//@lipi=2
indicator("String Contains Example", overlay=false)
ticker = syminfo.ticker
isForex = str.endswith(ticker, "USD")
plot(isForex ? 1 : 0, title="Contains USD", color=isForex ? color.green : color.red, style=plotStyle.bar)
```

### id

function:str.endswith~3

## str.endswith (function)

Asks whether a string finishes with a given ending.

The suffix is a string, not a pattern, and both arguments are required.

### syntax

```
str.endswith(series string source, series string suffix) → series bool
```

### args

- `source`: series string
  Source string.
  types: series string, simple string, input string, const string, literal string
- `suffix`: series string
  The substring to search for.
  types: series string, simple string, input string, const string, literal string

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("String Contains Example", overlay=false)
ticker = syminfo.ticker
isForex = str.endswith(ticker, "USD")
plot(isForex ? 1 : 0, title="Contains USD", color=isForex ? color.green : color.red, style=plotStyle.bar)
```

### id

function:str.endswith~4

## str.format_time (function)

Renders a time as text, in a format and a time zone you give.

`time_value` is in **seconds** since 1970-01-01 UTC, unlike `time`, `timenow` and the other Lipi times, which are in milliseconds: pass `math.floor(time / 1000)`. `format` is required and is written as a pattern of the reference date 2006-01-02 15:04:05 (for example `"2006-01-02 15:04"` or `"02 Jan 15:04"`). `timezone` defaults to `"UTC"`; an unknown time zone gives `na`.

### syntax

```
str.format_time(const int time_value, const string format, const string timezone) → const string
```

### args

- `time_value`: const int
  The time to render, in seconds since 1970-01-01 UTC. Lipi's own times are in milliseconds: divide by 1000 and round down with `math.floor`.
  types: const int, literal int
- `format`: const string
  The layout of the result, written as the reference date 2006-01-02 15:04:05 would appear: `2006` year, `01` month, `Jan` month name, `02` day, `15` hour (24-hour), `03` hour (12-hour), `04` minute, `05` second, `PM` the half of the day, `Mon` weekday. Required.
  types: const string, literal string
- `timezone?`: const string
  The time zone of the result, in UTC/GMT notation (such as `"UTC-5"` or `"GMT+0530"`) or as an IANA time zone name (such as `"America/New_York"`). Optional; the default is `"UTC"`. An unknown name gives `na`.
  types: const string, literal string
  default: "UTC"

### returnedType

const string

### notes

- `time_value` takes an int. A division such as `time / 1000` gives a float and is rejected; wrap it in `math.floor` to get an int.

### example

```lipi
//@lipi=2
indicator("str.format_time Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=str.format_time(math.floor(time / 1000), "2006-01-02 15:04", syminfo.timezone))
}
```

### id

function:str.format_time~1

## str.format_time (function)

Renders a time as text, in a format and a time zone you give.

`time_value` is in **seconds** since 1970-01-01 UTC, unlike `time`, `timenow` and the other Lipi times, which are in milliseconds: pass `math.floor(time / 1000)`. `format` is required and is written as a pattern of the reference date 2006-01-02 15:04:05 (for example `"2006-01-02 15:04"` or `"02 Jan 15:04"`). `timezone` defaults to `"UTC"`; an unknown time zone gives `na`.

### syntax

```
str.format_time(input int time_value, input string format, input string timezone) → input string
```

### args

- `time_value`: input int
  The time to render, in seconds since 1970-01-01 UTC. Lipi's own times are in milliseconds: divide by 1000 and round down with `math.floor`.
  types: input int, const int, literal int
- `format`: input string
  The layout of the result, written as the reference date 2006-01-02 15:04:05 would appear: `2006` year, `01` month, `Jan` month name, `02` day, `15` hour (24-hour), `03` hour (12-hour), `04` minute, `05` second, `PM` the half of the day, `Mon` weekday. Required.
  types: input string, const string, literal string
- `timezone?`: input string
  The time zone of the result, in UTC/GMT notation (such as `"UTC-5"` or `"GMT+0530"`) or as an IANA time zone name (such as `"America/New_York"`). Optional; the default is `"UTC"`. An unknown name gives `na`.
  types: input string, const string, literal string
  default: "UTC"

### returnedType

input string

### notes

- `time_value` takes an int. A division such as `time / 1000` gives a float and is rejected; wrap it in `math.floor` to get an int.

### example

```lipi
//@lipi=2
indicator("str.format_time Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=str.format_time(math.floor(time / 1000), "2006-01-02 15:04", syminfo.timezone))
}
```

### id

function:str.format_time~2

## str.format_time (function)

Renders a time as text, in a format and a time zone you give.

`time_value` is in **seconds** since 1970-01-01 UTC, unlike `time`, `timenow` and the other Lipi times, which are in milliseconds: pass `math.floor(time / 1000)`. `format` is required and is written as a pattern of the reference date 2006-01-02 15:04:05 (for example `"2006-01-02 15:04"` or `"02 Jan 15:04"`). `timezone` defaults to `"UTC"`; an unknown time zone gives `na`.

### syntax

```
str.format_time(simple int time_value, simple string format, simple string timezone) → simple string
```

### args

- `time_value`: simple int
  The time to render, in seconds since 1970-01-01 UTC. Lipi's own times are in milliseconds: divide by 1000 and round down with `math.floor`.
  types: simple int, input int, const int, literal int
- `format`: simple string
  The layout of the result, written as the reference date 2006-01-02 15:04:05 would appear: `2006` year, `01` month, `Jan` month name, `02` day, `15` hour (24-hour), `03` hour (12-hour), `04` minute, `05` second, `PM` the half of the day, `Mon` weekday. Required.
  types: simple string, input string, const string, literal string
- `timezone?`: simple string
  The time zone of the result, in UTC/GMT notation (such as `"UTC-5"` or `"GMT+0530"`) or as an IANA time zone name (such as `"America/New_York"`). Optional; the default is `"UTC"`. An unknown name gives `na`.
  types: simple string, input string, const string, literal string
  default: "UTC"

### returnedType

simple string

### notes

- `time_value` takes an int. A division such as `time / 1000` gives a float and is rejected; wrap it in `math.floor` to get an int.

### example

```lipi
//@lipi=2
indicator("str.format_time Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=str.format_time(math.floor(time / 1000), "2006-01-02 15:04", syminfo.timezone))
}
```

### id

function:str.format_time~3

## str.format_time (function)

Renders a time as text, in a format and a time zone you give.

`time_value` is in **seconds** since 1970-01-01 UTC, unlike `time`, `timenow` and the other Lipi times, which are in milliseconds: pass `math.floor(time / 1000)`. `format` is required and is written as a pattern of the reference date 2006-01-02 15:04:05 (for example `"2006-01-02 15:04"` or `"02 Jan 15:04"`). `timezone` defaults to `"UTC"`; an unknown time zone gives `na`.

### syntax

```
str.format_time(series int time_value, series string format, series string timezone) → series string
```

### args

- `time_value`: series int
  The time to render, in seconds since 1970-01-01 UTC. Lipi's own times are in milliseconds: divide by 1000 and round down with `math.floor`.
  types: series int, simple int, input int, const int, literal int
- `format`: series string
  The layout of the result, written as the reference date 2006-01-02 15:04:05 would appear: `2006` year, `01` month, `Jan` month name, `02` day, `15` hour (24-hour), `03` hour (12-hour), `04` minute, `05` second, `PM` the half of the day, `Mon` weekday. Required.
  types: series string, simple string, input string, const string, literal string
- `timezone?`: series string
  The time zone of the result, in UTC/GMT notation (such as `"UTC-5"` or `"GMT+0530"`) or as an IANA time zone name (such as `"America/New_York"`). Optional; the default is `"UTC"`. An unknown name gives `na`.
  types: series string, simple string, input string, const string, literal string
  default: "UTC"

### returnedType

series string

### notes

- `time_value` takes an int. A division such as `time / 1000` gives a float and is rejected; wrap it in `math.floor` to get an int.

### example

```lipi
//@lipi=2
indicator("str.format_time Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=str.format_time(math.floor(time / 1000), "2006-01-02 15:04", syminfo.timezone))
}
```

### id

function:str.format_time~4

## str.length (function)

Gives the length of a string as an int.

One argument, required. The length counts bytes of the text (UTF-8), not characters, so a character outside ASCII counts as two or more.

### syntax

```
str.length(const string source) → const int
```

### args

- `source`: const string
  Source string.
  types: const string, literal string

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("String Length Example", overlay=false)
tickerSymbol = syminfo.ticker
tickerLength = str.length(tickerSymbol)
plot(tickerLength, title="Ticker Length", color=color.blue)
```

### id

function:str.length~1

## str.length (function)

Gives the length of a string as an int.

One argument, required. The length counts bytes of the text (UTF-8), not characters, so a character outside ASCII counts as two or more.

### syntax

```
str.length(input string source) → input int
```

### args

- `source`: input string
  Source string.
  types: input string, const string, literal string

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("String Length Example", overlay=false)
tickerSymbol = syminfo.ticker
tickerLength = str.length(tickerSymbol)
plot(tickerLength, title="Ticker Length", color=color.blue)
```

### id

function:str.length~2

## str.length (function)

Gives the length of a string as an int.

One argument, required. The length counts bytes of the text (UTF-8), not characters, so a character outside ASCII counts as two or more.

### syntax

```
str.length(simple string source) → simple int
```

### args

- `source`: simple string
  Source string.
  types: simple string, input string, const string, literal string

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("String Length Example", overlay=false)
tickerSymbol = syminfo.ticker
tickerLength = str.length(tickerSymbol)
plot(tickerLength, title="Ticker Length", color=color.blue)
```

### id

function:str.length~3

## str.length (function)

Gives the length of a string as an int.

One argument, required. The length counts bytes of the text (UTF-8), not characters, so a character outside ASCII counts as two or more.

### syntax

```
str.length(series string source) → series int
```

### args

- `source`: series string
  Source string.
  types: series string, simple string, input string, const string, literal string

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("String Length Example", overlay=false)
tickerSymbol = syminfo.ticker
tickerLength = str.length(tickerSymbol)
plot(tickerLength, title="Ticker Length", color=color.blue)
```

### id

function:str.length~4

## str.lower (function)

Converts a string to lower case.

It takes the string and nothing else.

### syntax

```
str.lower(const string source) → const string
```

### args

- `source`: const string
  String to be converted.
  types: const string, literal string

### returnedType

const string

### example

```lipi
//@lipi=2
indicator("Lowercase Example", overlay=false)
tickerSymbol = syminfo.ticker
lowercaseTicker = str.lower(tickerSymbol)
isLowercase = tickerSymbol != lowercaseTicker
plot(isLowercase ? 1 : 0, title="Converted to Lowercase", color=color.blue)
```

### id

function:str.lower~1

## str.lower (function)

Converts a string to lower case.

It takes the string and nothing else.

### syntax

```
str.lower(input string source) → input string
```

### args

- `source`: input string
  String to be converted.
  types: input string, const string, literal string

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("Lowercase Example", overlay=false)
tickerSymbol = syminfo.ticker
lowercaseTicker = str.lower(tickerSymbol)
isLowercase = tickerSymbol != lowercaseTicker
plot(isLowercase ? 1 : 0, title="Converted to Lowercase", color=color.blue)
```

### id

function:str.lower~2

## str.lower (function)

Converts a string to lower case.

It takes the string and nothing else.

### syntax

```
str.lower(simple string source) → simple string
```

### args

- `source`: simple string
  String to be converted.
  types: simple string, input string, const string, literal string

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator("Lowercase Example", overlay=false)
tickerSymbol = syminfo.ticker
lowercaseTicker = str.lower(tickerSymbol)
isLowercase = tickerSymbol != lowercaseTicker
plot(isLowercase ? 1 : 0, title="Converted to Lowercase", color=color.blue)
```

### id

function:str.lower~3

## str.lower (function)

Converts a string to lower case.

It takes the string and nothing else.

### syntax

```
str.lower(series string source) → series string
```

### args

- `source`: series string
  String to be converted.
  types: series string, simple string, input string, const string, literal string

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("Lowercase Example", overlay=false)
tickerSymbol = syminfo.ticker
lowercaseTicker = str.lower(tickerSymbol)
isLowercase = tickerSymbol != lowercaseTicker
plot(isLowercase ? 1 : 0, title="Converted to Lowercase", color=color.blue)
```

### id

function:str.lower~4

## str.match (function)

Returns the first part of `source` that matches the regular expression `pattern`.

Patterns are written in RE2 syntax, which has no backreferences and no lookaround. A pattern that will not compile is not an error: the call returns empty text.

### syntax

```
str.match(const string source, const string pattern) → const string
```

### args

- `source`: const string
  Source string.
  types: const string, literal string
- `pattern`: const string
  The regular expression to which this string is to be matched.
  types: const string, literal string

### returnedType

const string

### example

```lipi
//@lipi=2
indicator("str.match Example", overlay=false)
string orderText = "order-4521-shipped"
string digits = str.match(orderText, "[0-9]+")
string capitals = str.match(orderText, "[A-Z]+")
plot(str.length(digits), title="Length of the match")
plot(str.length(capitals), title="Length when nothing matches")
```

### id

function:str.match~1

## str.match (function)

Returns the first part of `source` that matches the regular expression `pattern`.

Patterns are written in RE2 syntax, which has no backreferences and no lookaround. A pattern that will not compile is not an error: the call returns empty text.

### syntax

```
str.match(input string source, input string pattern) → input string
```

### args

- `source`: input string
  Source string.
  types: input string, const string, literal string
- `pattern`: input string
  The regular expression to which this string is to be matched.
  types: input string, const string, literal string

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("str.match Example", overlay=false)
string orderText = "order-4521-shipped"
string digits = str.match(orderText, "[0-9]+")
string capitals = str.match(orderText, "[A-Z]+")
plot(str.length(digits), title="Length of the match")
plot(str.length(capitals), title="Length when nothing matches")
```

### id

function:str.match~2

## str.match (function)

Returns the first part of `source` that matches the regular expression `pattern`.

Patterns are written in RE2 syntax, which has no backreferences and no lookaround. A pattern that will not compile is not an error: the call returns empty text.

### syntax

```
str.match(simple string source, simple string pattern) → simple string
```

### args

- `source`: simple string
  Source string.
  types: simple string, input string, const string, literal string
- `pattern`: simple string
  The regular expression to which this string is to be matched.
  types: simple string, input string, const string, literal string

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator("str.match Example", overlay=false)
string orderText = "order-4521-shipped"
string digits = str.match(orderText, "[0-9]+")
string capitals = str.match(orderText, "[A-Z]+")
plot(str.length(digits), title="Length of the match")
plot(str.length(capitals), title="Length when nothing matches")
```

### id

function:str.match~3

## str.match (function)

Returns the first part of `source` that matches the regular expression `pattern`.

Patterns are written in RE2 syntax, which has no backreferences and no lookaround. A pattern that will not compile is not an error: the call returns empty text.

### syntax

```
str.match(series string source, series string pattern) → series string
```

### args

- `source`: series string
  Source string.
  types: series string, simple string, input string, const string, literal string
- `pattern`: series string
  The regular expression to which this string is to be matched.
  types: series string, simple string, input string, const string, literal string

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("str.match Example", overlay=false)
string orderText = "order-4521-shipped"
string digits = str.match(orderText, "[0-9]+")
string capitals = str.match(orderText, "[A-Z]+")
plot(str.length(digits), title="Length of the match")
plot(str.length(capitals), title="Length when nothing matches")
```

### id

function:str.match~4

## str.pos (function)

Reports the position at which one string sits inside another.

The result is an int: the position of the first match, counted in bytes from 0, or -1 when `str` does not occur in `source`. For text outside ASCII a byte position is not a character position, so a result of `str.pos` passed to `str.substring`, which counts characters, can cut at the wrong place.

### syntax

```
str.pos(const string source, const string str) → const int
```

### args

- `source`: const string
  Source string.
  types: const string, literal string
- `str`: const string
  The substring to search for.
  types: const string, literal string

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("str.pos Example", overlay=true)
// Show where "USD" appears in the ticker
if barstate.islast {
    label.new(bar_index, high, text="USD at position " + str.tostring(str.pos(syminfo.ticker, "USD")))
}
```

### id

function:str.pos~1

## str.pos (function)

Reports the position at which one string sits inside another.

The result is an int: the position of the first match, counted in bytes from 0, or -1 when `str` does not occur in `source`. For text outside ASCII a byte position is not a character position, so a result of `str.pos` passed to `str.substring`, which counts characters, can cut at the wrong place.

### syntax

```
str.pos(input string source, input string str) → input int
```

### args

- `source`: input string
  Source string.
  types: input string, const string, literal string
- `str`: input string
  The substring to search for.
  types: input string, const string, literal string

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("str.pos Example", overlay=true)
// Show where "USD" appears in the ticker
if barstate.islast {
    label.new(bar_index, high, text="USD at position " + str.tostring(str.pos(syminfo.ticker, "USD")))
}
```

### id

function:str.pos~2

## str.pos (function)

Reports the position at which one string sits inside another.

The result is an int: the position of the first match, counted in bytes from 0, or -1 when `str` does not occur in `source`. For text outside ASCII a byte position is not a character position, so a result of `str.pos` passed to `str.substring`, which counts characters, can cut at the wrong place.

### syntax

```
str.pos(simple string source, simple string str) → simple int
```

### args

- `source`: simple string
  Source string.
  types: simple string, input string, const string, literal string
- `str`: simple string
  The substring to search for.
  types: simple string, input string, const string, literal string

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("str.pos Example", overlay=true)
// Show where "USD" appears in the ticker
if barstate.islast {
    label.new(bar_index, high, text="USD at position " + str.tostring(str.pos(syminfo.ticker, "USD")))
}
```

### id

function:str.pos~3

## str.pos (function)

Reports the position at which one string sits inside another.

The result is an int: the position of the first match, counted in bytes from 0, or -1 when `str` does not occur in `source`. For text outside ASCII a byte position is not a character position, so a result of `str.pos` passed to `str.substring`, which counts characters, can cut at the wrong place.

### syntax

```
str.pos(series string source, series string str) → series int
```

### args

- `source`: series string
  Source string.
  types: series string, simple string, input string, const string, literal string
- `str`: series string
  The substring to search for.
  types: series string, simple string, input string, const string, literal string

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("str.pos Example", overlay=true)
// Show where "USD" appears in the ticker
if barstate.islast {
    label.new(bar_index, high, text="USD at position " + str.tostring(str.pos(syminfo.ticker, "USD")))
}
```

### id

function:str.pos~4

## str.repeat (function)

Produces a string made of repeated copies of another, with the option of something between the copies.

The string and the count are required; the separator is not.

### syntax

```
str.repeat(const string source, const int count, const string separator) → const string
```

### args

- `source`: const string
  String to repeat.
  types: const string, literal string
- `count`: const int
  Number of times to repeat the source string. Must be greater than or equal to 0.
  types: const int, literal int
- `separator?`: const string
  String to inject between repeated values. Optional. The default is empty string.
  types: const string, literal string
  default: ""

### returnedType

const string

### example

```lipi
//@lipi=2
indicator("String Repeat Example", overlay=false)
str1 = "GoCharting"
repeatedStr = str.repeat(str1, 3)
plot(close, title=repeatedStr)
```

### id

function:str.repeat~1

## str.repeat (function)

Produces a string made of repeated copies of another, with the option of something between the copies.

The string and the count are required; the separator is not.

### syntax

```
str.repeat(input string source, input int count, input string separator) → input string
```

### args

- `source`: input string
  String to repeat.
  types: input string, const string, literal string
- `count`: input int
  Number of times to repeat the source string. Must be greater than or equal to 0.
  types: input int, const int, literal int
- `separator?`: input string
  String to inject between repeated values. Optional. The default is empty string.
  types: input string, const string, literal string
  default: ""

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("String Repeat Example", overlay=false)
str1 = "GoCharting"
repeatedStr = str.repeat(str1, 3)
plot(close, title=repeatedStr)
```

### id

function:str.repeat~2

## str.repeat (function)

Produces a string made of repeated copies of another, with the option of something between the copies.

The string and the count are required; the separator is not.

### syntax

```
str.repeat(simple string source, simple int count, simple string separator) → simple string
```

### args

- `source`: simple string
  String to repeat.
  types: simple string, input string, const string, literal string
- `count`: simple int
  Number of times to repeat the source string. Must be greater than or equal to 0.
  types: simple int, input int, const int, literal int
- `separator?`: simple string
  String to inject between repeated values. Optional. The default is empty string.
  types: simple string, input string, const string, literal string
  default: ""

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator("String Repeat Example", overlay=false)
str1 = "GoCharting"
repeatedStr = str.repeat(str1, 3)
plot(close, title=repeatedStr)
```

### id

function:str.repeat~3

## str.repeat (function)

Produces a string made of repeated copies of another, with the option of something between the copies.

The string and the count are required; the separator is not.

### syntax

```
str.repeat(series string source, series int count, series string separator) → series string
```

### args

- `source`: series string
  String to repeat.
  types: series string, simple string, input string, const string, literal string
- `count`: series int
  Number of times to repeat the source string. Must be greater than or equal to 0.
  types: series int, simple int, input int, const int, literal int
- `separator?`: series string
  String to inject between repeated values. Optional. The default is empty string.
  types: series string, simple string, input string, const string, literal string
  default: ""

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("String Repeat Example", overlay=false)
str1 = "GoCharting"
repeatedStr = str.repeat(str1, 3)
plot(close, title=repeatedStr)
```

### id

function:str.repeat~4

## str.replace (function)

Substitutes one piece of text for another inside a string.

The source, the old text and the new text are required; the count is optional.

### syntax

```
str.replace(const string source, const string old, const string new, const int count) → const string
```

### args

- `source`: const string
  Source string.
  types: const string, literal string
- `old`: const string
  String to be replaced.
  types: const string, literal string
- `new`: const string
  String to be inserted in place of `old`.
  types: const string, literal string
- `count?`: const int
  Maximum number of replacements, counted from the start of the string. Optional. The default is -1, which replaces every occurrence.
  types: const int, literal int
  default: -1

### returnedType

const string

### example

```lipi
//@lipi=2
indicator(str.replace("GoCharting is great!", "great", "awesome"), overlay=false)
plot(close)
```

### id

function:str.replace~1

## str.replace (function)

Substitutes one piece of text for another inside a string.

The source, the old text and the new text are required; the count is optional.

### syntax

```
str.replace(input string source, input string old, input string new, input int count) → input string
```

### args

- `source`: input string
  Source string.
  types: input string, const string, literal string
- `old`: input string
  String to be replaced.
  types: input string, const string, literal string
- `new`: input string
  String to be inserted in place of `old`.
  types: input string, const string, literal string
- `count?`: input int
  Maximum number of replacements, counted from the start of the string. Optional. The default is -1, which replaces every occurrence.
  types: input int, const int, literal int
  default: -1

### returnedType

input string

### example

```lipi
//@lipi=2
indicator(str.replace("GoCharting is great!", "great", "awesome"), overlay=false)
plot(close)
```

### id

function:str.replace~2

## str.replace (function)

Substitutes one piece of text for another inside a string.

The source, the old text and the new text are required; the count is optional.

### syntax

```
str.replace(simple string source, simple string old, simple string new, simple int count) → simple string
```

### args

- `source`: simple string
  Source string.
  types: simple string, input string, const string, literal string
- `old`: simple string
  String to be replaced.
  types: simple string, input string, const string, literal string
- `new`: simple string
  String to be inserted in place of `old`.
  types: simple string, input string, const string, literal string
- `count?`: simple int
  Maximum number of replacements, counted from the start of the string. Optional. The default is -1, which replaces every occurrence.
  types: simple int, input int, const int, literal int
  default: -1

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator(str.replace("GoCharting is great!", "great", "awesome"), overlay=false)
plot(close)
```

### id

function:str.replace~3

## str.replace (function)

Substitutes one piece of text for another inside a string.

The source, the old text and the new text are required; the count is optional.

### syntax

```
str.replace(series string source, series string old, series string new, series int count) → series string
```

### args

- `source`: series string
  Source string.
  types: series string, simple string, input string, const string, literal string
- `old`: series string
  String to be replaced.
  types: series string, simple string, input string, const string, literal string
- `new`: series string
  String to be inserted in place of `old`.
  types: series string, simple string, input string, const string, literal string
- `count?`: series int
  Maximum number of replacements, counted from the start of the string. Optional. The default is -1, which replaces every occurrence.
  types: series int, simple int, input int, const int, literal int
  default: -1

### returnedType

series string

### example

```lipi
//@lipi=2
indicator(str.replace("GoCharting is great!", "great", "awesome"), overlay=false)
plot(close)
```

### id

function:str.replace~4

## str.replace_all (function)

Substitutes new text for every occurrence of the old text.

It takes no count. That is the difference between it and str.replace, which does.

### syntax

```
str.replace_all(const string source, const string old, const string new) → const string
```

### args

- `source`: const string
  Source string.
  types: const string, literal string
- `old`: const string
  Text to look for: every occurrence of it in `source` is replaced.
  types: const string, literal string
- `new`: const string
  Text that replaces each occurrence of `old`.
  types: const string, literal string

### returnedType

const string

### example

```lipi
//@lipi=2
indicator(str.replace_all("GoCharting is great and GoCharting is powerful!", "Chart",  "view"), overlay=false)
plot(close)
```

### id

function:str.replace_all~1

## str.replace_all (function)

Substitutes new text for every occurrence of the old text.

It takes no count. That is the difference between it and str.replace, which does.

### syntax

```
str.replace_all(input string source, input string old, input string new) → input string
```

### args

- `source`: input string
  Source string.
  types: input string, const string, literal string
- `old`: input string
  Text to look for: every occurrence of it in `source` is replaced.
  types: input string, const string, literal string
- `new`: input string
  Text that replaces each occurrence of `old`.
  types: input string, const string, literal string

### returnedType

input string

### example

```lipi
//@lipi=2
indicator(str.replace_all("GoCharting is great and GoCharting is powerful!", "Chart",  "view"), overlay=false)
plot(close)
```

### id

function:str.replace_all~2

## str.replace_all (function)

Substitutes new text for every occurrence of the old text.

It takes no count. That is the difference between it and str.replace, which does.

### syntax

```
str.replace_all(simple string source, simple string old, simple string new) → simple string
```

### args

- `source`: simple string
  Source string.
  types: simple string, input string, const string, literal string
- `old`: simple string
  Text to look for: every occurrence of it in `source` is replaced.
  types: simple string, input string, const string, literal string
- `new`: simple string
  Text that replaces each occurrence of `old`.
  types: simple string, input string, const string, literal string

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator(str.replace_all("GoCharting is great and GoCharting is powerful!", "Chart",  "view"), overlay=false)
plot(close)
```

### id

function:str.replace_all~3

## str.replace_all (function)

Substitutes new text for every occurrence of the old text.

It takes no count. That is the difference between it and str.replace, which does.

### syntax

```
str.replace_all(series string source, series string old, series string new) → series string
```

### args

- `source`: series string
  Source string.
  types: series string, simple string, input string, const string, literal string
- `old`: series string
  Text to look for: every occurrence of it in `source` is replaced.
  types: series string, simple string, input string, const string, literal string
- `new`: series string
  Text that replaces each occurrence of `old`.
  types: series string, simple string, input string, const string, literal string

### returnedType

series string

### example

```lipi
//@lipi=2
indicator(str.replace_all("GoCharting is great and GoCharting is powerful!", "Chart",  "view"), overlay=false)
plot(close)
```

### id

function:str.replace_all~4

## str.split (function)

Splits `string` wherever `separator` occurs and returns the pieces as an array of strings. The separator itself is not included in the pieces.

### syntax

```
str.split(const string string, const string separator) → series array<string>
```

### args

- `string`: const string
  String to split.
  types: const string, literal string
- `separator`: const string
  The string at which `string` is split.
  types: const string, literal string

### returnedType

series array<string>

### example

```lipi
//@lipi=2
indicator("str.split Example", overlay=true)
parts = str.split("10,20,30", ",")
if barstate.islast {
    label.new(bar_index, high, text="Pieces: " + str.tostring(array.length(parts)))
}
```

### id

function:str.split~1

## str.split (function)

Splits `string` wherever `separator` occurs and returns the pieces as an array of strings. The separator itself is not included in the pieces.

### syntax

```
str.split(input string string, input string separator) → series array<string>
```

### args

- `string`: input string
  String to split.
  types: input string, const string, literal string
- `separator`: input string
  The string at which `string` is split.
  types: input string, const string, literal string

### returnedType

series array<string>

### example

```lipi
//@lipi=2
indicator("str.split Example", overlay=true)
parts = str.split("10,20,30", ",")
if barstate.islast {
    label.new(bar_index, high, text="Pieces: " + str.tostring(array.length(parts)))
}
```

### id

function:str.split~2

## str.split (function)

Splits `string` wherever `separator` occurs and returns the pieces as an array of strings. The separator itself is not included in the pieces.

### syntax

```
str.split(simple string string, simple string separator) → series array<string>
```

### args

- `string`: simple string
  String to split.
  types: simple string, input string, const string, literal string
- `separator`: simple string
  The string at which `string` is split.
  types: simple string, input string, const string, literal string

### returnedType

series array<string>

### example

```lipi
//@lipi=2
indicator("str.split Example", overlay=true)
parts = str.split("10,20,30", ",")
if barstate.islast {
    label.new(bar_index, high, text="Pieces: " + str.tostring(array.length(parts)))
}
```

### id

function:str.split~3

## str.split (function)

Splits `string` wherever `separator` occurs and returns the pieces as an array of strings. The separator itself is not included in the pieces.

### syntax

```
str.split(series string string, series string separator) → series array<string>
```

### args

- `string`: series string
  String to split.
  types: series string, simple string, input string, const string, literal string
- `separator`: series string
  The string at which `string` is split.
  types: series string, simple string, input string, const string, literal string

### returnedType

series array<string>

### example

```lipi
//@lipi=2
indicator("str.split Example", overlay=true)
parts = str.split("10,20,30", ",")
if barstate.islast {
    label.new(bar_index, high, text="Pieces: " + str.tostring(array.length(parts)))
}
```

### id

function:str.split~4

## str.startswith (function)

The counterpart of str.endswith, looking at the front of the string instead of the back.

Both arguments are required.

### syntax

```
str.startswith(const string source, const string prefix) → const bool
```

### args

- `source`: const string
  Source string.
  types: const string, literal string
- `prefix`: const string
  The substring to search for.
  types: const string, literal string

### returnedType

const bool

### example

```lipi
//@lipi=2
indicator("String StartsWith Example", overlay=false)
myStr = "GoCharting is awesome!"
doesStart = str.startswith(myStr, "GoCharting")
plot(doesStart ? 1 : 0, title="Starts with 'GoCharting'")
```

### id

function:str.startswith~1

## str.startswith (function)

The counterpart of str.endswith, looking at the front of the string instead of the back.

Both arguments are required.

### syntax

```
str.startswith(input string source, input string prefix) → input bool
```

### args

- `source`: input string
  Source string.
  types: input string, const string, literal string
- `prefix`: input string
  The substring to search for.
  types: input string, const string, literal string

### returnedType

input bool

### example

```lipi
//@lipi=2
indicator("String StartsWith Example", overlay=false)
myStr = "GoCharting is awesome!"
doesStart = str.startswith(myStr, "GoCharting")
plot(doesStart ? 1 : 0, title="Starts with 'GoCharting'")
```

### id

function:str.startswith~2

## str.startswith (function)

The counterpart of str.endswith, looking at the front of the string instead of the back.

Both arguments are required.

### syntax

```
str.startswith(simple string source, simple string prefix) → simple bool
```

### args

- `source`: simple string
  Source string.
  types: simple string, input string, const string, literal string
- `prefix`: simple string
  The substring to search for.
  types: simple string, input string, const string, literal string

### returnedType

simple bool

### example

```lipi
//@lipi=2
indicator("String StartsWith Example", overlay=false)
myStr = "GoCharting is awesome!"
doesStart = str.startswith(myStr, "GoCharting")
plot(doesStart ? 1 : 0, title="Starts with 'GoCharting'")
```

### id

function:str.startswith~3

## str.startswith (function)

The counterpart of str.endswith, looking at the front of the string instead of the back.

Both arguments are required.

### syntax

```
str.startswith(series string source, series string prefix) → series bool
```

### args

- `source`: series string
  Source string.
  types: series string, simple string, input string, const string, literal string
- `prefix`: series string
  The substring to search for.
  types: series string, simple string, input string, const string, literal string

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("String StartsWith Example", overlay=false)
myStr = "GoCharting is awesome!"
doesStart = str.startswith(myStr, "GoCharting")
plot(doesStart ? 1 : 0, title="Starts with 'GoCharting'")
```

### id

function:str.startswith~4

## str.substring (function)

Cuts a piece out of a string. There are two forms: one takes a start and an end, the other takes a start alone.

Positions are ints, counted in characters from 0, not in bytes. `start` is inclusive and `end` is exclusive. Without `end`, the result runs to the end of `source`. A `start` at or beyond the end of the text gives an empty string, and an `end` beyond it stops at the end. With `end`, a negative `start` or `end`, or an `end` before `start`, is refused with the error "Invalid argument passed to Subsctring" by the check that runs when the script is added to the chart (the editor's check does not report it); on a later bar the same invalid range gives `na`. Without `end`, a negative `start` gives an empty string.

### syntax

```
str.substring(const string source, const int start, const int end) → const string
```

### args

- `source`: const string
  Source string from which to extract the substring.
  types: const string, literal string
- `start`: const int
  The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
  types: const int, literal int
- `end`: const int
  The ending position. It is exclusive (the extracted string does not include the character at that position).
  types: const int, literal int

### returnedType

const string

### example

```lipi
//@lipi=2
indicator("String Substring Example", overlay=false)
myStr = "GoCharting is powerful"
subStr = str.substring(myStr, 0, 10)
plot(close, title=subStr)
```

### id

function:str.substring~1

## str.substring (function)

Cuts a piece out of a string. There are two forms: one takes a start and an end, the other takes a start alone.

Positions are ints, counted in characters from 0, not in bytes. `start` is inclusive and `end` is exclusive. Without `end`, the result runs to the end of `source`. A `start` at or beyond the end of the text gives an empty string, and an `end` beyond it stops at the end. With `end`, a negative `start` or `end`, or an `end` before `start`, is refused with the error "Invalid argument passed to Subsctring" by the check that runs when the script is added to the chart (the editor's check does not report it); on a later bar the same invalid range gives `na`. Without `end`, a negative `start` gives an empty string.

### syntax

```
str.substring(input string source, input int start, input int end) → input string
```

### args

- `source`: input string
  Source string from which to extract the substring.
  types: input string, const string, literal string
- `start`: input int
  The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
  types: input int, const int, literal int
- `end`: input int
  The ending position. It is exclusive (the extracted string does not include the character at that position).
  types: input int, const int, literal int

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("String Substring Example", overlay=false)
myStr = "GoCharting is powerful"
subStr = str.substring(myStr, 0, 10)
plot(close, title=subStr)
```

### id

function:str.substring~2

## str.substring (function)

Cuts a piece out of a string. There are two forms: one takes a start and an end, the other takes a start alone.

Positions are ints, counted in characters from 0, not in bytes. `start` is inclusive and `end` is exclusive. Without `end`, the result runs to the end of `source`. A `start` at or beyond the end of the text gives an empty string, and an `end` beyond it stops at the end. With `end`, a negative `start` or `end`, or an `end` before `start`, is refused with the error "Invalid argument passed to Subsctring" by the check that runs when the script is added to the chart (the editor's check does not report it); on a later bar the same invalid range gives `na`. Without `end`, a negative `start` gives an empty string.

### syntax

```
str.substring(simple string source, simple int start, simple int end) → simple string
```

### args

- `source`: simple string
  Source string from which to extract the substring.
  types: simple string, input string, const string, literal string
- `start`: simple int
  The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
  types: simple int, input int, const int, literal int
- `end`: simple int
  The ending position. It is exclusive (the extracted string does not include the character at that position).
  types: simple int, input int, const int, literal int

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator("String Substring Example", overlay=false)
myStr = "GoCharting is powerful"
subStr = str.substring(myStr, 0, 10)
plot(close, title=subStr)
```

### id

function:str.substring~3

## str.substring (function)

Cuts a piece out of a string. There are two forms: one takes a start and an end, the other takes a start alone.

Positions are ints, counted in characters from 0, not in bytes. `start` is inclusive and `end` is exclusive. Without `end`, the result runs to the end of `source`. A `start` at or beyond the end of the text gives an empty string, and an `end` beyond it stops at the end. With `end`, a negative `start` or `end`, or an `end` before `start`, is refused with the error "Invalid argument passed to Subsctring" by the check that runs when the script is added to the chart (the editor's check does not report it); on a later bar the same invalid range gives `na`. Without `end`, a negative `start` gives an empty string.

### syntax

```
str.substring(series string source, series int start, series int end) → series string
```

### args

- `source`: series string
  Source string from which to extract the substring.
  types: series string, simple string, input string, const string, literal string
- `start`: series int
  The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
  types: series int, simple int, input int, const int, literal int
- `end`: series int
  The ending position. It is exclusive (the extracted string does not include the character at that position).
  types: series int, simple int, input int, const int, literal int

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("String Substring Example", overlay=false)
myStr = "GoCharting is powerful"
subStr = str.substring(myStr, 0, 10)
plot(close, title=subStr)
```

### id

function:str.substring~4

## str.substring (function)

Cuts a piece out of a string. There are two forms: one takes a start and an end, the other takes a start alone.

Positions are ints, counted in characters from 0, not in bytes. `start` is inclusive and `end` is exclusive. Without `end`, the result runs to the end of `source`. A `start` at or beyond the end of the text gives an empty string, and an `end` beyond it stops at the end. With `end`, a negative `start` or `end`, or an `end` before `start`, is refused with the error "Invalid argument passed to Subsctring" by the check that runs when the script is added to the chart (the editor's check does not report it); on a later bar the same invalid range gives `na`. Without `end`, a negative `start` gives an empty string.

### syntax

```
str.substring(const string source, const int start) → const string
```

### args

- `source`: const string
  Source string from which to extract the substring.
  types: const string, literal string
- `start`: const int
  The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
  types: const int, literal int

### returnedType

const string

### example

```lipi
//@lipi=2
indicator("String Substring Example", overlay=false)
myStr = "GoCharting is powerful"
subStr = str.substring(myStr, 0, 10)
plot(close, title=subStr)
```

### id

function:str.substring~5

## str.substring (function)

Cuts a piece out of a string. There are two forms: one takes a start and an end, the other takes a start alone.

Positions are ints, counted in characters from 0, not in bytes. `start` is inclusive and `end` is exclusive. Without `end`, the result runs to the end of `source`. A `start` at or beyond the end of the text gives an empty string, and an `end` beyond it stops at the end. With `end`, a negative `start` or `end`, or an `end` before `start`, is refused with the error "Invalid argument passed to Subsctring" by the check that runs when the script is added to the chart (the editor's check does not report it); on a later bar the same invalid range gives `na`. Without `end`, a negative `start` gives an empty string.

### syntax

```
str.substring(input string source, input int start) → input string
```

### args

- `source`: input string
  Source string from which to extract the substring.
  types: input string, const string, literal string
- `start`: input int
  The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
  types: input int, const int, literal int

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("String Substring Example", overlay=false)
myStr = "GoCharting is powerful"
subStr = str.substring(myStr, 0, 10)
plot(close, title=subStr)
```

### id

function:str.substring~6

## str.substring (function)

Cuts a piece out of a string. There are two forms: one takes a start and an end, the other takes a start alone.

Positions are ints, counted in characters from 0, not in bytes. `start` is inclusive and `end` is exclusive. Without `end`, the result runs to the end of `source`. A `start` at or beyond the end of the text gives an empty string, and an `end` beyond it stops at the end. With `end`, a negative `start` or `end`, or an `end` before `start`, is refused with the error "Invalid argument passed to Subsctring" by the check that runs when the script is added to the chart (the editor's check does not report it); on a later bar the same invalid range gives `na`. Without `end`, a negative `start` gives an empty string.

### syntax

```
str.substring(simple string source, simple int start) → simple string
```

### args

- `source`: simple string
  Source string from which to extract the substring.
  types: simple string, input string, const string, literal string
- `start`: simple int
  The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
  types: simple int, input int, const int, literal int

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator("String Substring Example", overlay=false)
myStr = "GoCharting is powerful"
subStr = str.substring(myStr, 0, 10)
plot(close, title=subStr)
```

### id

function:str.substring~7

## str.substring (function)

Cuts a piece out of a string. There are two forms: one takes a start and an end, the other takes a start alone.

Positions are ints, counted in characters from 0, not in bytes. `start` is inclusive and `end` is exclusive. Without `end`, the result runs to the end of `source`. A `start` at or beyond the end of the text gives an empty string, and an `end` beyond it stops at the end. With `end`, a negative `start` or `end`, or an `end` before `start`, is refused with the error "Invalid argument passed to Subsctring" by the check that runs when the script is added to the chart (the editor's check does not report it); on a later bar the same invalid range gives `na`. Without `end`, a negative `start` gives an empty string.

### syntax

```
str.substring(series string source, series int start) → series string
```

### args

- `source`: series string
  Source string from which to extract the substring.
  types: series string, simple string, input string, const string, literal string
- `start`: series int
  The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
  types: series int, simple int, input int, const int, literal int

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("String Substring Example", overlay=false)
myStr = "GoCharting is powerful"
subStr = str.substring(myStr, 0, 10)
plot(close, title=subStr)
```

### id

function:str.substring~8

## str.tonumber (function)

Reads a number out of a string.

The result is a float in every form, so a string holding a whole number still comes back as a float.

### syntax

```
str.tonumber(const string source) → const float
```

### args

- `source`: const string
  String containing the representation of an integer or floating point value.
  types: const string, literal string

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("String to Number Example", overlay=false)
numStr1 = "123.45"
numStr2 = "456"
num1 = str.tonumber(numStr1)
num2 = str.tonumber(numStr2)
plot(num1, title="Converted Number 1")
plot(num2, title="Converted Number 2")
```

### id

function:str.tonumber~1

## str.tonumber (function)

Reads a number out of a string.

The result is a float in every form, so a string holding a whole number still comes back as a float.

### syntax

```
str.tonumber(input string source) → input float
```

### args

- `source`: input string
  String containing the representation of an integer or floating point value.
  types: input string, const string, literal string

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("String to Number Example", overlay=false)
numStr1 = "123.45"
numStr2 = "456"
num1 = str.tonumber(numStr1)
num2 = str.tonumber(numStr2)
plot(num1, title="Converted Number 1")
plot(num2, title="Converted Number 2")
```

### id

function:str.tonumber~2

## str.tonumber (function)

Reads a number out of a string.

The result is a float in every form, so a string holding a whole number still comes back as a float.

### syntax

```
str.tonumber(simple string source) → simple float
```

### args

- `source`: simple string
  String containing the representation of an integer or floating point value.
  types: simple string, input string, const string, literal string

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("String to Number Example", overlay=false)
numStr1 = "123.45"
numStr2 = "456"
num1 = str.tonumber(numStr1)
num2 = str.tonumber(numStr2)
plot(num1, title="Converted Number 1")
plot(num2, title="Converted Number 2")
```

### id

function:str.tonumber~3

## str.tonumber (function)

Reads a number out of a string.

The result is a float in every form, so a string holding a whole number still comes back as a float.

### syntax

```
str.tonumber(series string source) → series float
```

### args

- `source`: series string
  String containing the representation of an integer or floating point value.
  types: series string, simple string, input string, const string, literal string

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("String to Number Example", overlay=false)
numStr1 = "123.45"
numStr2 = "456"
num1 = str.tonumber(numStr1)
num2 = str.tonumber(numStr2)
plot(num1, title="Converted Number 1")
plot(num2, title="Converted Number 2")
```

### id

function:str.tonumber~4

## str.tostring (function)

Renders a value as a string.

Overload on `float` or `bool` alone: a float is rounded to 4 decimal places and trailing zeros are trimmed, so a smaller difference is lost (`0.00004` gives `0`); to keep more digits, use the overload with `format`, for example `str.tostring(price, "#.########")`. Bools become `true` or `false`; `na` becomes `"NA"`.

Overload on `float` with `format` (and optional `mintick`): supports `mintick`, `volume`, and `percent`, plus custom patterns made of `#` and `0` (for example `#.##`). Default format is `#.##########`.

### syntax

```
str.tostring(simple float source) → simple string
```

### args

- `source`: simple float
  Value to convert (`float` or `bool` depending on overload).
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple string

### returnDesc

String representation of the input.

### example

```lipi
//@lipi=2
indicator("str.tostring Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Vol: " + str.tostring(volume, format.volume))
    label.new(bar_index, low, text="Tick: " + str.tostring(close, format.mintick), style=label.style_label_up)
}
```

### id

function:str.tostring~1

## str.tostring (function)

Renders a value as a string.

Overload on `float` or `bool` alone: a float is rounded to 4 decimal places and trailing zeros are trimmed, so a smaller difference is lost (`0.00004` gives `0`); to keep more digits, use the overload with `format`, for example `str.tostring(price, "#.########")`. Bools become `true` or `false`; `na` becomes `"NA"`.

Overload on `float` with `format` (and optional `mintick`): supports `mintick`, `volume`, and `percent`, plus custom patterns made of `#` and `0` (for example `#.##`). Default format is `#.##########`.

### syntax

```
str.tostring(series float source) → series string
```

### args

- `source`: series float
  Value to convert (`float` or `bool` depending on overload).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series string

### returnDesc

String representation of the input.

### example

```lipi
//@lipi=2
indicator("str.tostring Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Vol: " + str.tostring(volume, format.volume))
    label.new(bar_index, low, text="Tick: " + str.tostring(close, format.mintick), style=label.style_label_up)
}
```

### id

function:str.tostring~2

## str.tostring (function)

Renders a value as a string.

Overload on `float` or `bool` alone: a float is rounded to 4 decimal places and trailing zeros are trimmed, so a smaller difference is lost (`0.00004` gives `0`); to keep more digits, use the overload with `format`, for example `str.tostring(price, "#.########")`. Bools become `true` or `false`; `na` becomes `"NA"`.

Overload on `float` with `format` (and optional `mintick`): supports `mintick`, `volume`, and `percent`, plus custom patterns made of `#` and `0` (for example `#.##`). Default format is `#.##########`.

### syntax

```
str.tostring(simple float value, simple string format, simple float mintick) → simple string
```

### args

- `value`: simple float
  Float to format when using the two- or three-argument overload (`value`, `format`, optional `mintick`).
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
- `format?`: simple string
  Format name or pattern for the float overload: `format.mintick`, `format.volume`, `format.percent`, a `#`/`0` pattern, or the default `#.##########`.
  types: simple string, input string, const string, literal string
  default: "#.##########"
- `mintick?`: simple float
  Tick size used when `format` is `format.mintick`. Defaults to `syminfo.mintick` when omitted.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
  default: syminfo.mintick

### returnedType

simple string

### returnDesc

String representation of the input.

### example

```lipi
//@lipi=2
indicator("str.tostring Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Vol: " + str.tostring(volume, format.volume))
    label.new(bar_index, low, text="Tick: " + str.tostring(close, format.mintick), style=label.style_label_up)
}
```

### id

function:str.tostring~3

## str.tostring (function)

Renders a value as a string.

Overload on `float` or `bool` alone: a float is rounded to 4 decimal places and trailing zeros are trimmed, so a smaller difference is lost (`0.00004` gives `0`); to keep more digits, use the overload with `format`, for example `str.tostring(price, "#.########")`. Bools become `true` or `false`; `na` becomes `"NA"`.

Overload on `float` with `format` (and optional `mintick`): supports `mintick`, `volume`, and `percent`, plus custom patterns made of `#` and `0` (for example `#.##`). Default format is `#.##########`.

### syntax

```
str.tostring(series float value, series string format, simple float mintick) → series string
```

### args

- `value`: series float
  Float to format when using the two- or three-argument overload (`value`, `format`, optional `mintick`).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `format?`: series string
  Format name or pattern for the float overload: `format.mintick`, `format.volume`, `format.percent`, a `#`/`0` pattern, or the default `#.##########`.
  types: series string, simple string, input string, const string, literal string
  default: "#.##########"
- `mintick?`: simple float
  Tick size used when `format` is `format.mintick`. Defaults to `syminfo.mintick` when omitted.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
  default: syminfo.mintick

### returnedType

series string

### returnDesc

String representation of the input.

### example

```lipi
//@lipi=2
indicator("str.tostring Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Vol: " + str.tostring(volume, format.volume))
    label.new(bar_index, low, text="Tick: " + str.tostring(close, format.mintick), style=label.style_label_up)
}
```

### id

function:str.tostring~4

## str.tostring (function)

Renders a value as a string.

Overload on `float` or `bool` alone: a float is rounded to 4 decimal places and trailing zeros are trimmed, so a smaller difference is lost (`0.00004` gives `0`); to keep more digits, use the overload with `format`, for example `str.tostring(price, "#.########")`. Bools become `true` or `false`; `na` becomes `"NA"`.

Overload on `float` with `format` (and optional `mintick`): supports `mintick`, `volume`, and `percent`, plus custom patterns made of `#` and `0` (for example `#.##`). Default format is `#.##########`.

### syntax

```
str.tostring(simple bool source) → simple string
```

### args

- `source`: simple bool
  Value to convert (`float` or `bool` depending on overload).
  types: simple bool, simple int, input int, const int, literal int, simple float, input float, const float, literal float, input bool, const bool, literal bool

### returnedType

simple string

### returnDesc

String representation of the input.

### example

```lipi
//@lipi=2
indicator("str.tostring Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Vol: " + str.tostring(volume, format.volume))
    label.new(bar_index, low, text="Tick: " + str.tostring(close, format.mintick), style=label.style_label_up)
}
```

### id

function:str.tostring~5

## str.tostring (function)

Renders a value as a string.

Overload on `float` or `bool` alone: a float is rounded to 4 decimal places and trailing zeros are trimmed, so a smaller difference is lost (`0.00004` gives `0`); to keep more digits, use the overload with `format`, for example `str.tostring(price, "#.########")`. Bools become `true` or `false`; `na` becomes `"NA"`.

Overload on `float` with `format` (and optional `mintick`): supports `mintick`, `volume`, and `percent`, plus custom patterns made of `#` and `0` (for example `#.##`). Default format is `#.##########`.

### syntax

```
str.tostring(series bool source) → series string
```

### args

- `source`: series bool
  Value to convert (`float` or `bool` depending on overload).
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool

### returnedType

series string

### returnDesc

String representation of the input.

### example

```lipi
//@lipi=2
indicator("str.tostring Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Vol: " + str.tostring(volume, format.volume))
    label.new(bar_index, low, text="Tick: " + str.tostring(close, format.mintick), style=label.style_label_up)
}
```

### id

function:str.tostring~6

## str.trim (function)

Removes whitespace from around a string and hands back the result.

It removes the white space that Unicode defines at both ends: spaces, tabs, line breaks and the other characters Unicode marks as white space.

### syntax

```
str.trim(const string source) → const string
```

### args

- `source`: const string
  String to trim.
  types: const string, literal string

### returnedType

const string

### example

```lipi
//@lipi=2
indicator("String Trim Example", overlay=false)
strWithSpaces = "GoCharting"
trimmedStr = str.trim(strWithSpaces)
plot(close, title=trimmedStr)
```

### id

function:str.trim~1

## str.trim (function)

Removes whitespace from around a string and hands back the result.

It removes the white space that Unicode defines at both ends: spaces, tabs, line breaks and the other characters Unicode marks as white space.

### syntax

```
str.trim(input string source) → input string
```

### args

- `source`: input string
  String to trim.
  types: input string, const string, literal string

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("String Trim Example", overlay=false)
strWithSpaces = "GoCharting"
trimmedStr = str.trim(strWithSpaces)
plot(close, title=trimmedStr)
```

### id

function:str.trim~2

## str.trim (function)

Removes whitespace from around a string and hands back the result.

It removes the white space that Unicode defines at both ends: spaces, tabs, line breaks and the other characters Unicode marks as white space.

### syntax

```
str.trim(simple string source) → simple string
```

### args

- `source`: simple string
  String to trim.
  types: simple string, input string, const string, literal string

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator("String Trim Example", overlay=false)
strWithSpaces = "GoCharting"
trimmedStr = str.trim(strWithSpaces)
plot(close, title=trimmedStr)
```

### id

function:str.trim~3

## str.trim (function)

Removes whitespace from around a string and hands back the result.

It removes the white space that Unicode defines at both ends: spaces, tabs, line breaks and the other characters Unicode marks as white space.

### syntax

```
str.trim(series string source) → series string
```

### args

- `source`: series string
  String to trim.
  types: series string, simple string, input string, const string, literal string

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("String Trim Example", overlay=false)
strWithSpaces = "GoCharting"
trimmedStr = str.trim(strWithSpaces)
plot(close, title=trimmedStr)
```

### id

function:str.trim~4

## str.upper (function)

Converts a string to upper case; the other half of the pair with str.lower.

It takes the string and nothing else.

### syntax

```
str.upper(const string source) → const string
```

### args

- `source`: const string
  String to be converted.
  types: const string, literal string

### returnedType

const string

### example

```lipi
//@lipi=2
indicator("str.upper Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=str.upper(syminfo.ticker))
}
```

### id

function:str.upper~1

## str.upper (function)

Converts a string to upper case; the other half of the pair with str.lower.

It takes the string and nothing else.

### syntax

```
str.upper(input string source) → input string
```

### args

- `source`: input string
  String to be converted.
  types: input string, const string, literal string

### returnedType

input string

### example

```lipi
//@lipi=2
indicator("str.upper Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=str.upper(syminfo.ticker))
}
```

### id

function:str.upper~2

## str.upper (function)

Converts a string to upper case; the other half of the pair with str.lower.

It takes the string and nothing else.

### syntax

```
str.upper(simple string source) → simple string
```

### args

- `source`: simple string
  String to be converted.
  types: simple string, input string, const string, literal string

### returnedType

simple string

### example

```lipi
//@lipi=2
indicator("str.upper Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=str.upper(syminfo.ticker))
}
```

### id

function:str.upper~3

## str.upper (function)

Converts a string to upper case; the other half of the pair with str.lower.

It takes the string and nothing else.

### syntax

```
str.upper(series string source) → series string
```

### args

- `source`: series string
  String to be converted.
  types: series string, simple string, input string, const string, literal string

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("str.upper Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=str.upper(syminfo.ticker))
}
```

### id

function:str.upper~4
