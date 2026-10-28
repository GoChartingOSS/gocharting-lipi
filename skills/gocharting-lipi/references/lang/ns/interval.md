Contents: interval (library) · interval.change (function) · interval.from_seconds (function) · interval.in_seconds (function) · interval.interval (variable) · interval.isdaily (variable) · interval.iseod (variable) · interval.ishourly (variable) · interval.isintraday (variable) · interval.isminutes (variable) · interval.ismonthly (variable) · interval.isseconds (variable) · interval.isweekly (variable) · interval.multiplier (variable) · interval.timeframe_minutes (variable)

# interval

## interval (library)

Eleven values describing the interval the chart is drawn on: the interval itself, its multiplier, its length in minutes, and eight booleans for what kind of interval it is.

Every one is simple rather than series, because the chart's interval does not change while a script runs.

### example

```lipi
//@lipi=2
indicator("interval Library Example", overlay=true)
if barstate.islast {
    kind = interval.isintraday ? "Intraday" : interval.isdaily ? "Daily" : "Weekly or longer"
    label.new(bar_index, high, text=kind + " chart, interval " + interval.interval)
}
```

### id

library:interval

## interval.change (function)

Returns true on the first bar of each new period of `interval`, for example on the first bar of every day when `interval` is "1D". Use it to reset values at the start of a larger period.

### syntax

```
interval.change(series string interval) → series bool
```

### args

- `interval`: series string
  Interval string: a count and a unit, such as "15m", "4h" or "1D", with the units `s`, `m`, `h`, `D`, `W` and `M`. For `D`, `W` and `M` the count must be 1. Any other string compiles and gives false.
  types: series string, simple string, input string, const string, literal string

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("interval.change Example", overlay=true)
static float dayHigh = na
if interval.change("1D") {
    dayHigh := high
} else {
    dayHigh := math.max(dayHigh, high)
}
plot(dayHigh, title="High of the Day", color=color.green)
```

### id

function:interval.change

## interval.from_seconds (function)

Returns the interval string for a length in seconds, rounded up to the next supported interval. It is not an exact inverse of `interval.in_seconds`.

The result is one of "5s", "10s", "15s", "30s", "45s", "1m", "3m", "5m", "10m", "15m", "30m", "1h", "2h", "4h", "1D", "1W", "1M", "3M", "6M" and "12M": 2 seconds gives "5s", 120 seconds gives "3m", 86400 gives "1D". 1 second or less gives "1s", and more than 31622400 seconds gives "12M". Exactly 1, 3, 6 or 12 times 2628003 seconds (the length of a month in `interval.in_seconds`) is read first as that many months (another multiple, such as 2 months, is rounded up: 5256006 gives "3M"), while the rounding table counts a month as 30 days, so 2592001 seconds gives "3M" but 2628003 gives "1M".

### syntax

```
interval.from_seconds(series int seconds) → series string
```

### args

- `seconds`: series int
  Length of the interval in seconds.
  types: series int, simple int, input int, const int, literal int

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("interval.from_seconds Example", overlay=true)
fourTimesChart = interval.from_seconds(interval.in_seconds() * 4)
if barstate.islast {
    label.new(bar_index, high, text="4x chart interval: " + fourTimesChart)
}
```

### id

function:interval.from_seconds

## interval.in_seconds (function)

Returns the length of `interval` in seconds, for example 86400 for "1D". With no argument it measures the chart's own interval.

### syntax

```
interval.in_seconds(series string interval) → series int
```

### args

