Contents: orderflow (library) · orderflow.buy (variable) · orderflow.buyvolume (variable) · orderflow.cothigh (variable) · orderflow.cotlow (variable) · orderflow.cvd (function) · orderflow.delta (variable) · orderflow.maxdelta (variable) · orderflow.mindelta (variable) · orderflow.sell (variable) · orderflow.sellvolume (variable) · orderflow.trades (variable)

# orderflow

## orderflow (library)

Ten integer series read from a bar's footprint data — buy and sell trade counts, buy and sell volumes, delta with its intra-bar extremes, and the commitment-of-traders high and low — plus one function, `orderflow.cvd()`.

That is the whole of the orderflow surface a script can reach. Every variable in it reads `na` on a bar with no footprint data, which is also how a script tests whether the data is there at all.

### example

```lipi
//@lipi=2
indicator("orderflow Library Example", overlay=false)
plot(orderflow.delta, title="Delta", color=color.blue, style=plotStyle.histogram)
plot(orderflow.cvd(), title="Cumulative Delta", color=color.orange)
```

### id

library:orderflow

## orderflow.buy (variable)

How many buy trades the bar carried.

This counts trades, not volume. `orderflow.buyvolume` measures the volume those trades moved, and the two are separate figures rather than two views of one.

### type

series int

### example

```lipi
//@lipi=2
indicator("Buy Trades per Bar", overlay=false)
buyTrades = orderflow.buy
plot(buyTrades, title="Buy Trades", style=plotStyle.histogram, color=color.green)
```

### id

variable:orderflow.buy

## orderflow.buyvolume (variable)

The volume bought in the bar.

A bar can carry more buy trades than sell trades while more volume goes the other way, so pick the count or the volume according to the question.

### type

series int

### example

```lipi
//@lipi=2
indicator("Buy Volume per Bar", overlay=false)
buyVol = orderflow.buyvolume
plot(buyVol, title="Buy Volume", style=plotStyle.histogram, color=color.green)
```

### id

variable:orderflow.buyvolume

## orderflow.cothigh (variable)

The commitment-of-traders high for the bar, taken from the same per-bar footprint summary as the delta figures.

### type

series int

### example

```lipi
//@lipi=2
indicator("orderflow.cothigh Example", overlay=true)
coth = orderflow.cothigh
plot(coth, title="COTH", color=color.red, style=plotStyle.line)
```

### id

variable:orderflow.cothigh

## orderflow.cotlow (variable)

The commitment-of-traders low for the bar.

The summary these two come from also holds a buy and a sell breakdown of each. Lipi does not expose those, so the high and the low are all a script can read.

### type

series int

### example

```lipi
//@lipi=2
indicator("orderflow.cotlow Example", overlay=true)
cotl = orderflow.cotlow
plot(cotl, title="COTL", color=color.blue, style=plotStyle.line)
```

### id

variable:orderflow.cotlow

## orderflow.cvd (function)

Cumulative volume delta. On each bar it adds that bar's delta - the balance of buying against selling, taken as at the bar's close - to a running total, and hands you that total as one whole number per bar.

The total restarts from zero on the first bar of every session. What you read is therefore the delta accumulated within the current session, not a figure running from the start of the chart, and a fall to zero at a session boundary is the restart rather than a move in the market.

There are no arguments, so the session restart cannot be moved or switched off. Where a bar's delta is `na`, the running total carries forward unchanged instead of becoming `na`.

### syntax

```
orderflow.cvd() → series int
```

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("Cumulative Volume Delta (CVD)", overlay=false)
cvd = orderflow.cvd()
plot(cvd, title="CVD", style=plotStyle.line, color=color.orange)
```

### id

function:orderflow.cvd

## orderflow.delta (variable)

The bar's delta as at its close.

For the delta accumulated across a session rather than one bar's figure, call `orderflow.cvd()`.

### type

series int

### example

```lipi
//@lipi=2
indicator("Orderflow Delta", overlay=false)
delta = orderflow.delta
plot(delta, title="Delta", style=plotStyle.histogram, color=delta >= 0 ? color.green : color.red)
```

### id

variable:orderflow.delta

## orderflow.maxdelta (variable)

The highest delta the bar reached while it was forming.

It belongs to that bar alone and starts afresh on the next one, so it is not a running high across the chart.

### type

series int

### example

```lipi
//@lipi=2
indicator("Max Delta per Bar", overlay=false)
maxDelta = orderflow.maxdelta
plot(maxDelta, title="Max Delta", style=plotStyle.histogram, color=color.green)
```

### id

variable:orderflow.maxdelta

## orderflow.mindelta (variable)

The lowest delta the bar reached while it was forming.

Read it with `orderflow.maxdelta` when you want the swing inside a bar: a bar can close near zero having travelled a long way in both directions, and the closing figure will not show that.

### type

series int

### example

```lipi
//@lipi=2
indicator("Min Delta per Bar", overlay=false)
minDelta = orderflow.mindelta
plot(minDelta, title="Min Delta", style=plotStyle.histogram, color=color.red)
```

### id

variable:orderflow.mindelta

## orderflow.sell (variable)

How many sell trades the bar carried.

The mirror of `orderflow.buy`, and a count in the same way.

### type

series int

### example

```lipi
//@lipi=2
indicator("Sell Trades per Bar", overlay=false)
sellTrades = orderflow.sell
plot(sellTrades, title="Sell Trades", style=plotStyle.histogram, color=color.red)
```

### id

variable:orderflow.sell

## orderflow.sellvolume (variable)

The volume sold in the bar.

### type

series int

### example

```lipi
//@lipi=2
indicator("Sell Volume per Bar", overlay=false)
sellVol = orderflow.sellvolume
plot(sellVol, title="Sell Volume", style=plotStyle.histogram, color=color.red)
```

### id

variable:orderflow.sellvolume

## orderflow.trades (variable)

The bar's overall trade count.

It is read from the bar's own footprint totals, not worked out by adding the buy and sell counts together.

### type

series int

### example

```lipi
//@lipi=2
indicator("Total Trades per Bar", overlay=false)
totalTrades = orderflow.trades
plot(totalTrades, title="Total Trades", style=plotStyle.histogram, color=color.gray)
```

### id

variable:orderflow.trades
