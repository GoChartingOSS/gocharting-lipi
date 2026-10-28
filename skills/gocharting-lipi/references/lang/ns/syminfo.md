Contents: syminfo (library) · syminfo.asset_type (variable) · syminfo.currency (variable) · syminfo.exchange (variable) · syminfo.isindex (variable) · syminfo.mincontract (variable) · syminfo.minmove (variable) · syminfo.mintick (variable) · syminfo.pricescale (variable) · syminfo.root (variable) · syminfo.segment (variable) · syminfo.sizescale (variable) · syminfo.symbol (variable) · syminfo.ticker (variable) · syminfo.timezone (variable)

# syminfo

## syminfo (library)

Fourteen properties of the chart's instrument — eight strings, one boolean, two floats and three ints.

All fourteen are simple, so an instrument property is settled for the whole run of a script; they are set from the instrument's record before the script runs. `syminfo.minmove` is the tick size and `syminfo.mintick` is the tick size divided by the price precision.

### example

```lipi
//@lipi=2
indicator("syminfo Library Example", overlay=true)
if barstate.islast {
    info = syminfo.ticker + " on " + syminfo.exchange + ", tick " + str.tostring(syminfo.mintick) + " " + syminfo.currency
    label.new(bar_index, high, text=info)
}
```

### id

library:syminfo

## syminfo.asset_type (variable)

The instrument's asset type.

### type

simple string

### example

```lipi
//@lipi=2
indicator(title="Asset Type", overlay=true)
assetType = syminfo.asset_type
colorType = assetType == "EQUITY" ? color.blue : assetType == "CRYPTO" ? color.red : color.gray
plot(close, color=colorType)
```

### id

variable:syminfo.asset_type

## syminfo.currency (variable)

The currency the instrument is quoted in.

### type

simple string

### example

```lipi
//@lipi=2
indicator(title="Currency Background Example", overlay=true)
currency = syminfo.currency
bgColor = currency == "USD" ? color.new(color.blue, 0.2) : currency == "JPY" ? color.new(color.red, 0.2) : color.new(color.gray, 0.2)
bgcolor(bgColor)
plot(close)
```

### id

variable:syminfo.currency

## syminfo.exchange (variable)

The exchange the instrument trades on.

### type

simple string

### example

```lipi
//@lipi=2
indicator(title="Exchange", overlay=true)
exchange = syminfo.exchange
bgcolor(exchange == "NSE" ? color.blue : exchange == "CME" ? color.red : exchange == "US" ? color.green : color.gray)
```

### id

variable:syminfo.exchange

## syminfo.isindex (variable)

True when the chart instrument is an index.

It is the only boolean in the namespace. Like the other `syminfo` properties it is set from the instrument's record when the script runs, so it is known on every bar.

### type

simple bool

### example

```lipi
//@lipi=2
indicator(title="Is Index Plotting", overlay=true)
is_index = syminfo.isindex
plot(close, color=is_index ? color.blue : color.red)
```

### id

variable:syminfo.isindex

## syminfo.mincontract (variable)

The instrument's minimum contract, as a whole number.

### type

simple int

### example

```lipi
//@lipi=2
indicator(title="Min Contract", overlay=true)
min_contract = syminfo.mincontract
plot(min_contract)
```

### id

variable:syminfo.mincontract

## syminfo.minmove (variable)

The instrument's tick size, as a float. `strategy.exit` counts its `profit` and `loss` arguments in this unit.

### type

simple float

### example

```lipi
//@lipi=2
indicator(title="Min Move Example", overlay=true)
min_move = syminfo.minmove
plot(close, color=min_move < 0.01 ? color.blue : color.red)
```

### id

variable:syminfo.minmove

## syminfo.mintick (variable)

The instrument's tick size divided by its price scale: `syminfo.minmove / syminfo.pricescale`.

It is not the tick size itself. `syminfo.minmove` is the tick size, and the `profit` and `loss` arguments of `strategy.exit` count ticks of `syminfo.minmove`.

### type

simple float

### example

```lipi
//@lipi=2
indicator(title="Min Tick Example", overlay=true)
minTickValue = syminfo.mintick
plot(minTickValue, title="Min Tick", color=color.red)
```

### id

variable:syminfo.mintick

## syminfo.pricescale (variable)

The instrument's maximum tick precision, as an int. `syminfo.mintick` is `syminfo.minmove` divided by this value.

### type

simple int

### example

```lipi
//@lipi=2
indicator(title="Price Scale Example", overlay=true)
priceScaleValue = syminfo.pricescale
plot(priceScaleValue, title="Price Scale", color=color.green)
```

### id

variable:syminfo.pricescale

## syminfo.root (variable)

The instrument's root.

### type

simple string

### example

```lipi
//@lipi=2
indicator(title="Root Symbol", overlay=true)
root = syminfo.root
plot(talib.sma(close, 14), color=root == "ES" ? color.green : color.orange)
```

### id

variable:syminfo.root

## syminfo.segment (variable)

The segment the instrument belongs to.

### type

simple string

### example

```lipi
//@lipi=2
indicator(title="Segment Example", overlay=true)
assetSegment = syminfo.segment
isMainSegment = assetSegment == "FUTURE" ? 1 : 0
plot(isMainSegment, title="Is Main Segment", color=color.green)
```

### id

variable:syminfo.segment

## syminfo.sizescale (variable)

The instrument's size scale, the counterpart of its price scale.

### type

simple int

### example

```lipi
//@lipi=2
indicator("syminfo.sizescale Example", overlay=true)
if barstate.islast {
    label.new(bar_index, high, text="Size scale: " + str.tostring(syminfo.sizescale))
}
```

### id

variable:syminfo.sizescale

## syminfo.symbol (variable)

The instrument's symbol, distinct from its ticker.

### type

simple string

### example

```lipi
//@lipi=2
indicator(title="Symbol Display", overlay=true)
assetSymbol = syminfo.symbol
plotColor = assetSymbol == "AAPL" ? color.green : assetSymbol == "TSLA" ? color.red : color.blue
plot(close, title="Price", color=plotColor)
```

### id

variable:syminfo.symbol

## syminfo.ticker (variable)

The chart instrument's ticker.

Every `syminfo` value is simple — fixed for the whole run of the script — and set from the instrument's record before the script runs.

### type

simple string

### example

```lipi
//@lipi=2
indicator(title="Ticker Example", overlay=true)
assetTicker = syminfo.ticker
plotColor = assetTicker == "US:SPOT:AAPL" ? color.green : assetTicker == "US:SPOT:TSLA" ? color.red : color.blue
plot(close, title="Price", color=plotColor)
```

### id

variable:syminfo.ticker

## syminfo.timezone (variable)

The instrument's timezone.

It is the value to pass as the timezone argument of the date functions, which each take it as an optional argument.

### type

simple string

### example

```lipi
//@lipi=2
indicator(title="Timezone Example", overlay=true)
bgColor = syminfo.timezone == "America/New_York" ? color.new(color.blue, 0.2) : syminfo.timezone == "Asia/Kolkata" ? color.new(color.red, 0.2) : syminfo.timezone == "UTC" ? color.new(color.orange, 0.2) : color.new(color.gray, 0.2)
bgcolor(bgColor)
```

### id

variable:syminfo.timezone
