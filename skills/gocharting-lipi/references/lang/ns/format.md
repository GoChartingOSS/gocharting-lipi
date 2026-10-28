Contents: format (library) · format.inherit (constant) · format.mintick (constant) · format.percent (constant) · format.price (constant) · format.volume (constant)

# format

## format (library)

Named formats for script values: `format.inherit`, `format.price`, `format.percent`, `format.volume` and `format.mintick`. Pass one to the `format` argument of `indicator`, `strategy` or `plot` to control how values appear on the price scale and in the status line.

### example

```lipi
//@lipi=2
indicator("format Library Example", overlay=false, format=format.percent)
changePct = (close - close[1]) / close[1] * 100
plot(changePct, title="Change %", color=color.blue)
```

### id

library:format

## format.inherit (constant)

A format for script values, for the `format` argument of `indicator` and `strategy`. Uses the format of the parent series: the price scale of the chart, or of the pane the script is drawn in. This is the default there. The plot functions (`plot`, `hline`, `plotarrow`, `plotchar`, `plotshape`) refuse it when the script is added to the chart: leave their `format` out.

### type

const string

### example

```lipi
//@lipi=2
indicator("format.inherit Example", overlay=false, format=format.inherit)
plot(talib.rsi(close, 14), title="RSI", color=color.blue)
```

### id

constant:format.inherit

## format.mintick (constant)

A format for script values, for the `format` argument of `str.tostring`. Shows values rounded to the instrument's minimum tick. `indicator`, `strategy` and the plot functions pass it in the editor's check but refuse it when the script is added to the chart.

### type

const string

### example

```lipi
//@lipi=2
indicator("format.mintick Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, str.tostring(close, format.mintick))
}
plot(close)
```

### id

constant:format.mintick

## format.percent (constant)

A format for script values, for the `format` argument of `indicator`, `strategy` and the plot functions (`plot`, `hline`, `plotarrow`, `plotchar`, `plotshape`). Shows values as percentages, with a % sign.

### type

const string

### example

```lipi
//@lipi=2
indicator("format.percent Example", overlay=false, format=format.percent)
plot(talib.rsi(close, 14), title="RSI", color=color.blue)
```

### id

constant:format.percent

## format.price (constant)

A format for script values, for the `format` argument of `indicator`, `strategy` and the plot functions (`plot`, `hline`, `plotarrow`, `plotchar`, `plotshape`). Shows values as prices, with as many decimals as the instrument's price scale.

### type

const string

### example

```lipi
//@lipi=2
indicator("format.price Example", overlay=false, format=format.price)
plot(talib.rsi(close, 14), title="RSI", color=color.blue)
```

### id

constant:format.price

## format.volume (constant)

A format for script values, for the `format` argument of `indicator`, `strategy` and the plot functions (`plot`, `hline`, `plotarrow`, `plotchar`, `plotshape`). Shows values as volume, abbreviating large numbers (for example 5.2K or 1.3M).

### type

const string

### example

```lipi
//@lipi=2
indicator("format.volume Example", overlay=false, format=format.volume)
plot(volume, title="Volume", color=color.blue, style=plotStyle.histogram)
```

### id

constant:format.volume
