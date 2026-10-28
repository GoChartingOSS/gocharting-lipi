Contents: talib (library) · talib.alma (function) · talib.atr (function) · talib.barssince (function) · talib.bb (function) · talib.bbw (function) · talib.cci (function) · talib.change (function) · talib.change (function) · talib.change (function) · talib.cmo (function) · talib.cog (function) · talib.correlation (function) · talib.cross (function) · talib.crossover (function) · talib.crossunder (function) · talib.cum (function) · talib.dc (function) · talib.dcw (function) · talib.dev (function) · talib.dmi (function) · talib.ema (function) · talib.falling (function) · talib.highest (function) · talib.highestbars (function) · talib.hma (function) · talib.kc (function) · talib.kcw (function) · talib.linreg (function) · talib.lowest (function) · talib.lowestbars (function) · talib.macd (function) · talib.median (function) · talib.mfi (function) · talib.mode (function) · talib.nvi (function) · talib.obv (function) · talib.percentile_linear_interpolation (function) · talib.percentile_nearest_rank (function) · talib.percentrank (function) · talib.pivothigh (function) · talib.pivotlow (function) · talib.psar (function) · talib.pvi (function) · talib.pvt (function) · talib.range (function) · talib.rising (function) · talib.rma (function) · talib.roc (function) · talib.rsi (function) · talib.sma (function) · talib.stdev (function) · talib.stoch (function) · talib.sum (function) · talib.supertrend (function) · talib.swma (function) · talib.tr (function) · talib.tsi (function) · talib.valuewhen (function) · talib.variance (function) · talib.vwap (function) · talib.vwma (function) · talib.wma (function) · talib.wpr (function) · talib.wvad (function)

# talib

## talib (library)

Sixty-two named indicator and series functions: moving averages, oscillators, channels, ranges, pivots, window statistics and the volume indices.

Some take a `source` and a `length`; several — the volume indices, the true-range and channel functions among them — take no source and read the chart's own bars instead.

### example

```lipi
//@lipi=2
indicator("talib Library Example", overlay=true)
fast = talib.ema(close, 12)
slow = talib.ema(close, 26)
rsi = talib.rsi(close, 14)
plot(fast, title="Fast EMA", color=color.green)
plot(slow, title="Slow EMA", color=color.red)
plotshape(talib.crossover(fast, slow) and rsi < 70, title="Buy", location=location.belowbar, shape=shape.triangleup, color=color.green)
```

### id

library:talib

## talib.alma (function)

An Arnaud Legoux moving average of `source` over `length` bars.

Two further arguments, `offset` and `sigma`, shape the weighting. Both accept an int or a float.

### syntax

```
talib.alma(series float source, series int length, series float offset, series float sigma) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int
- `offset`: series float
  Controls tradeoff between smoothness (closer to 1) and responsiveness (closer to 0).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `sigma`: series float
  Changes the smoothness of ALMA. The larger sigma the smoother ALMA.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("ALMA vs EMA", overlay=true)
length = input(20, title="Moving Average Length")
almaLine = talib.alma(close, length, 0.85, 6)
emaLine = talib.ema(close, length)
plot(almaLine, color=color.blue, title="ALMA", linewidth=2)
plot(emaLine, color=color.red, title="EMA", linewidth=2)
```

### id

function:talib.alma

## talib.atr (function)

Average true range over `length` bars. Read it as a measure of how far the market has been travelling, not as a price level.

There is no `source` argument. The reading is built from the chart's own bars.

### syntax

```
talib.atr(series int length) → series float
```

### args

- `length`: series int
  Length (number of bars back).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("ATR Indicator", overlay=false)
// Define ATR length
atrLength = input(14, title="ATR Length")
// Calculate ATR
atrValue = talib.atr(atrLength)
// Plot ATR
plot(atrValue, color=color.blue, title="ATR", linewidth=2)
```

### id

function:talib.atr

## talib.barssince (function)

Counts the bars that have gone by since `condition` was last true.

`condition` may be a bool, an int or a float expression; a number counts as true when it is not zero. The result is -1, not `na`, when the condition has not been true on any bar so far or is `na`.

### syntax

```
talib.barssince(series bool condition) → series int
```

### args

- `condition`: series bool
  The condition to check for.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Last Breakout Marker", overlay=true)
// Define breakout condition
breakout = close > talib.highest(low, 20)
// Get bars since last breakout
barsSinceBreakout = talib.barssince(breakout)
// Mark breakout bar with an arrow
plotshape(barsSinceBreakout == 0, location=location.abovebar, color=color.green, shape=shape.square, title="Breakout")
```

### id

function:talib.barssince

## talib.bb (function)

Bollinger bands for `source` over `length` bars, with `mult` setting how far the outer bands sit from the middle one.

`mult` is a float series, so whole numbers and values such as `2.5` are both valid.

### syntax

```
talib.bb(series float source, series int length, series float mult) → [series float, series float, series float]
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int
- `mult`: series float
  Standard deviation factor.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

[series float, series float, series float]

### returns

- `middle`: series float
  Middle band.
- `upper`: series float
  Upper band.
- `lower`: series float
  Lower band.

### example

```lipi
//@lipi=2
indicator("Bollinger Bands", overlay=true)
// User inputs
length = input.int(20, title="BB Length")
mult = input.float(2.5, title="BB Multiplier")
// Calculate Bollinger Bands
[bbMiddle, bbUpper, bbLower] = talib.bb(close, length, mult)
// Plot the bands
plot(bbMiddle, title="BB Middle", color=color.blue)
plot(bbUpper, title="BB Upper", color=color.green)
plot(bbLower, title="BB Lower", color=color.red)
```

### id

function:talib.bb

## talib.bbw (function)

Bollinger band width: the same calculation as `talib.bb`, delivered as one number instead of three bands.

Its arguments match `talib.bb` exactly, including `mult` as a float series.

### syntax

```
talib.bbw(series float source, series int length, series float mult) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int
- `mult`: series float
  Standard deviation factor.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### notes

