Contents: barstate (library) · barstate.isconfirmed (variable) · barstate.isfirst (variable) · barstate.ishistory (variable) · barstate.islast (variable) · barstate.islastconfirmedhistory (variable) · barstate.isnew (variable) · barstate.isrealtime (variable)

# barstate

## barstate (library)

Seven boolean series that tell your script which kind of bar it is being evaluated on: the first, a new one, a historical one, the last, the last confirmed historical one, one that is still updating, and one that is confirmed.

No functions live here — the namespace is variables only.

### example

```lipi
//@lipi=2
indicator("barstate Library Example", overlay=true)
// Colour the first bar, realtime bars and the last bar differently
c = barstate.isfirst ? color.blue : barstate.isrealtime ? color.orange : barstate.islast ? color.green : na
bgcolor(color.new(c, 0.2))
```

### id

library:barstate

## barstate.isconfirmed (variable)

Returns true if the current bar is confirmed (closed). On historical bars this is true, except on the last historical bar while the market is open, where it is false because that bar is still forming. On the real-time bar this is false until the bar closes.

### type

series bool

### example

```lipi
//@lipi=2
indicator("BarState.isconfirmed Example", overlay=true)
bgcolor(barstate.isconfirmed ? color.green : na)
```

### id

variable:barstate.isconfirmed

## barstate.isfirst (variable)

Your script is being evaluated on the first bar of the chart. On every bar after that one, this reads false.

A script is evaluated once per bar, in order, so this holds on the earliest run only.

### type

series bool

### example

```lipi
//@lipi=2
indicator("First Bar Check", overlay=true)
static float firstBarClose = barstate.isfirst ? close : na
plot(firstBarClose)
```

### id

variable:barstate.isfirst

## barstate.ishistory (variable)

Tells your script whether the bar it is being evaluated on is a historical bar. On a bar that is not historical it reads false.

The value is a series, so the answer it gives changes as the script moves from bar to bar.

### type

series bool

### example

```lipi
//@lipi=2
indicator(title="barstate.ishistory Example", overlay=true)
static float barHigh = na
barHigh := high 
histValue = barstate.ishistory ? barHigh : 0
realtimeValue = barstate.ishistory ? 0 : barHigh
plot(histValue, color=color.blue, title="Historical High")
plot(realtimeValue, color=color.red, title="Real-time High")
```

### id

variable:barstate.ishistory

## barstate.islast (variable)

The bar your script is on is the last bar of the chart. On every bar before it, this reads false.

It marks a single position in the series rather than a range of bars.

### type

series bool

### example

```lipi
//@lipi=2
indicator("BarState.islast Example", overlay=true)
plotshape(barstate.islast, location=location.abovebar, shape=shape.triangleup, color=color.red, size=size.small)
```

### id

variable:barstate.islast

## barstate.islastconfirmedhistory (variable)

This marks the last confirmed historical bar of the chart, when the market is closed. Every other bar reads false.

While the market is open the flag is false on every loaded bar, because the last loaded bar is still forming and is not confirmed. It is a separate flag from barstate.islast, which marks the last bar.

### type

series bool

### example

```lipi
//@lipi=2
indicator("BarState.islastconfirmedhistory Example", overlay=true)

// Check if the current bar is the last confirmed historical bar
is_last_confirmed = barstate.islastconfirmedhistory
// Highlight the last confirmed historical bar
plotshape(is_last_confirmed, location=location.abovebar, shape=shape.triangleup, color=color.blue, size=size.small)
```

### id

variable:barstate.islastconfirmedhistory

## barstate.isnew (variable)

The bar being evaluated is a new bar. Where it is not, your script reads false.

Read it in a condition, as you would any series value: the answer it gives changes from bar to bar.

### type

series bool

### example

```lipi
//@lipi=2
indicator("barstate.isnew Example", overlay=false)
// 1 on a new bar, otherwise 0
new_bar_signal = barstate.isnew ? 1 : 0
plot(new_bar_signal, color=color.green, style=plotStyle.histogram, title="New Bar Signal")
```

### id

variable:barstate.isnew

## barstate.isrealtime (variable)

The bar under evaluation is a live bar: this is true on every run of that bar, including the run when the bar closes, and false on historical bars.

It is not the opposite of `barstate.isconfirmed`: on the run when the bar closes both are true. To test that a bar has closed, use `barstate.isconfirmed`. If a result must not move once it is drawn, base it on a bar that has closed.

### type

series bool

### example

```lipi
//@lipi=2
indicator("BarState.isrealtime Background Example", overlay=true)
// Change background color if the bar is real-time
bgcolor(barstate.isrealtime ? color.red : na)
```

### id

variable:barstate.isrealtime
