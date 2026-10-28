Contents: chart (library) · chart.bg_color (variable) · chart.fg_color (variable) · chart.is_heikinashi (variable) · chart.is_kagi (variable) · chart.is_linebreak (variable) · chart.is_pnf (variable) · chart.is_range (variable) · chart.is_renko (variable) · chart.is_standard (variable)

# chart

## chart (library)

Values that describe the chart the script is drawn on: its colours (`chart.bg_color` and `chart.fg_color`) and its type (`chart.is_standard`, `chart.is_heikinashi`, `chart.is_renko` and the other `chart.is_*` values).

### example

```lipi
//@lipi=2
indicator("chart Library Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=chart.is_standard ? "Standard chart" : "Synthetic bars", color=chart.bg_color, textcolor=chart.fg_color)
}
```

### id

library:chart

## chart.bg_color (variable)

The background colour of the chart the script is drawn on, as set by the reader.

### type

input color

### example

```lipi
//@lipi=2
indicator("chart.bg_color Example", overlay=true)
if barstate.islast {
    // A label that blends in with the chart background, with contrasting text
    label.new(bar_index, high, text="Close", color=chart.bg_color, textcolor=chart.fg_color)
}
```

### id

variable:chart.bg_color

## chart.fg_color (variable)

A foreground colour that contrasts with the chart's background, for text and lines that must stay readable on both light and dark charts.

### type

input color

### example

```lipi
//@lipi=2
indicator("chart.fg_color Example", overlay=true)
plot(talib.sma(close, 20), title="SMA", color=chart.fg_color)
```

### id

variable:chart.fg_color

## chart.is_heikinashi (variable)

True when the chart type is Heikin Ashi. Charts built from synthetic bars do not show the instrument's real open, high, low and close, so a script can use this to warn the reader or to adjust its calculations.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("chart.is_heikinashi Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=chart.is_heikinashi ? "heikinashi chart" : "Another chart type")
}
```

### id

variable:chart.is_heikinashi

## chart.is_kagi (variable)

True when the chart type is Kagi. Charts built from synthetic bars do not show the instrument's real open, high, low and close, so a script can use this to warn the reader or to adjust its calculations.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("chart.is_kagi Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=chart.is_kagi ? "kagi chart" : "Another chart type")
}
```

### id

variable:chart.is_kagi

## chart.is_linebreak (variable)

True when the chart type is Line Break. Charts built from synthetic bars do not show the instrument's real open, high, low and close, so a script can use this to warn the reader or to adjust its calculations.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("chart.is_linebreak Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=chart.is_linebreak ? "linebreak chart" : "Another chart type")
}
```

### id

variable:chart.is_linebreak

## chart.is_pnf (variable)

True when the chart type is Point & Figure. Charts built from synthetic bars do not show the instrument's real open, high, low and close, so a script can use this to warn the reader or to adjust its calculations.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("chart.is_pnf Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=chart.is_pnf ? "pnf chart" : "Another chart type")
}
```

### id

variable:chart.is_pnf

## chart.is_range (variable)

True when the chart type is Range. Charts built from synthetic bars do not show the instrument's real open, high, low and close, so a script can use this to warn the reader or to adjust its calculations.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("chart.is_range Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=chart.is_range ? "range chart" : "Another chart type")
}
```

### id

variable:chart.is_range

## chart.is_renko (variable)

True when the chart type is Renko. Charts built from synthetic bars do not show the instrument's real open, high, low and close, so a script can use this to warn the reader or to adjust its calculations.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("chart.is_renko Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=chart.is_renko ? "renko chart" : "Another chart type")
}
```

### id

variable:chart.is_renko

## chart.is_standard (variable)

True when the chart type is a standard chart type (candles, bars, line or area). Charts built from synthetic bars do not show the instrument's real open, high, low and close, so a script can use this to warn the reader or to adjust its calculations.

### type

simple bool

### example

```lipi
//@lipi=2
indicator("chart.is_standard Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text=chart.is_standard ? "standard chart" : "Another chart type")
}
```

### id

variable:chart.is_standard