- A length above 500 bars passes the editor's check but is refused when the script is added to the chart, with "The script is trying to access historical data outside allowed range (501). The allowed range is 0 to 500." (for 501). Other `ta` functions accept such a length when compiled and stop when the script runs.

### example

```lipi
//@lipi=2
indicator("Bollinger Band Width (BBW)", overlay=false)
length = input.int(20, title="Length")
mult = input.int(2, title="Multiplier")
[middle, upper, lower] = talib.bb(close, length, mult)
bbw = (upper - lower) / middle
plot(bbw, title="BBW", color=color.blue)
hline(0.5, "0.5 Line", color=color.gray)
```

### id

function:talib.bbw

## talib.cci (function)

Commodity Channel Index for `source` over `length` bars.

The source is an argument rather than a fixed price, so the index can be run on anything a script computes.

### syntax

```
talib.cci(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("CCI Indicator", overlay=false)
// User inputs
length = input(20, title="CCI Length")
// Compute CCI
cciValue = talib.cci(close, length)
// Plot CCI
plot(cciValue, title="CCI", color=color.blue, linewidth=2)
// Overbought/Oversold Levels
hline(100, "Overbought", color=color.green)
hline(0, "Neutral", color=color.gray)
hline(-100, "Oversold", color=color.red)
```

### id

function:talib.cci

## talib.change (function)

The difference between the current value of `source` and its value `length` bars back.

Three overloads exist, one each for an int, a float and a bool source, and the returned type follows the source you pass. `length` is optional in all three.

### syntax

```
talib.change(series int source, series int length) → series int
```

### args

- `source`: series int
  Source series.
  types: series int, simple int, input int, const int, literal int
- `length?`: series int
  How far the past source value is offset from the current one, in bars. Optional. The default is 1.
  types: series int, simple int, input int, const int, literal int
  default: 1

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Price Change", overlay=false)
// User input for change period
length = input(1, title="Change Period")
// Calculate price change
priceChange = talib.change(close, length)
// Plot price change
plot(priceChange, title="Price Change", color=color.blue, linewidth=2, style=plotStyle.histogram)
```

### id

function:talib.change~1

## talib.change (function)

The difference between the current value of `source` and its value `length` bars back.

Three overloads exist, one each for an int, a float and a bool source, and the returned type follows the source you pass. `length` is optional in all three.

### syntax

```
talib.change(series float source, series int length) → series float
```

### args

- `source`: series float
  Source series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length?`: series int
  How far the past source value is offset from the current one, in bars. Optional. The default is 1.
  types: series int, simple int, input int, const int, literal int
  default: 1

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Price Change", overlay=false)
// User input for change period
length = input(1, title="Change Period")
// Calculate price change
priceChange = talib.change(close, length)
// Plot price change
plot(priceChange, title="Price Change", color=color.blue, linewidth=2, style=plotStyle.histogram)
```

### id

function:talib.change~2

## talib.change (function)

The difference between the current value of `source` and its value `length` bars back.

Three overloads exist, one each for an int, a float and a bool source, and the returned type follows the source you pass. `length` is optional in all three.

### syntax

```
talib.change(series bool source, series int length) → series bool
```

### args

- `source`: series bool
  Source series.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
- `length?`: series int
  How far the past source value is offset from the current one, in bars. Optional. The default is 1.
  types: series int, simple int, input int, const int, literal int
  default: 1

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("Price Change", overlay=false)
// User input for change period
length = input(1, title="Change Period")
// Calculate price change
priceChange = talib.change(close, length)
// Plot price change
plot(priceChange, title="Price Change", color=color.blue, linewidth=2, style=plotStyle.histogram)
```

### id

function:talib.change~3

## talib.cmo (function)

Chande Momentum Oscillator for `source` over `length` bars.

Two arguments in, one series float out — the same call shape as `talib.rsi`.

### syntax

```
talib.cmo(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Chande Momentum Oscillator (CMO)", overlay=false)
// User input
length = input(14, title="CMO Length")
// Calculate CMO
cmoValue = talib.cmo(close, length)
// Plot CMO
plot(cmoValue, title="CMO", color=color.blue, linewidth=2)
// Overbought/Oversold Levels
hline(50, "Overbought", color=color.green)
hline(0, "Neutral", color=color.gray)
hline(-50, "Oversold", color=color.red)
```

### id

function:talib.cmo

## talib.cog (function)

Centre of gravity of `source` across a window of `length` bars.

### syntax

```
talib.cog(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Center of Gravity (COG)", overlay=false)
// Input length for calculation
length = input(10, title="COG Length")
// Compute the COG value
cogValue = talib.cog(close, length)
// Plot the COG line
plot(cogValue, title="COG", color=color.blue, linewidth=2)
```

### id

function:talib.cog

## talib.correlation (function)

Correlation between two series, `source1` and `source2`, measured over `length` bars.

Both series are ordinary arguments, so you can correlate anything a script can compute — not only prices.

### syntax

```
talib.correlation(series float source1, series float source2, series int length) → series float
```

### args

- `source1`: series float
  Source series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `source2`: series float
  Target series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
   Length (number of bars back).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Price-Volume Correlation", overlay=false)
// Input for correlation period
length = input(20, title="Correlation Length")
// Calculate correlation between closing price and volume
correlationValue = talib.correlation(close, volume, length)
// Plot correlation value
plot(correlationValue, title="Price-Volume Correlation", color=color.blue, linewidth=2)
// Add reference levels
hline(1, "Perfect Positive", color=color.green)
hline(0, "No Correlation", color=color.gray)
hline(-1, "Perfect Negative", color=color.red)
```

### id

function:talib.correlation

## talib.cross (function)

True on a bar where `source1` and `source2` cross, in either direction.

When the direction of the cross matters, reach for `talib.crossover` or `talib.crossunder` instead.

### syntax

```
talib.cross(series float source1, series float source2) → series bool
```

### args

- `source1`: series float
  First data series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `source2`: series float
  Second data series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("MACD Crossover Strategy", overlay=true)
// MACD parameters
fastLength = input(12, title="Fast EMA Length")
slowLength = input(26, title="Slow EMA Length")
signalSmoothing = input(9, title="Signal Smoothing")
// Compute MACD components
[macdLine, signalLine, _] = talib.macd(close, fastLength, slowLength, signalSmoothing)
// Detect crossovers
bullishCrossover = talib.cross(macdLine, signalLine)
bearishCrossover = talib.cross(signalLine, macdLine)
// Plot Buy and Sell signals
plotshape(bullishCrossover, location=location.belowbar, color=color.green, shape=shape.labelup, title="Buy Signal")
plotshape(bearishCrossover, location=location.abovebar, color=color.red, shape=shape.labeldown, title="Sell Signal")
```

