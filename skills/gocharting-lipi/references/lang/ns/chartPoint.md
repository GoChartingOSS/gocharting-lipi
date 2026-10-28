Contents: chartPoint (library) · chartPoint (type) · chartPoint.copy (function) · chartPoint.from_index (function) · chartPoint.from_time (function) · chartPoint.new (function) · chartPoint.now (function)

# chartPoint

## chartPoint (library)

Five functions that build a chart point — `new`, `from_time`, `from_index`, `now` and `copy` — for the type of the same name, whose three fields are a time, an index and a price.

Drawing functions take chart points: `line.new`, `box.new` and `polyline.new` accept them, and `label.set_point`, `line.set_point1`, `line.set_point2`, `box.set_top_left_point` and `box.set_bottom_right_point` set a drawing's position from one.

### example

```lipi
//@lipi=2
indicator("chartPoint Library Example", overlay=true)
if barstate.islast {
    start = chartPoint.from_index(bar_index[30], low[30])
    finish = chartPoint.now(high)
    line.new(start, finish, color=color.blue, width=2)
}
```

### id

library:chartPoint

## chartPoint (type)

A single position on the chart, described by three fields: time carries when, index carries which bar, and price carries where on the price scale.

All three fields are series, so a point built on one bar need not hold the same coordinates as one built on the next.

### fields

- `time`: series int
  The x-coordinate of the point, expressed as a UNIX time value, in milliseconds.
- `index`: series int
  The x-coordinate of the point, expressed as a bar index value.
- `price`: series float
  The y-coordinate of the point.

### example

```lipi
//@lipi=2
indicator("chartPoint Example", overlay=true)
if barstate.islast {
    chartPoint p1 = chartPoint.from_index(bar_index[20], low[20])
    chartPoint p2 = chartPoint.from_index(bar_index, high)
    line.new(p1, p2, color=color.blue, width=2)
}
```

### id

type:chartPoint

## chartPoint.copy (function)

Hands back a copy of a chart point.

One argument, required: the point to copy.

### syntax

```
chartPoint.copy(series chartPoint id) → series chartPoint
```

### args

- `id`: series chartPoint
  A chartPoint object.
  types: series chartPoint, simple chartPoint, input chartPoint, const chartPoint, literal chartPoint

### returnedType

series chartPoint

### returnDesc

A new chartPoint with the same coordinates as id.

### example

```lipi
//@lipi=2
indicator("chartPoint.copy Example", overlay=true)
if barstate.islast {
    p = chartPoint.from_index(bar_index, close)
    c = chartPoint.copy(p)
}
```

### id

function:chartPoint.copy

## chartPoint.from_index (function)

Builds a chart point from a bar index and a price.

Both arguments are required. Where you would rather locate the point by time, use chartPoint.from_time.

### syntax

```
chartPoint.from_index(series int index, series float price) → series chartPoint
```

### args

- `index`: series int
  The x-coordinate of the point, expressed as a bar index value.
  types: series int, simple int, input int, const int, literal int
- `price`: series float
  The y-coordinate of the point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series chartPoint

### returnDesc

A chartPoint with the given bar index and price.

### example

```lipi
//@lipi=2
indicator("chartPoint.from_index Example", overlay=true)
if barstate.islast {
    p1 = chartPoint.from_index(bar_index[10], high[10])
    p2 = chartPoint.from_index(bar_index, close)
    pts = array.new<chartPoint>(0)
    array.push(pts, p1)
    array.push(pts, p2)
    polyline.new(pts, line_color=color.orange)
}
```

### id

function:chartPoint.from_index

## chartPoint.from_time (function)

Builds a chart point from a time and a price.

Both arguments are required. It is the time-based counterpart of chartPoint.from_index.

### syntax

```
chartPoint.from_time(series int time, series float price) → series chartPoint
```

### args

- `time`: series int
  The x-coordinate of the point, expressed as a UNIX time value, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `price`: series float
  The y-coordinate of the point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series chartPoint

### returnDesc

A chartPoint with the given UNIX time and price.

### example

```lipi
//@lipi=2
indicator("chartPoint.from_time Example", overlay=true)
if barstate.islast {
    p = chartPoint.from_time(time, close)
    pts = array.new<chartPoint>(0)
    array.push(pts, p)
    array.push(pts, chartPoint.from_time(time[5], high[5]))
    polyline.new(pts, xloc=xloc.bar_time, line_color=color.teal)
}
```

### id

function:chartPoint.from_time

## chartPoint.new (function)

Builds a chart point with all three of its fields given: a time, a bar index and a price.

All three arguments are required. Use one of the narrower constructors where you have only two of the three.

### syntax

```
chartPoint.new(series int time, series int index, series float price) → series chartPoint
```

### args

- `time`: series int
  The x-coordinate of the point, expressed as a UNIX time value, in milliseconds.
  types: series int, simple int, input int, const int, literal int
- `index`: series int
  The x-coordinate of the point, expressed as a bar index value.
  types: series int, simple int, input int, const int, literal int
- `price`: series float
  The y-coordinate of the point.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series chartPoint

### returnDesc

A chartPoint with the given time, index, and price.

### example

```lipi
//@lipi=2
indicator("chartPoint.new Example", overlay=true)
if barstate.islast {
    p = chartPoint.new(time, bar_index, close)
}
```

### id

function:chartPoint.new

## chartPoint.now (function)

Builds a chart point from a price alone: you give no time and no bar index, and even the price is optional.

The point is placed at the current bar: its index is `bar_index`, its time is the open time of the bar (the same value as `time`), and its price is `price`.

### syntax

```
chartPoint.now(series float price) → series chartPoint
```

### args

- `price?`: series float
  The y-coordinate of the point. Optional. The default is close.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: close

### returnedType

series chartPoint

### returnDesc

A chartPoint at the current bar, with the given price (default close).

### example

```lipi
//@lipi=2
indicator("chartPoint.now Example", overlay=true)
if barstate.islast {
    p = chartPoint.now(high)
}
```

### id

function:chartPoint.now