- `interval?`: series string
  Interval string, for example "1D". Optional. The default is the chart's own interval.
  types: series string, simple string, input string, const string, literal string
  default: interval.interval

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("interval.in_seconds Example", overlay=false)
chartSeconds = interval.in_seconds()
// Bars per day on an intraday chart
plot(86400 / chartSeconds, title="Bars per Day", color=color.blue)
```

### id

function:interval.in_seconds

## interval.interval (variable)

The interval the chart is drawn on, as a string.

Every name in this namespace is simple, so the answer is the same on the first bar and on the last.

### type

simple string

### example

```lipi
//@lipi=2
indicator("Timeframe Example", overlay=true)
plot(interval.interval == "1D" ? 1 : 0, color=color.blue, title="Daily Timeframe Signal")
```

### id

variable:interval.interval

## interval.isdaily (variable)

True when the interval is daily.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("Timeframe is Daily Example", overlay=true)
bgcolor(interval.isdaily ? color.green : na)
```

### id

variable:interval.isdaily

## interval.iseod (variable)

True when the interval is an end-of-day interval: a day, a week or a month.

It is true whenever `interval.isdaily`, `interval.isweekly` or `interval.ismonthly` is true, so it is wider than `interval.isdaily`, which is true for day intervals only.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("Timeframe is DWM Example", overlay=true)
plot(interval.iseod ? 1 : 0, color=color.blue, title="DWM Timeframe Signal")
```

### id

variable:interval.iseod

## interval.ishourly (variable)

True when the interval is hourly.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("Interval Hourly Signal", overlay=true)
plot(interval.ishourly ? 1 : 0, color=color.green, title="Hourly Interval Signal")
```

### id

variable:interval.ishourly

## interval.isintraday (variable)

True when the chart's interval is intraday.

Eight of these booleans exist, one per kind of interval, and all eight are simple rather than series.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("Intraday Volume Example", overlay=false)
intradayVolume = interval.isintraday ? volume : na
plot(intradayVolume, color=color.blue, title="Intraday Volume")
```

### id

variable:interval.isintraday

## interval.isminutes (variable)

True when the interval is measured in minutes.

It is narrower than `interval.isintraday`: both can hold at once, so test the one that matches the question you are asking.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("Minutes Interval Check", overlay=true)
minCheck = interval.isminutes and close > open
plot(minCheck ? high : na, color=color.red, title="Bullish Candle on Minute Chart")
```

### id

variable:interval.isminutes

## interval.ismonthly (variable)

True when the interval is monthly.

Together with `interval.isweekly` and `interval.isdaily` it covers the intervals a script cannot treat as intraday.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("Monthly Interval Example", overlay=true)
monthlyclose = interval.ismonthly ? close : na
plot(monthlyclose, color=color.purple, title="Monthly High")
```

### id

variable:interval.ismonthly

## interval.isseconds (variable)

True when the chart's interval is measured in seconds.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("interval.isseconds Example", overlay=true)
bgcolor(interval.isseconds ? color.new(color.orange, 0.1) : na)
```

### id

variable:interval.isseconds

## interval.isweekly (variable)

True when the interval is weekly.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("Weekly Interval Example", overlay=false)
weeklyVolumeAvg = interval.isweekly ? talib.sma(volume, 4) : na
plot(weeklyVolumeAvg, color=color.orange, title="Weekly Avg Volume")
```

### id

variable:interval.isweekly

## interval.multiplier (variable)

The multiplier of the chart's interval, as a whole number.

Read it alongside `interval.interval` when you need the size of the interval rather than a yes-or-no answer about its kind.

### type

simple int

### example

```lipi
//@lipi=2
indicator("Interval Multiplier Example", overlay=true)
multipliedClose = close * interval.multiplier
plot(multipliedClose, color=color.blue, title="Close x Interval Multiplier")
```

### id

variable:interval.multiplier

## interval.timeframe_minutes (variable)

The chart's interval counted in minutes.

It is the one interval value you can compare arithmetically, which makes it the usual way to write "only on intervals shorter than an hour".

### type

simple int

### example

```lipi
//@lipi=2
indicator("interval.timeframe_minutes Example", overlay=false)
// Bars in a 6.5-hour trading day on an intraday chart
barsPerDay = 390 / interval.timeframe_minutes
plot(barsPerDay, title="Bars per Day", color=color.blue)
```

### id

variable:interval.timeframe_minutes