### id

function:talib.cross

## talib.crossover (function)

Flags the bar on which `source1` crosses above `source2`. Crosses the other way are ignored.

### syntax

```
talib.crossover(series float source1, series float source2) → series bool
```

### args

- `source1`: series float
  First data series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `source2`: series float
  Second data series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("Crossover Example", overlay=true)
length1 = input.int(10, title="Fast MA Length")
length2 = input.int(20, title="Slow MA Length")
fastMA = talib.sma(close, length1)
slowMA = talib.sma(close, length2)
crossover = talib.crossover(fastMA, slowMA)
crossunder = talib.crossunder(fastMA, slowMA)
plot(fastMA, color=color.blue, title="Fast MA")
plot(slowMA, color=color.red, title="Slow MA")
plotshape(crossover, title="Crossover", location=location.belowbar, color=color.green, shape=shape.triangleup, size=size.small)
plotshape(crossunder, title="Crossunder", location=location.abovebar, color=color.red, shape=shape.triangledown, size=size.small)
```

### id

function:talib.crossover

## talib.crossunder (function)

The mirror of `talib.crossover`: true on the bar where `source1` crosses below `source2`.

### syntax

```
talib.crossunder(series float source1, series float source2) → series bool
```

### args

- `source1`: series float
  First data series
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `source2`: series float
  Second data series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("Crossunder Example", overlay=true)
fastMA = talib.sma(close, 10)
slowMA = talib.sma(close, 20)
crossunderSignal = talib.crossunder(fastMA, slowMA)
plot(fastMA, color=color.blue, title="Fast MA")
plot(slowMA, color=color.red, title="Slow MA")
plotshape(crossunderSignal, location=location.abovebar, color=color.red, shape=shape.triangledown, title="Crossunder")
```

### id

function:talib.crossunder

## talib.cum (function)

Accumulates `source` as the script advances through the chart.

There is no `length` argument: this is a running total rather than a moving window. For a window, use `talib.sum`.

### syntax

```
talib.cum(series float source) → series float
```

### args

- `source`: series float
  Source used for the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Cumulative Sum Example", overlay=false)
// Define input source
src = close
// Compute cumulative sum
cumulative_sum = talib.cum(src)
// Plot the result
plot(cumulative_sum, title="Cumulative Sum", color=color.blue)
```

### id

function:talib.cum

## talib.dc (function)

Donchian channel over `length` bars.

`length` is the only argument. The channel is taken from the chart's own bars rather than from a series you supply.

### syntax

```
talib.dc(series int length) → [series float, series float, series float]
```

### args

- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

[series float, series float, series float]

### returns

- `middle`: series float
  Middle line: halfway between the upper and the lower band.
- `upper`: series float
  Upper band: the highest high over `length` bars.
- `lower`: series float
  Lower band: the lowest low over `length` bars.

### notes

- The values come in the order middle, upper, lower, as with `talib.bb`. Bind them in that order: the compiler cannot tell a wrong order, so a script that swaps them compiles and plots the wrong band.

### example

```lipi
//@lipi=2
indicator("talib.dc Example", overlay=true)
[dcMiddle, dcUpper, dcLower] = talib.dc(20)
plot(dcUpper, title="Upper", color=color.green)
plot(dcMiddle, title="Middle", color=color.gray)
plot(dcLower, title="Lower", color=color.red)
```

### id

function:talib.dc

## talib.dcw (function)

Donchian channel width over `length` bars, as a single figure.

Where `talib.dc` gives you the channel, this gives you how wide it is.

### syntax

```
talib.dcw(series int length) → series float
```

### args

- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("talib.dcw Example", overlay=false)
width = talib.dcw(20)
plot(width, title="Donchian Channel Width", color=color.blue)
```

### id

function:talib.dcw

## talib.dev (function)

A deviation measure for `source` over `length` bars.

It is not the same function as `talib.stdev`.

### syntax

```
talib.dev(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Standard Deviation Example", overlay=false)
// Define input source and period
src = close
length = 20
// Compute standard deviation
std_dev = talib.dev(src, length)
// Plot the result
plot(std_dev, title="Standard Deviation", color=color.red)
```

### id

function:talib.dev

## talib.dmi (function)

The directional movement family in one call, calculated from the chart's own bars.

It takes two lengths rather than one: `diLength` for the directional readings and `adxSmoothing` for the strength reading built on them.

### syntax

```
talib.dmi(series int diLength, series int adxSmoothing) → [series float, series float, series float]
```

### args

- `diLength`: series int
  DI Period.
  types: series int, simple int, input int, const int, literal int
- `adxSmoothing`: series int
  ADX Smoothing Period.
  types: series int, simple int, input int, const int, literal int

### returnedType

[series float, series float, series float]

### returns

- `plusDI`: series float
  The +DI reading.
- `minusDI`: series float
  The -DI reading.
- `adx`: series float
  The ADX reading, the strength reading built on the directional readings.

### example

```lipi
//@lipi=2
indicator("DMI Example", overlay=false)
// Define input length and smoothing factor
length = 14
smoothing = 14
// Compute DMI values
[plusDI, minusDI, adx] = talib.dmi(length, smoothing)
// Plot the results
plot(plusDI, title="+DI", color=color.green)
plot(minusDI, title="-DI", color=color.red)
plot(adx, title="ADX", color=color.blue)
```

