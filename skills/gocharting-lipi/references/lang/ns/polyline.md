Contents: polyline (library) · polyline (type) · polyline.all (variable) · polyline.all (function) · polyline.delete (function) · polyline.new (function)

# polyline

## polyline (library)

Functions for creating and deleting multi-point polyline drawings from an array of chartPoint vertices.

### example

```lipi
//@lipi=2
indicator("polyline Library Example", overlay=true)
if barstate.islast {
    pts = array.new<chartPoint>(0)
    int i = 0
    while i <= 4 {
        array.push(pts, chartPoint.from_index(bar_index - i * 5, close[i * 5]))
        i := i + 1
    }
    polyline.new(pts, curved=true, line_color=color.purple, line_width=2)
}
```

### id

library:polyline

## polyline (type)

A multi-point drawing built from an array of chartPoint values. Unlike line, a polyline takes many vertices (at most 1000) and has an optional curve and fill.

### example

```lipi
//@lipi=2
indicator("Polyline Type Example", overlay=true)
if barstate.islast {
    pts = array.new<chartPoint>(0)
    array.push(pts, chartPoint.from_index(bar_index[20], low[20]))
    array.push(pts, chartPoint.from_index(bar_index[10], high[10]))
    array.push(pts, chartPoint.from_index(bar_index, close))
    polyline.new(pts, line_color=color.orange, line_width=2)
}
```

### id

type:polyline

## polyline.all (variable)

Array of all currently existing polyline drawings, from oldest to newest.

### type

series array<polyline>

### example

```lipi
//@lipi=2
indicator("polyline.all Example", overlay=true)
if barstate.islast {
    pts = array.new<chartPoint>(0)
    array.push(pts, chartPoint.from_index(bar_index[5], high[5]))
    array.push(pts, chartPoint.from_index(bar_index, close))
    polyline.new(pts)
}
plot(array.length(polyline.all), title="Polyline Count")
```

### id

variable:polyline.all

## polyline.all (function)

Returns the array of all existing polyline objects (same as the polyline.all variable).

### syntax

```
polyline.all() → series array<polyline>
```

### returnedType

series array<polyline>

### returnDesc

An array of polyline IDs, oldest to newest.

### example

```lipi
//@lipi=2
indicator("polyline.all Function Example", overlay=true)
plot(array.length(polyline.all), title="Polylines")
```

### id

function:polyline.all

## polyline.delete (function)

Deletes a polyline object.

### syntax

```
polyline.delete(series polyline id) → void
```

### args

- `id`: series polyline
  Polyline object to delete.
  types: series polyline, simple polyline, input polyline, const polyline, literal polyline

### returnedType

void

### returnDesc

void

### example

```lipi
//@lipi=2
indicator("polyline.delete Example", overlay=true)
if barstate.islast {
    pts = array.new<chartPoint>(0)
    array.push(pts, chartPoint.from_index(bar_index[5], high[5]))
    array.push(pts, chartPoint.from_index(bar_index, close))
    p = polyline.new(pts)
    polyline.delete(p)
}
```

### id

function:polyline.delete

## polyline.new (function)

Creates a polyline from an array of chartPoint objects. The drawing is bar/price anchored via those points. A polyline holds at most 1000 vertices: with an empty array, or with more than 1000 points, the call draws nothing and returns `na`.

### syntax

```
polyline.new(series array<chartPoint> points, series bool curved, series bool closed, series string xloc, series color line_color, series color fill_color, series string line_style, series int line_width, const bool force_overlay) → series polyline
```

### args

- `points`: series array<chartPoint>
  Array of chartPoint vertices, in drawing order: at most 1000. An empty array, or one with more than 1000 points, makes the call return `na`.
  types: series array<chartPoint>, simple array<chartPoint>, input array<chartPoint>, const array<chartPoint>, literal array<chartPoint>
- `curved?`: series bool
  If true, connect points with a curve. Default is false.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: false
- `closed?`: series bool
  If true, connect the last point back to the first. Default is false.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: false
- `xloc?`: series string
  How x-coordinates are interpreted: xloc.bar_index or xloc.bar_time. Default is xloc.bar_index.
  types: series string, simple string, input string, const string, literal string
  values: xloc.bar_index, xloc.bar_time
  default: xloc.bar_index
- `line_color?`: series color
  Stroke color. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `fill_color?`: series color
  Interior fill color when the polyline is closed. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na
- `line_style?`: series string
  Stroke style (line.style_*). Optional.
  types: series string, simple string, input string, const string, literal string
  values: line.style_arrow_both, line.style_arrow_left, line.style_arrow_right, line.style_dashed, line.style_dotted, line.style_solid
  default: line.style_solid
- `line_width?`: series int
  Stroke width in pixels. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 1
- `force_overlay?`: const bool
  If true, draw on the main pane even when the script is not overlay. Default is false.
  types: const bool, const int, literal int, const float, literal float, literal bool
  default: false

### returnedType

series polyline

### returnDesc

The ID of the created polyline, or na if points are invalid.

### example

```lipi
//@lipi=2
indicator("polyline.new Example", overlay=true)
if barstate.islast {
    pts = array.new<chartPoint>(0)
    array.push(pts, chartPoint.from_index(bar_index[20], low[20]))
    array.push(pts, chartPoint.from_index(bar_index[10], high[10]))
    array.push(pts, chartPoint.from_index(bar_index, close))
    polyline.new(pts, curved=false, closed=false, line_color=color.orange, line_width=2)
}
```

### id

function:polyline.new