### id

function:talib.dmi

## talib.ema (function)

Exponential moving average of `source` over `length` bars, weighted so that recent bars count for more than older ones.

It takes the same two arguments as `talib.sma`, so swapping one for the other is a one-word change.

### syntax

```
talib.ema(series float source, series int length) → series float
```

### args

- `source`: series float
   Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### notes

- A length above 500 bars passes the editor's check but is refused when the script is added to the chart, with "The script is trying to access historical data outside allowed range (501). The allowed range is 0 to 500." (for 501). Other `ta` functions accept such a length when compiled and stop when the script runs.

### example

```lipi
//@lipi=2
indicator("EMA Example", overlay=true)
// Define input source and period
src = close
length = 20
// Compute EMA
ema_line = talib.ema(src, length)
// Plot the EMA
plot(ema_line, title="EMA 20", color=color.blue)
```

### id

function:talib.ema

## talib.falling (function)

Asks the same question as `talib.rising` in the other direction: has `source` been falling across `length` bars?

The answer is a bool, not a number.

### syntax

```
talib.falling(series float source, series int length) → series bool
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("Falling Example", overlay=true)
// Define input source and period
src = close
length = 5
// Compute falling condition
is_falling = talib.falling(src, length)
// Plot background color if falling
bgcolor(is_falling ? color.red : na)
```

### id

function:talib.falling

## talib.highest (function)

The highest value `source` reached in the last `length` bars.

Any series can be passed, so this is not limited to the bar's high.

### syntax

```
talib.highest(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Highest Example", overlay=true)
// Define input source and period
src = high
length = 10
// Compute highest value
highest_value = talib.highest(src, length)
// Plot the highest value as a horizontal line
plot(highest_value, title="Highest 10 Bars", color=color.green)
```

### id

function:talib.highest

## talib.highestbars (function)

Locates the highest value of `source` within the last `length` bars and returns its position rather than its value.

It returns a series int, which makes it the companion to `talib.highest`.

### syntax

```
talib.highestbars(series float source, series int length) → series int
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Highest Bars Example", overlay=true)
// Define input source and period
src = high
length = 20
// Compute the number of bars ago the highest value occurred
bars_since_highest = talib.highestbars(src, length)
// Mark the highest point with a plot shape
plotshape(bars_since_highest == 0, location=location.abovebar, color=color.green, shape=shape.circle, title="Highest")
```

### id

function:talib.highestbars

## talib.hma (function)

Hull moving average of `source` over `length` bars.

### syntax

```
talib.hma(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("HMA Example", overlay=true)
// Define input source and period
src = close
length = 20
// Compute Hull Moving Average
hma_line = talib.hma(src, length)
// Plot the HMA
plot(hma_line, title="HMA 20", color=color.blue)
```

### id

function:talib.hma

## talib.kc (function)

Keltner channels for `source` over `length` bars, with `mult` setting the distance to the outer bands.

An optional `useTrueRange` flag selects true range for the width calculation. `mult` is a float series, like `talib.bb` and `talib.supertrend`'s `multiplier`.

### syntax

```
talib.kc(series float source, series int length, series float mult, series bool useTrueRange) → [series float, series float, series float]
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int
- `mult`: series float
  Multiplier of the average range. The upper and lower bands lie `mult` times the exponential moving average of the range, over `length` bars, above and below the middle line, which is the exponential moving average of `source`. The range is the true range, or `high - low` when `useTrueRange` is false.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `useTrueRange?`: series bool
  Selects true range for the width calculation. Optional.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: true

### returnedType

[series float, series float, series float]

### returns

- `middle`: series float
  Middle line: the moving average of `source`.
- `upper`: series float
  Upper band.
- `lower`: series float
  Lower band.

### notes

- The values come in the order middle, upper, lower, as with `talib.bb`. Bind them in that order: the compiler cannot tell a wrong order, so a script that swaps them compiles and plots the wrong band.
- A length above 500 bars passes the editor's check but is refused when the script is added to the chart, with "The script is trying to access historical data outside allowed range (501). The allowed range is 0 to 500." (for 501), because the middle line is an `ema`. (2.7: FACTS F-218; probes MF-645-C to MF-648-C; source ema.go:52-55.)

### example

```lipi
//@lipi=2
indicator("Keltner Channels", overlay=true)
length = input.int(20, "Length")
mult = input.float(1.5, "Multiplier")
[kcMiddle, kcUpper, kcLower] = talib.kc(close, length, mult)
plot(kcUpper, color=color.blue, title="Upper KC")
plot(kcMiddle, color=color.gray, title="Middle KC")
plot(kcLower, color=color.red, title="Lower KC")
```

### id

function:talib.kc

## talib.kcw (function)

Keltner channel width for `source` over `length` bars: one figure in place of the three the channel call returns.

The argument list matches `talib.kc`, `useTrueRange` included.

The width is the distance between the upper and the lower band divided by the middle line.

### syntax

```
talib.kcw(series float source, series int length, series float mult, series bool useTrueRange) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int
- `mult`: series float
  Multiplier of the average range. The bands lie `mult` times the exponential moving average of the range, over `length` bars, above and below the middle line, which is the exponential moving average of `source`. The range is the true range, or `high - low` when `useTrueRange` is false.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `useTrueRange?`: series bool
  Selects true range for the width calculation. Optional.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: true

### returnedType

series float

### notes

- A length above 500 bars passes the editor's check but is refused when the script is added to the chart, with "The script is trying to access historical data outside allowed range (501). The allowed range is 0 to 500." (for 501). Other `ta` functions accept such a length when compiled and stop when the script runs.

### example

```lipi
//@lipi=2
indicator("Keltner Channel Width (KCW)", overlay=false)
length = input(20, "Length")
mult = input(2, "Multiplier")
source = input(close, "Source")
kcWidth = talib.kcw(source, length, mult)
plot(kcWidth, color=color.blue, title="KC Width", style=plotStyle.histogram)
hline(0, "Zero Line", color=color.gray)
```

### id

function:talib.kcw

## talib.linreg (function)

Fits a linear regression to `source` across `length` bars and returns a value from that fit.

The `offset` argument shifts which point of the fit you get back.

### syntax

```
talib.linreg(series float source, series int length, series int offset) → series float
```

### args

- `source`: series float
  Source series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int
- `offset`: series int
  Offset.'
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Linear Regression Line", overlay=true)
length = input(20, "Length")
source = input(close, "Source")
offset = input(0, "Offset")
linreg = talib.linreg(source, length, offset)
plot(linreg, color=color.blue, title="Linear Regression")
```

### id

function:talib.linreg

## talib.lowest (function)

The lowest value `source` reached in the last `length` bars.

It is the counterpart of `talib.highest` and takes the same two arguments.

### syntax

```
talib.lowest(series float source, series int length) → series float
```

### args

- `source`: series float
   Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Lowest Low", overlay=true)
length = input(20, "Length")
lowestLow = talib.lowest(low, length)
plot(lowestLow, color=color.red, title="Lowest Low")
```

### id

function:talib.lowest

## talib.lowestbars (function)

Gives the position of the lowest value of `source` within the last `length` bars, not the value itself.

Use `talib.lowest` when you want the value.

### syntax

```
talib.lowestbars(series float source, series int length) → series int
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars back.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Lowest Bars Ago", overlay=true)
length = input(20, "Lookback Period")
barsAgo = talib.lowestbars(low, length)
lowestLow = talib.lowest(low, length)
plotshape(barsAgo == 0, location=location.belowbar, color=color.red, shape=shape.labeldown, title="Lowest Low")
plot(lowestLow, color=color.blue, title="Lowest Low")
```

### id

function:talib.lowestbars

## talib.macd (function)

Moving average convergence/divergence for `source`, from three lengths: `fastlen`, `slowlen` and `siglen`.

One call covers the whole study, including the signal line that `siglen` sizes.

### syntax

```
talib.macd(series float source, series int fastlen, series int slowlen, series int siglen) → [series float, series float, series float]
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `fastlen`: series int
  Fast Length parameter.
  types: series int, simple int, input int, const int, literal int
- `slowlen`: series int
  Slow Length parameter.
  types: series int, simple int, input int, const int, literal int
- `siglen`: series int
  Signal Length parameter.
  types: series int, simple int, input int, const int, literal int

### returnedType

[series float, series float, series float]

### returns

- `macdLine`: series float
  The MACD line.
- `signalLine`: series float
  The signal line, sized by `siglen`.
- `hist`: series float
  The histogram.

### notes

- A length above 500 bars passes the editor's check but is refused when the script is added to the chart, with "The script is trying to access historical data outside allowed range (501). The allowed range is 0 to 500." (for 501). Other `ta` functions accept such a length when compiled and stop when the script runs.

### example

```lipi
//@lipi=2
indicator("MACD (TA-Lib)", overlay=false)
shortLength = input(12, "Short EMA")
longLength = input(26, "Long EMA")
signalSmoothing = input(9, "Signal Smoothing")
source = input(close, "Source")
[macdLine, signalLine, hist] = talib.macd(source, shortLength, longLength, signalSmoothing)
plot(macdLine, color=color.blue, title="MACD Line")
plot(signalLine, color=color.red, title="Signal Line")
histColor = hist >= 0 ? color.green : color.red
plot(hist, color=histColor, style=plotStyle.histogram, title="Histogram")
```

### id

function:talib.macd

## talib.median (function)

The middle value of the last `length` values of `source`.

It sits alongside `talib.mode` and the two percentile functions: all four summarise a window of values rather than average it.

### syntax

```
talib.median(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Median Price", overlay=true)
length = input(20, "Lookback Period")
source = input(close, "Source")
medianPrice = talib.median(source, length)
plot(medianPrice, color=color.blue, title="Median Price")
```

### id

function:talib.median

## talib.mfi (function)

Money Flow Index for `source` over `length` bars.

There is no volume argument in the signature.

### syntax

```
talib.mfi(series float source, series int length) → series float
```

### args

- `source`: series float
   Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Money Flow Index (MFI)", overlay=false)
length = input(14, "MFI Length")
seres = input(close,"Series")
mfi = talib.mfi(seres, length)
plot(mfi, color=color.blue, title="MFI")
hline(80, "Overbought", color=color.red)
hline(20, "Oversold", color=color.green)
```

### id

function:talib.mfi

## talib.mode (function)

Of the last `length` values of `source`, this reports the one that recurs most often.

It is a statistical mode over a moving window, and it returns a series float like the other window functions here.

### syntax

```
talib.mode(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Length (number of bars back).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Mode of Close Price", overlay=true)
length = input(20, "Lookback Period")
modePrice = talib.mode(close, length)
plot(modePrice, color=color.blue, title="Mode Price")
```

### id

function:talib.mode

## talib.nvi (function)

Negative volume index for the chart's bars.

It takes no arguments at all.

### syntax

```
talib.nvi() → series float
```

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("talib.nvi Example", overlay=false)
nvi = talib.nvi()
plot(nvi, title="NVI", color=color.blue)
plot(talib.ema(nvi, 255), title="NVI Signal", color=color.orange)
```

### id

function:talib.nvi

## talib.obv (function)

On-balance volume for the chart's bars.

Like the other volume indices in this namespace, it is called with an empty argument list.

### syntax

```
talib.obv() → series float
```

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("talib.obv Example", overlay=false)
obv = talib.obv()
plot(obv, title="On-Balance Volume", color=color.blue)
plot(talib.sma(obv, 20), title="OBV SMA", color=color.orange)
```

### id

function:talib.obv

## talib.percentile_linear_interpolation (function)

The requested `percentile` of `source` over `length` bars, interpolating between the two values that straddle the rank.

Because it interpolates, the result need not be a value that actually occurred in the window.

### syntax

```
talib.percentile_linear_interpolation(series float source, series int length, series float percentile) → series float
```

### args

- `source`: series float
  Series of values to process (source).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
   Number of bars back (length).
  types: series int, simple int, input int, const int, literal int
- `percentile`: series float
  Percentage, a number from range 0..100.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("talib.percentile_linear_interpolation Example", overlay=true)
p90 = talib.percentile_linear_interpolation(close, 50, 90)
p10 = talib.percentile_linear_interpolation(close, 50, 10)
plot(p90, title="90th Percentile", color=color.green)
plot(p10, title="10th Percentile", color=color.red)
```

### id

function:talib.percentile_linear_interpolation

## talib.percentile_nearest_rank (function)

Takes the requested `percentile` of `source` over `length` bars at the nearest rank, without interpolating.

The result is therefore one of the values in the window. Where you would rather have a smoother figure, use the linear-interpolation function.

### syntax

```
talib.percentile_nearest_rank(series float source, series int length, series float percentile) → series float
```

### args

- `source`: series float
  Series of values to process (source).
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
   Number of bars back (length).
  types: series int, simple int, input int, const int, literal int
- `percentile`: series float
  Percentage, a number from range 0..100.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Percentile Linear Interpolation", overlay=true)
length = input(20, "Lookback Period")
percentile = input(75, "Percentile")
source = input(hlc3, "Source")
percentileValue = talib.percentile_linear_interpolation(source, length, percentile)
plot(percentileValue, color=color.blue, title="75th Percentile", linewidth=2)
plot(close, color=color.gray, style=plotStyle.scatter, title="Price")
plot(percentileValue, color=color.blue, title="75th Percentile")
```

### id

function:talib.percentile_nearest_rank

## talib.percentrank (function)

Ranks where `source` now stands against the last `length` bars of itself.

It answers the question the other way round from the percentile functions: they take a rank and give a value, this takes the value and gives its rank.

### syntax

```
talib.percentrank(series float source, series int length) → series float
```

### args

- `source`: series float
   Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Percent Rank", overlay=false)
length = input(20, "Lookback Period")
source = input(close, "Source")
percentRank = talib.percentrank(source, length) * 100
plot(percentRank, color=color.blue, title="Percent Rank")
hline(80, "Overbought", color=color.red)
hline(20, "Oversold", color=color.green)
```

### id

function:talib.percentrank

## talib.pivothigh (function)

Looks for a pivot high in `source`, as this build implements it. On each bar it takes the last `leftBars + rightBars - 1` bars of `source`, the current bar included. When the highest value in that window is `leftBars` bars back, it returns the current bar's `source`; otherwise it returns `na`.

This is not a conventional pivot test. The value returned is the current bar's, not the pivot bar's, and with `rightBars` = 1 the window is too short for the highest value ever to be `leftBars` bars back, so the result is always `na`. `source` is optional; the two bar counts are not.

### syntax

```
talib.pivothigh(series float source, series int leftBars, series int rightBars) → series float
```

### args

- `source?`: series float
  Series to read. The default is `close`. It is the first argument: to leave it out, pass `leftBars` and `rightBars` by name.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: close
- `leftBars`: series int
  Left strength.
  types: series int, simple int, input int, const int, literal int
- `rightBars`: series int
  Right strength.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Pivot Highs", overlay=true)
leftBars = input(5, "Left Bars")
rightBars = input(5, "Right Bars")
pivotHigh = talib.pivothigh(high, leftBars, rightBars)
plot(pivotHigh, style=plotStyle.scatter, color=color.red, title="Pivot Highs", offset=-rightBars)
```

### id

function:talib.pivothigh

## talib.pivotlow (function)

Looks for a pivot low in `source`, as this build implements it. On each bar it takes the last `leftBars + rightBars - 1` bars of `source`, the current bar included. When the lowest value in that window is `leftBars` bars back, it returns the current bar's `source`; otherwise it returns `na`.

This is not a conventional pivot test. The value returned is the current bar's, not the pivot bar's, and with `rightBars` = 1 the window is too short for the lowest value ever to be `leftBars` bars back, so the result is always `na`. `source` is optional; the two bar counts are not.

### syntax

```
talib.pivotlow(series float source, series int leftBars, series int rightBars) → series float
```

### args

- `source?`: series float
  Series to read. The default is `close`. It is the first argument: to leave it out, pass `leftBars` and `rightBars` by name.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: close
- `leftBars`: series int
   Left strength.
  types: series int, simple int, input int, const int, literal int
- `rightBars`: series int
  Right strength.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Pivot Lows", overlay=true)
leftBars = input(5, "Left Bars")
rightBars = input(5, "Right Bars")
pivotLow = talib.pivotlow(low, leftBars, rightBars)
plot(pivotLow, style=plotStyle.cross, color=color.green, title="Pivot Lows", offset=-rightBars)
```

### id

function:talib.pivotlow

## talib.psar (function)

Parabolic SAR, controlled by three numbers rather than a bar count: where the calculation starts, how much it moves on each step, and how far it is allowed to go.

All three accept an int or a float.

### syntax

```
talib.psar(series float start, series float step, series float max_step) → series float
```

### args

- `start`: series float
  This is the initial acceleration factor
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `step`: series float
  This is the amount by which the acceleration factor increases each time the trend continues in the same direction.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `max_step`: series float
  This is the maximum value the acceleration factor can reach
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Parabolic SAR (PSAR)", overlay=true)
start = input.float(0.02, title="Start", minval=0.01)
stepInc = input.float(0.02, title="Step", minval=0.01)
max_step = input.float(0.2, title="Max Step", minval=0.1)
psar = talib.psar(start, stepInc, max_step)
plot(psar, color=color.blue, title="PSAR", linewidth=2,style=plotStyle.scatter)
```

### id

function:talib.psar

## talib.pvi (function)

Positive volume index for the chart's bars, the counterpart of `talib.nvi`.

No arguments.

### syntax

```
talib.pvi() → series float
```

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("talib.pvi Example", overlay=false)
pvi = talib.pvi()
plot(pvi, title="PVI", color=color.blue)
plot(talib.ema(pvi, 255), title="PVI Signal", color=color.orange)
```

### id

function:talib.pvi

## talib.pvt (function)

Price-volume trend for the chart's bars.

It is called with no arguments, and reads a series float back.

### syntax

```
talib.pvt() → series float
```

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("talib.pvt Example", overlay=false)
pvt = talib.pvt()
plot(pvt, title="Price-Volume Trend", color=color.blue)
```

### id

function:talib.pvt

## talib.range (function)

How much ground `source` covered over the last `length` bars, expressed as one figure.

Any series is accepted, so the window need not be a price window.

### syntax

```
talib.range(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Range Over Period", overlay=false)
length = input(20, "Lookback Period")
rangeOverPeriod = talib.range(close, length)
plot(rangeOverPeriod, style=plotStyle.bar, color=color.blue, title="Range Over Period")
```

### id

function:talib.range

## talib.rising (function)

Tests whether `source` has been rising across `length` bars.

It returns a bool, so it drops straight into a condition.

### syntax

```
talib.rising(series float source, series int length) → series bool
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("Rising Trend", overlay=true)
length = input(3, "Bars to Check")
isRising = talib.rising(close, length)
bgcolor(isRising ? color.green : na)
```

### id

function:talib.rising

## talib.rma (function)

Rolling moving average of `source` over `length` bars.

It is a function of its own, alongside `talib.sma` and `talib.ema`, and is not a synonym for either.

### syntax

```
talib.rma(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Running Moving Average (RMA)", overlay=true)
length = input(14, "RMA Length")
rmaValue = talib.rma(close, length)
plot(rmaValue, color=color.blue, title="RMA")
```

### id

function:talib.rma

## talib.roc (function)

Rate of change of `source` measured across `length` bars.

Where `talib.change` gives the difference, this gives the rate.

### syntax

```
talib.roc(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Rate of Change (ROC)", overlay=false)
length = input(10, "ROC Length")
rocValue = talib.roc(close, length)
plot(rocValue, color=color.blue, title="ROC")
hline(0, "Zero Line", color=color.gray)
```

### id

function:talib.roc

## talib.rsi (function)

Relative Strength Index for `source` over `length` bars.

Two arguments and one series float back — the same shape as `talib.cmo` and `talib.cci`.

### syntax

```
talib.rsi(series float source, series int length) → series float
```

### args

- `source`: series float
   Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Relative Strength Index (RSI)", overlay=false)
length = input(14, "RSI Length")
rsiValue = talib.rsi(close, length)
plot(rsiValue, color=color.blue, title="RSI")
hline(70, "Overbought", color=color.red)
hline(30, "Oversold", color=color.green)
```

### id

function:talib.rsi

## talib.sma (function)

Simple moving average of `source` over `length` bars: every bar in the window counts for the same.

Reach for this one unless you want a particular weighting, in which case see `talib.ema`, `talib.wma` or `talib.vwma`.

### syntax

```
talib.sma(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Simple Moving Average (SMA)", overlay=true)
length = input(20, "SMA Length")
smaValue = talib.sma(close, length)
plot(smaValue, color=color.blue, title="SMA")
```

### id

function:talib.sma

## talib.stdev (function)

Standard deviation of `source` over `length` bars. It is the population standard deviation: the squared differences from the mean are divided by `length`, not by `length - 1`.

Unlike `talib.variance`, this signature carries no `biased` flag: there is one form of the calculation and no switch.

### syntax

```
talib.stdev(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Standard Deviation (StDev)", overlay=false)
length = input(20, "StDev Length")
stdevValue = talib.stdev(close, length)
plot(stdevValue, color=color.blue, title="Standard Deviation")
```

### id

function:talib.stdev

## talib.stoch (function)

Stochastic reading that places `source` inside the span set by `high` and `low` over `length` bars.

The high and low series are arguments rather than assumptions, so you can drive the calculation from series of your own.

### syntax

```
talib.stoch(series float source, series float high, series float low, series int length) → series float
```

### args

- `source`: series float
  Source series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `high`: series float
  Series of high.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `low`: series float
  Series of low.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Length (number of bars back).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Stochastic Oscillator", overlay=false)
length = input(14, "Stochastic Length")
stochValue = talib.stoch(close, high, low, length)
plot(stochValue, color=color.blue, title="%K Line")
hline(80, "Overbought", color=color.red)
hline(20, "Oversold", color=color.green)
```

### id

function:talib.stoch

## talib.sum (function)

Adds up the last `length` values of `source`.

It is a moving window, which is what separates it from `talib.cum`. `math.sum` is equivalent.

### syntax

```
talib.sum(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Sum of Close Prices", overlay=false)
length = input(10, "Sum Length")
sumClose = talib.sum(close, length)
plot(sumClose, color=color.blue, title="Sum of Close Prices")
```

### id

function:talib.sum

## talib.supertrend (function)

Supertrend from a `multiplier` and an `atrLength`, calculated on the chart's own bars.

`multiplier` is a float series, as is `mult` on `talib.bb`, `talib.bbw`, `talib.kc`, and `talib.kcw`.

### syntax

```
talib.supertrend(series float multiplier, series int atrLength) → [series float, series float]
```

### args

- `multiplier`: series float
  The multiplier by which the ATR will get multiplied.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `atrLength`: series int
  Length of ATR.
  types: series int, simple int, input int, const int, literal int

### returnedType

[series float, series float]

### returns

- `supertrend`: series float
  The supertrend line.
- `direction`: series float
  A direction value; the entry example compares it with 1.

### example

```lipi
//@lipi=2
indicator("Supertrend", overlay=true)
atrLength = input(10, "ATR Length")
factor = input(3.0, "Multiplier")
[supertrend, direction] = talib.supertrend(factor, atrLength)
plot(supertrend, color=color.green, title="Supertrend")
bgcolor(direction == 1 ? color.green : color.red)
```

### id

function:talib.supertrend

## talib.swma (function)

Symmetrically weighted moving average of `source` over the last four bars, with the weights 1/6, 2/6, 2/6 and 1/6. It is `na` until four values exist.

There is no `length` argument: the window is fixed by the function, and you choose only what to feed it.

### syntax

```
talib.swma(series float source) → series float
```

### args

- `source`: series float
  Source series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Symmetric Weighted Moving Average (SWMA)", overlay=true)
length = input(10, "SWMA Length")
swmaValue = talib.swma(close)
plot(swmaValue, color=color.blue, title="SWMA")
```

### id

function:talib.swma

## talib.tr (function)

True range for the bar the script is on, taken from the chart's own bars.

The one argument, `handle_na`, is optional and selects how a missing value is treated.

### syntax

```
talib.tr(series bool handle_na) → series float
```

### args

- `handle_na?`: series bool
   How NaN values are handled. if true, and previous day's close is NaN then tr would be calculated as current day high-low. Otherwise (if false) tr would return NaN in such cases. Also note that `talib.atr` uses `talib.tr(true)`.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: false

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("True Range (TR)", overlay=false)
trValue = talib.tr()
plot(trValue, color=color.blue, title="True Range")
```

### id

function:talib.tr

## talib.tsi (function)

True Strength Index for `source`, smoothed by two lengths, `r` and `s`.

Both are ints, and both are required.

### syntax

```
talib.tsi(series float source, series int r, series int s) → series float
```

### args

- `source`: series float
   Source series.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `r`: series int
  Long length.
  types: series int, simple int, input int, const int, literal int
- `s`: series int
  Short length.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("True Strength Index (TSI)", overlay=false)
shortLength = input(13, "Short EMA Length")
longLength = input(25, "Long EMA Length")
tsiValue = talib.tsi(close, shortLength, longLength)
plot(tsiValue, color=color.blue, title="TSI")
hline(0, "Zero Line", color=color.gray)
```

### id

function:talib.tsi

## talib.valuewhen (function)

Reads `source` from the bar on which `condition` was true, going back as far as `occurrence` says.

`occurrence` is a simple int, not a series, so it is fixed for the run of the script and cannot be varied bar by bar.

### syntax

```
talib.valuewhen(series bool condition, series float source, simple int occurrence) → series float
```

### args

- `condition`: series bool
  The condition to search for.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
- `source`: series float
  The value to be returned from the bar where the condition is met.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `occurrence`: simple int
  The occurrence of the condition. The numbering starts from 0 and goes back in time, so '0' is the most recent occurrence of condition, '1' is the second most recent and so forth. Must be an integer >= 0.
  types: simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("talib.valuewhen Example", overlay=true)
cond = talib.crossover(close, talib.sma(close, 20))
v = talib.valuewhen(cond, close, 0)
plot(v, title="valuewhen", color=color.orange)
```

### id

function:talib.valuewhen

## talib.variance (function)

Variance of `source` over `length` bars.

An optional `biased` flag chooses between the biased and unbiased forms of the calculation. `talib.stdev` has no such flag.

### syntax

```
talib.variance(series float source, series int length, series bool biased) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int
- `biased?`: series bool
  Determines which estimate should be used. Optional. The default is true.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: true

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Variance Indicator", overlay=false)
length = input(20, "Variance Length")
varianceValue = talib.variance(close, length)
plot(varianceValue, color=color.blue, title="Variance")
```

### id

function:talib.variance

## talib.vwap (function)

Volume-weighted average price built on `source`.

The signature has one argument. There is no volume argument and no length or anchor argument.

### syntax

```
talib.vwap(series float source) → series float
```

### args

- `source`: series float
  Source used for the VWAP calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("VWAP Indicator", overlay=true)
vwapValue = talib.vwap(hlc3)
plot(vwapValue, color=color.blue, title="VWAP")
```

### id

function:talib.vwap

## talib.vwma (function)

Volume-weighted moving average of `source` over `length` bars: bars that traded more count for more.

Volume is not an argument, so you pass only the series and the window.

### syntax

```
talib.vwma(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("VWMA Indicator", overlay=true)
length = input(20, "VWMA Length")
vwmaValue = talib.vwma(close, length)
plot(vwmaValue, color=color.blue, title="VWMA")
```

### id

function:talib.vwma

## talib.wma (function)

Weighted moving average of `source` over `length` bars.

For an average weighted by volume, use `talib.vwma` instead.

### syntax

```
talib.wma(series float source, series int length) → series float
```

### args

- `source`: series float
  Series of values to process.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  Number of bars (length).
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Weighted Moving Average (WMA)", overlay=true)
length = input(20, "WMA Length")
wmaValue = talib.wma(close, length)
plot(wmaValue, color=color.blue, title="WMA")
```

### id

function:talib.wma

## talib.wpr (function)

Williams %R over `length` bars. In this build it is read from the previous bar's high, low and close: the value on a bar is the %R as of the bar before it, so it lags the chart by one bar.

`length` is the only argument; the reading comes from the chart's own bars.

### syntax

```
talib.wpr(series int length) → series float
```

### args

- `length`: series int
  Number of bars.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Williams %R (WPR)", overlay=false)
length = input(14, "WPR Length")
wprValue = talib.wpr(length)
plot(wprValue, color=color.blue, title="Williams %R")
hline(-20, "Overbought", color=color.red)
hline(-80, "Oversold", color=color.green)
hline(-50, "Mid-Level", color=color.gray)
```

### id

function:talib.wpr

## talib.wvad (function)

Williams variable accumulation/distribution, calculated on the chart's own bars. In this build `length` does not set a window and nothing is accumulated: the value on each bar is `(close - open) / (high - low) * volume` for that bar alone.

One argument, and a single series float back.

### syntax

```
talib.wvad(series int length) → series float
```

### args

- `length`: series int
  Accepted, but in this build it does not build a window: see the description.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("talib.wvad Example", overlay=false)
wvad = talib.wvad(14)
plot(wvad, title="WVAD", color=color.blue, style=plotStyle.histogram)
```

### id

function:talib.wvad
