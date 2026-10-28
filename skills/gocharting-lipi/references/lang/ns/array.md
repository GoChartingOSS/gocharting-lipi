Contents: array (library) · array (type) · array.abs (function) · array.avg (function) · array.binary_search (function) · array.binary_search_leftmost (function) · array.binary_search_rightmost (function) · array.clear (function) · array.concat (function) · array.copy (function) · array.covariance (function) · array.every (function) · array.fill (function) · array.first (function) · array.from (function) · array.from (function) · array.from (function) · array.from (function) · array.from (function) · array.from (function) · array.from (function) · array.from (function) · array.from (function) · array.from (function) · array.from (function) · array.get (function) · array.includes (function) · array.indexof (function) · array.insert (function) · array.join (function) · array.last (function) · array.lastindexof (function) · array.length (function) · array.max (function) · array.median (function) · array.min (function) · array.mode (function) · array.new (function) · array.new_bool (function) · array.new_box (function) · array.new_color (function) · array.new_float (function) · array.new_int (function) · array.new_label (function) · array.new_line (function) · array.new_linefill (function) · array.new_string (function) · array.new_table (function) · array.percentile_linear_interpolation (function) · array.percentile_nearest_rank (function) · array.percentrank (function) · array.pop (function) · array.push (function) · array.range (function) · array.remove (function) · array.removeAll (function) · array.reverse (function) · array.set (function) · array.shift (function) · array.slice (function) · array.some (function) · array.sort (function) · array.sort_indices (function) · array.standardize (function) · array.stdev (function) · array.sum (function) · array.unshift (function) · array.variance (function)

# array

## array (library)

Functions for creating and working with arrays: ordered, resizable lists of values of one type. They cover creation (`array.new` with optional `initial_value`, the typed `array.new_*` constructors and `array.from`), reading and editing elements, searching and sorting, and statistics over the elements such as `array.avg`, `array.stdev` and `array.percentile_nearest_rank`.

Arrays declared with `static` keep their elements from bar to bar, which makes them the usual tool for rolling windows and for keeping a limited history of drawings.

### notes

- An `array.<name>(a, ...)` function can also be called on the array as `a.<name>(...)`: `a.push(x)`, `a.get(i)`, `a.set(i, x)`, `a.length()`, `a.sum()`, `a.first()`, `a.last()`, `a.pop()` and `a.clear()` all compile. There is no `a.size()`: the name is `length`.
- The numeric functions (`abs`, `avg`, `covariance`, `max`, `median`, `min`, `mode`, `percentile_linear_interpolation`, `percentile_nearest_rank`, `percentrank`, `range`, `standardize`, `stdev`, `sum` and `variance`) take an array of int or float elements. Another element type fails the check, for example `array.sum` on a string array: "Error in `array.sum()`: array type must be int or float".
- `sort`, `sort_indices`, `join` and the three `binary_search` forms take an array of int, float or string elements; `every` and `some` take bool, int or float. Another element type fails the check, for example "Error in `array.sort()`: array type must be int, float or string".
- The numeric functions that return one value leave out `na` elements and return `na` when none is left (an empty array, or only `na` elements); `stdev`, `variance` and `covariance` also return `na` when `biased` is false and fewer than two values are left. `abs` and `standardize` return an array instead: each slot is kept, a `na` element stays `na`, and an empty array gives an empty array. `array.covariance` stops the script with a runtime error when its two arrays differ in size.

### example

```lipi
//@lipi=2
indicator("array Library Example", overlay=true)
static array<float> closes = array.new_float(0)
array.push(closes, close)
if array.length(closes) > 20 {
    array.shift(closes)
}
plot(array.max(closes), title="20-Bar Max", color=color.green)
plot(array.min(closes), title="20-Bar Min", color=color.red)
plot(array.avg(closes), title="20-Bar Average", color=color.gray)
```

### id

library:array

## array (type)

An ordered, resizable list of values of one type, written `array<type>`, as in `array<float>`. Create one with `array.new<type>(length)`, a typed constructor such as `array.new_float`, or `array.from`, and work with it through the `array` functions.

An array declared with `static` keeps its elements from one bar to the next; without `static` it is created again on every bar.

### example

```lipi
//@lipi=2
indicator("array Example", overlay=true)
// The last 10 closes, kept across bars
static array<float> closes = array.new_float(0)
array.push(closes, close)
if array.length(closes) > 10 {
    array.shift(closes)
}
plot(array.avg(closes), title="10-Bar Average", color=color.blue)
```

### id

type:array

## array.abs (function)

Returns a new array holding the absolute value of each element. The original array is not changed.

### syntax

```
array.abs(series array id) → series array
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series array

### example

```lipi
//@lipi=2
indicator("array.abs Example", overlay=false)
changes = array.from(close - close[1], close[1] - close[2], close[2] - close[3])
plot(array.sum(array.abs(changes)), title="Total Movement, 3 Bars", color=color.blue)
```

### id

function:array.abs

## array.avg (function)

Returns the mean of the array's elements.

### syntax

```
array.avg(series array id) → series float
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("array.avg Example", overlay=true)
prices = array.from(high, low, close)
plot(array.avg(prices), title="Typical Price", color=color.blue)
```

### id

function:array.avg

## array.binary_search (function)

Searches an array sorted in ascending order for `value` and returns its index, or -1 when it is not there. The array must already be sorted.

### syntax

```
array.binary_search(series array id, series <type of the array's elements> value) → series int
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to search for.

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("array.binary_search Example", overlay=false)
levels = array.from(10.0, 20.0, 30.0, 40.0)
plot(array.binary_search(levels, 30.0), title="Index of 30 (2)", color=color.blue)
```

### id

function:array.binary_search

## array.binary_search_leftmost (function)

Searches an array sorted in ascending order. When `value` is found, returns the index of its first occurrence; otherwise returns the index at which `value` would be inserted to keep the array sorted: the index of the first element larger than `value`, or the length of the array when every element is smaller. The array must already be sorted.

### syntax

```
array.binary_search_leftmost(series array id, series <type of the array's elements> value) → series int
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to search for.

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("array.binary_search_leftmost Example", overlay=false)
levels = array.from(10.0, 20.0, 30.0, 40.0)
// 25 is not in the array: the result is 2, the index of 30, the first element larger than 25
plot(array.binary_search_leftmost(levels, 25.0), title="Leftmost Index", color=color.blue)
```

### id

function:array.binary_search_leftmost

## array.binary_search_rightmost (function)

Searches an array sorted in ascending order. When `value` is found, returns the index of its last occurrence; otherwise returns the index at which `value` would be inserted to keep the array sorted: the index of the smallest element larger than `value`, or the length of the array when every element is smaller. The array must already be sorted.

### syntax

```
array.binary_search_rightmost(series array id, series <type of the array's elements> value) → series int
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to search for.

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("array.binary_search_rightmost Example", overlay=false)
levels = array.from(10.0, 20.0, 30.0, 40.0)
// 25 is not in the array: the result points at 30 (index 2)
plot(array.binary_search_rightmost(levels, 25.0), title="Rightmost Index", color=color.blue)
```

### id

function:array.binary_search_rightmost

## array.clear (function)

Removes every element, leaving an empty array. The array itself remains usable.

### syntax

```
array.clear(series array id) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.clear Example", overlay=true)
static array<float> sessionCloses = array.new_float(0)
// Start collecting again at every new session
if session.isfirst {
    array.clear(sessionCloses)
}
array.push(sessionCloses, close)
plot(array.avg(sessionCloses), title="Session Average Close", color=color.blue)
```

### id

function:array.clear

## array.concat (function)

Appends the elements of `id2` to the end of `id1` and returns `id1`. `id2` is not changed.

### syntax

```
array.concat(series array id1, series array id2) → series array
```

### args

- `id1`: series array
  The array to append to.
  types: series array, simple array, input array, const array, literal array
- `id2`: series array
  The array whose elements are appended.
  types: series array, simple array, input array, const array, literal array

### returnedType

series array

### example

```lipi
//@lipi=2
indicator("array.concat Example", overlay=false)
a = array.from(1.0, 2.0)
b = array.from(3.0, 4.0)
array.concat(a, b)
// a is now 1.0, 2.0, 3.0, 4.0
plot(array.length(a), title="Length (4)", color=color.blue)
```

### id

function:array.concat

## array.copy (function)

Returns a new array with the same elements.

The copy has its own slots and its own length: replacing, adding or removing an element of the copy does not change the original. It is a shallow copy: elements that are objects of a custom type or drawings are the same ones in both arrays, so a change made inside one of them shows through both.

### syntax

```
array.copy(series array id) → series array
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series array

### example

```lipi
//@lipi=2
indicator("array.copy Example", overlay=false)
original = array.from(3.0, 1.0, 2.0)
sorted = array.copy(original)
array.sort(sorted, order.ascending)
// original is unchanged: 3.0, 1.0, 2.0
plot(array.get(original, 0) - array.get(sorted, 0), title="3 - 1", color=color.blue)
```

### id

function:array.copy

## array.covariance (function)

Returns the covariance of two arrays of the same size.

`biased` chooses the estimate: true (the default) divides by the number of elements, false by one less.

### syntax

```
array.covariance(series array id1, series array id2, series bool biased) → series float
```

### args

- `id1`: series array
  The first array.
  types: series array, simple array, input array, const array, literal array
- `id2`: series array
  The second array.
  types: series array, simple array, input array, const array, literal array
- `biased?`: series bool
  Determines which estimate should be used. Optional. The default is true.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: true

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("array.covariance Example", overlay=false)
static array<float> a = array.new_float(20, close)
static array<float> b = array.new_float(20, volume)
array.shift(a)
array.push(a, close)
array.shift(b)
array.push(b, volume)
plot(array.covariance(a, b), title="Close/Volume Covariance", color=color.blue)
```

### id

function:array.covariance

## array.every (function)

Returns true when every element is true. It takes a bool, int or float array: a number counts as true when it is not zero. An `na` element makes the result false, and for an empty array the result is true.

### syntax

```
array.every(series array id) → series bool
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("array.every Example", overlay=true)
rising = array.from(close > close[1], close[1] > close[2], close[2] > close[3])
threeUp = array.every(rising)
bgcolor(threeUp ? color.new(color.green, 0.2) : na)
```

### id

function:array.every

## array.fill (function)

Sets elements of the array to `value`. With no index arguments every element is set; `index_from` and `index_to` limit the change to a range, where `index_to` is not included.

### syntax

```
array.fill(series array id, series <type of the array's elements> value, series int index_from, series int index_to) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to set the elements to.
- `index_from?`: series int
  Index of the first element to set. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `index_to?`: series int
  Index at which the range ends. That element is not set. Optional.
  types: series int, simple int, input int, const int, literal int
  default: na

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.fill Example", overlay=true)
values = array.new<float>(5)
array.fill(values, 0.0)
// Set elements 1 and 2 to the close
array.fill(values, close, 1, 3)
plot(array.sum(values), title="Sum (2 x close)", color=color.blue)
```

### id

function:array.fill

## array.first (function)

Returns the first element of the array. The array must not be empty.

### syntax

```
array.first(series array id) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.first Example", overlay=true)
values = array.from(open, close)
plot(array.first(values), title="Open", color=color.blue)
```

### id

function:array.first

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. Int and float values can be mixed (`array.from(1, 2.5)` is an `array<float>`); a string cannot be mixed with another type. At most 4000 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series int arg0, arg1, ...) → series array<int>
```

### args

- `arg0, arg1, ...`: series int
  The values to put in the array, in order.
  types: series int, simple int, input int, const int, literal int

### returnedType

series array<int>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~1

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. Int and float values can be mixed (`array.from(1, 2.5)` is an `array<float>`); a string cannot be mixed with another type. At most 4000 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series float arg0, arg1, ...) → series array<float>
```

### args

- `arg0, arg1, ...`: series float
  The values to put in the array, in order.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series array<float>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~2

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 4000 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series bool arg0, arg1, ...) → series array<bool>
```

### args

- `arg0, arg1, ...`: series bool
  The values to put in the array, in order.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool

### returnedType

series array<bool>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~3

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 999 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series string arg0, arg1, ...) → series array<string>
```

### args

- `arg0, arg1, ...`: series string
  The values to put in the array, in order.
  types: series string, simple string, input string, const string, literal string

### returnedType

series array<string>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~4

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 4000 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series color arg0, arg1, ...) → series array<color>
```

### args

- `arg0, arg1, ...`: series color
  The values to put in the array, in order.
  types: series color, simple color, input color, const color, literal color

### returnedType

series array<color>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~5

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 999 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series label arg0, arg1, ...) → series array<label>
```

### args

- `arg0, arg1, ...`: series label
  The values to put in the array, in order.
  types: series label, simple label, input label, const label, literal label

### returnedType

series array<label>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~6

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 999 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series line arg0, arg1, ...) → series array<line>
```

### args

- `arg0, arg1, ...`: series line
  The values to put in the array, in order.
  types: series line, simple line, input line, const line, literal line

### returnedType

series array<line>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~7

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 999 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series box arg0, arg1, ...) → series array<box>
```

### args

- `arg0, arg1, ...`: series box
  The values to put in the array, in order.
  types: series box, simple box, input box, const box, literal box

### returnedType

series array<box>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~8

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 999 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series linefill arg0, arg1, ...) → series array<linefill>
```

### args

- `arg0, arg1, ...`: series linefill
  The values to put in the array, in order.
  types: series linefill, simple linefill, input linefill, const linefill, literal linefill

### returnedType

series array<linefill>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~9

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 999 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series polyline arg0, arg1, ...) → series array<polyline>
```

### args

- `arg0, arg1, ...`: series polyline
  The values to put in the array, in order.
  types: series polyline, simple polyline, input polyline, const polyline, literal polyline

### returnedType

series array<polyline>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~10

## array.from (function)

Creates an array from the values passed to it, in order.

The element type is the type of the overload. At most 999 values are accepted; more stop the script with a runtime error.

### syntax

```
array.from(series table arg0, arg1, ...) → series array<table>
```

### args

- `arg0, arg1, ...`: series table
  The values to put in the array, in order.
  types: series table, simple table, input table, const table, literal table

### returnedType

series array<table>

### example

```lipi
//@lipi=2
indicator("array.from Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.avg(prices), title="OHLC Average", color=color.blue)
```

### id

function:array.from~11

## array.get (function)

Returns the element at `index`. Indexes start at 0; an index outside the array is an error.

### syntax

```
array.get(series array id, series int index) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `index`: series int
  Index of the element to return. Indexes start at 0.
  types: series int, simple int, input int, const int, literal int

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.get Example", overlay=true)
values = array.from(open, high, low, close)
plot(array.get(values, 1), title="High (element 1)", color=color.green)
```

### id

function:array.get

## array.includes (function)

Returns true when `value` is one of the array's elements.

### syntax

```
array.includes(series array id, series <type of the array's elements> value) → series bool
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to search for.

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("array.includes Example", overlay=true)
weekend = array.from(1, 7)
// dayofweek counts Sunday as 1 and Saturday as 7
isWeekend = array.includes(weekend, dayofweek)
bgcolor(isWeekend ? color.new(color.gray, 0.3) : na)
```

### id

function:array.includes

## array.indexof (function)

Returns the index of the first element equal to `value`, or -1 when no element matches.

### syntax

```
array.indexof(series array id, series <type of the array's elements> value) → series int
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to search for.

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("array.indexof Example", overlay=false)
levels = array.from(100.0, 200.0, 300.0)
pos = array.indexof(levels, 200.0)
plot(pos, title="Index of 200 (1)", color=color.blue)
```

### id

function:array.indexof

## array.insert (function)

Inserts `value` at `index`, moving the element that was there, and every element after it, up one index.

### syntax

```
array.insert(series array id, series int index, series <type of the array's elements> value) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `index`: series int
  Index at which to insert the value.
  types: series int, simple int, input int, const int, literal int
- `value`: series <type of the array's elements>
  The value to insert.

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.insert Example", overlay=false)
values = array.from(1.0, 3.0)
array.insert(values, 1, 2.0)
// values is now 1.0, 2.0, 3.0
plot(array.get(values, 1), title="Inserted Value", color=color.blue)
```

### id

function:array.insert

## array.join (function)

Joins the elements into one string, with `separator` between them.

### syntax

```
array.join(series array id, series string separator) → series string
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `separator?`: series string
  String to place between the elements. Optional.
  types: series string, simple string, input string, const string, literal string
  default: ""

### returnedType

series string

### example

```lipi
//@lipi=2
indicator("array.join Example", overlay=true)
parts = array.from("O", "H", "L", "C")
if barstate.islast {
    label.new(bar_index, high, text=array.join(parts, " / "))
}
```

### id

function:array.join

## array.last (function)

Returns the last element of the array. The array must not be empty.

### syntax

```
array.last(series array id) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.last Example", overlay=true)
values = array.from(open, close)
plot(array.last(values), title="Close", color=color.blue)
```

### id

function:array.last

## array.lastindexof (function)

Returns the index of the last element equal to `value`, or -1 when no element matches.

### syntax

```
array.lastindexof(series array id, series <type of the array's elements> value) → series int
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to search for.

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("array.lastindexof Example", overlay=false)
values = array.from(1.0, 2.0, 1.0)
plot(array.lastindexof(values, 1.0), title="Last Index of 1 (2)", color=color.blue)
```

### id

function:array.lastindexof

## array.length (function)

Returns the number of elements in the array.

### syntax

```
array.length(series array id) → series int
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("array.length Example", overlay=false)
static array<float> highs = array.new_float(0)
if high > high[1] {
    array.push(highs, high)
}
plot(array.length(highs), title="Higher Highs So Far", color=color.blue)
```

### id

function:array.length

## array.max (function)

Returns the largest element. With `nth`, returns the nth largest instead, counting from 0.

The result has the element type of the array: `int` for an int array, `float` for a float array. `na` elements are left out. The result is `na` when none is left, and with `nth` when `nth` is negative or not smaller than the number of elements left.

### syntax

```
array.max(series array id, series int nth) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `nth?`: series int
  Which largest element to return, counting from 0. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.max Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.max(prices), title="Largest (High)", color=color.green)
plot(array.max(prices, 1), title="Second Largest", color=color.lime)
```

### id

function:array.max

## array.median (function)

Returns the median of the array's elements: the middle value once they are sorted, or the mean of the two middle values when the count is even.

### syntax

```
array.median(series array id) → series float
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("array.median Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.median(prices), title="Median of OHLC", color=color.blue)
```

### id

function:array.median

## array.min (function)

Returns the smallest element. With `nth`, returns the nth smallest instead, counting from 0.

The result has the element type of the array: `int` for an int array, `float` for a float array. `na` elements are left out. The result is `na` when none is left, and with `nth` when `nth` is negative or not smaller than the number of elements left.

### syntax

```
array.min(series array id, series int nth) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `nth?`: series int
  Which smallest element to return, counting from 0. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.min Example", overlay=true)
prices = array.from(open, high, low, close)
plot(array.min(prices), title="Smallest (Low)", color=color.red)
plot(array.min(prices, 1), title="Second Smallest", color=color.orange)
```

### id

function:array.min

## array.mode (function)

Returns the most frequent element. When several values are equally frequent, the smallest of them is returned.

The result has the element type of the array: `int` for an int array, `float` for a float array.

### syntax

```
array.mode(series array id) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.mode Example", overlay=false)
values = array.from(1.0, 2.0, 2.0, 3.0)
plot(array.mode(values), title="Mode (2)", color=color.blue)
```

### id

function:array.mode

## array.new (function)

Creates an array of the given length. The element type is written in angle brackets, as in `array.new<float>(10)`.

Optional `initial_value` fills every slot in one step (elements stay `na` when it is omitted). The value must match the array's element type.

### syntax

```
array.new(series int length, series <type of the array's elements> initial_value) → series array
```

### args

- `length?`: series int
  Number of elements. Default is 0 (empty array).
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series <type of the array's elements>
  Value copied into every element when `length` is greater than 0. Optional; omitted slots are `na`. Must be compatible with the array element type.
  default: na

### returnedType

series array

### notes

- `array.new<bool>(n)` starts with `na` elements, while `array.new_bool(n)` starts with `false`.

### example

```lipi
//@lipi=2
indicator("array.new Example", overlay=false)
static array<float> values = array.new<float>(5, 0.0)
array.set(values, 0, close)
plot(array.get(values, 0), title="First Element", color=color.blue)
```

### id

function:array.new

## array.new_bool (function)

Creates an array of `bool` elements with `size` elements, each set to `initial_value`.

Both arguments are optional: leave `size` out for an empty array, and `initial_value` out for elements that start as `false`. This differs from the other typed constructors and from `array.new<bool>`, whose elements start as `na`.

### syntax

```
array.new_bool(series int size, series bool initial_value) → series array<bool>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series bool
  Value each element is set to. Optional.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: false

### returnedType

series array<bool>

### example

```lipi
//@lipi=2
indicator("array.new_bool Example", overlay=true)
// Remember whether each of the last 3 bars closed up
static array<bool> ups = array.new_bool(3, false)
array.shift(ups)
array.push(ups, close > open)
allUp = array.every(ups)
bgcolor(allUp ? color.new(color.green, 0.2) : na)
```

### id

function:array.new_bool

## array.new_box (function)

Creates an array of `box` IDs with `size` elements, each set to `initial_value`.

Arrays of drawing IDs are the usual way to keep a limited history of drawings: push each new box and delete the oldest when the array grows past a limit. Both arguments are optional; elements start as `na` when `initial_value` is left out.

### syntax

```
array.new_box(series int size, series box initial_value) → series array<box>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series box
  Value each element is set to. Optional.
  types: series box, simple box, input box, const box, literal box
  default: na

### returnedType

series array<box>

### example

```lipi
//@lipi=2
indicator("array.new_box Example", overlay=true)
// Keep only the 3 most recent inside-bar boxes
static array<box> boxes = array.new_box(0)
if high < high[1] and low > low[1] {
    array.push(boxes, box.new(bar_index[1], high[1], bar_index, low[1], border_color=color.orange, bgcolor=color.new(color.orange, 0.2), textcolor=color.white))
    if array.length(boxes) > 3 {
        box.delete(array.shift(boxes))
    }
}
```

### id

function:array.new_box

## array.new_color (function)

Creates an array of `color` elements with `size` elements, each set to `initial_value`.

Both arguments are optional: leave `size` out for an empty array, and `initial_value` out for elements that start as `na`.

### syntax

```
array.new_color(series int size, series color initial_value) → series array<color>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series color
  Value each element is set to. Optional.
  types: series color, simple color, input color, const color, literal color
  default: na

### returnedType

series array<color>

### example

```lipi
//@lipi=2
indicator("array.new_color Example", overlay=true)
palette = array.new_color(0)
array.push(palette, color.red)
array.push(palette, color.green)
array.push(palette, color.blue)
// Cycle through the palette bar by bar
barcolor(array.get(palette, bar_index % array.length(palette)))
```

### id

function:array.new_color

## array.new_float (function)

Creates an array of `float` elements with `size` elements, each set to `initial_value`.

Both arguments are optional: leave `size` out for an empty array, and `initial_value` out for elements that start as `na`.

### syntax

```
array.new_float(series int size, series float initial_value) → series array<float>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series float
  Value each element is set to. Optional.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na

### returnedType

series array<float>

### example

```lipi
//@lipi=2
indicator("array.new_float Example", overlay=true)
// Keep the last 10 closes
static array<float> closes = array.new_float(10, close)
array.shift(closes)
array.push(closes, close)
plot(array.avg(closes), title="Average of Last 10 Closes", color=color.blue)
```

### id

function:array.new_float

## array.new_int (function)

Creates an array of `int` elements with `size` elements, each set to `initial_value`.

Both arguments are optional: leave `size` out for an empty array, and `initial_value` out for elements that start as `na`.

### syntax

```
array.new_int(series int size, series int initial_value) → series array<int>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series int
  Value each element is set to. Optional.
  types: series int, simple int, input int, const int, literal int
  default: na

### returnedType

series array<int>

### example

```lipi
//@lipi=2
indicator("array.new_int Example", overlay=false)
// Count up-bars and down-bars: slot 0 = up, slot 1 = down
static array<int> counts = array.new_int(2, 0)
if close > open {
    array.set(counts, 0, array.get(counts, 0) + 1)
} else if close < open {
    array.set(counts, 1, array.get(counts, 1) + 1)
}
plot(array.get(counts, 0) - array.get(counts, 1), title="Up minus Down Bars", color=color.blue)
```

### id

function:array.new_int

## array.new_label (function)

Creates an array of `label` IDs with `size` elements, each set to `initial_value`.

Arrays of drawing IDs are the usual way to keep a limited history of drawings: push each new label and delete the oldest when the array grows past a limit. Both arguments are optional; elements start as `na` when `initial_value` is left out.

### syntax

```
array.new_label(series int size, series label initial_value) → series array<label>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series label
  Value each element is set to. Optional.
  types: series label, simple label, input label, const label, literal label
  default: na

### returnedType

series array<label>

### example

```lipi
//@lipi=2
indicator("array.new_label Example", overlay=true)
// Keep only the 5 most recent high labels
static array<label> labels = array.new_label(0)
ph = talib.pivothigh(high, 3, 3)
if not na(ph) {
    array.push(labels, label.new(bar_index[3], high[3], text="PH"))
    if array.length(labels) > 5 {
        label.delete(array.shift(labels))
    }
}
```

### id

function:array.new_label

## array.new_line (function)

Creates an array of `line` IDs with `size` elements, each set to `initial_value`.

Arrays of drawing IDs are the usual way to keep a limited history of drawings: push each new line and delete the oldest when the array grows past a limit. Both arguments are optional; elements start as `na` when `initial_value` is left out.

### syntax

```
array.new_line(series int size, series line initial_value) → series array<line>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series line
  Value each element is set to. Optional.
  types: series line, simple line, input line, const line, literal line
  default: na

### returnedType

series array<line>

### example

```lipi
//@lipi=2
indicator("array.new_line Example", overlay=true)
// Keep only the 3 most recent horizontal lines at each new 20-bar high
static array<line> lines = array.new_line(0)
if high == talib.highest(high, 20) {
    array.push(lines, line.new(bar_index, high, bar_index + 10, high, color=color.green))
    if array.length(lines) > 3 {
        line.delete(array.shift(lines))
    }
}
```

### id

function:array.new_line

## array.new_linefill (function)

Creates an array of `linefill` IDs with `size` elements, each set to `initial_value`.

Arrays of drawing IDs are the usual way to keep a limited history of drawings: push each new linefill and delete the oldest when the array grows past a limit. Both arguments are optional; elements start as `na` when `initial_value` is left out.

### syntax

```
array.new_linefill(series int size, series linefill initial_value) → series array<linefill>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series linefill
  Value each element is set to. Optional.
  types: series linefill, simple linefill, input linefill, const linefill, literal linefill
  default: na

### returnedType

series array<linefill>

### example

```lipi
//@lipi=2
indicator("array.new_linefill Example", overlay=true)
static array<linefill> fills = array.new_linefill(0)
if barstate.islast {
    l1 = line.new(bar_index[20], high[20], bar_index, high, color=color.green)
    l2 = line.new(bar_index[20], low[20], bar_index, low, color=color.red)
    array.push(fills, linefill.new(l1, l2, color.new(color.blue, 0.2)))
}
```

### id

function:array.new_linefill

## array.new_string (function)

Creates an array of `string` elements with `size` elements, each set to `initial_value`.

Both arguments are optional: leave `size` out for an empty array, and `initial_value` out for elements that start as `na`.

### syntax

```
array.new_string(series int size, series string initial_value) → series array<string>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series string
  Value each element is set to. Optional.
  types: series string, simple string, input string, const string, literal string
  default: na

### returnedType

series array<string>

### example

```lipi
//@lipi=2
indicator("array.new_string Example", overlay=true)
names = array.new_string(0)
array.push(names, "Open")
array.push(names, "High")
array.push(names, "Low")
if barstate.islast {
    label.new(bar_index, high, text=array.join(names, ", "))
}
```

### id

function:array.new_string

## array.new_table (function)

Creates an array of `table` IDs with `size` elements, each set to `initial_value`.

Arrays of drawing IDs are the usual way to keep a limited history of drawings: push each new table and delete the oldest when the array grows past a limit. Both arguments are optional; elements start as `na` when `initial_value` is left out.

### syntax

```
array.new_table(series int size, series table initial_value) → series array<table>
```

### args

- `size?`: series int
  Number of elements in the array. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `initial_value?`: series table
  Value each element is set to. Optional.
  types: series table, simple table, input table, const table, literal table
  default: na

### returnedType

series array<table>

### example

```lipi
//@lipi=2
indicator("array.new_table Example", overlay=true)
static array<table> tables = array.new_table(0)
if barstate.islast {
    t = table.new(position.top_right, 1, 1, bgcolor=color.gray)
    table.cell(t, 0, 0, text="Close: " + str.tostring(math.round(close, 2)))
    array.push(tables, t)
}
```

### id

function:array.new_table

## array.percentile_linear_interpolation (function)

Returns the value below which `percentage` percent of the elements fall, interpolating between the two nearest elements.

### syntax

```
array.percentile_linear_interpolation(series array id, series float percentage) → series float
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `percentage`: series float
  Percentage, a number from range 0..100.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("array.percentile_linear_interpolation Example", overlay=true)
static array<float> closes = array.new_float(50, close)
array.shift(closes)
array.push(closes, close)
plot(array.percentile_linear_interpolation(closes, 90), title="90th Percentile", color=color.blue)
```

### id

function:array.percentile_linear_interpolation

## array.percentile_nearest_rank (function)

Returns the value below which `percentage` percent of the elements fall, using the nearest element rather than interpolating.

The result has the element type of the array: `int` for an int array, `float` for a float array. A `percentage` below 0 or above 100 is taken as 0 or 100.

### syntax

```
array.percentile_nearest_rank(series array id, series float percentage) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `percentage`: series float
  Percentage, a number from range 0..100.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.percentile_nearest_rank Example", overlay=true)
static array<float> closes = array.new_float(50, close)
array.shift(closes)
array.push(closes, close)
plot(array.percentile_nearest_rank(closes, 10), title="10th Percentile", color=color.blue)
```

### id

function:array.percentile_nearest_rank

## array.percentrank (function)

Returns the percentile rank of the element at `index`: the percentage of elements that are less than or equal to it.

### syntax

```
array.percentrank(series array id, series int index) → series float
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `index`: series int
  Index of the element to rank.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("array.percentrank Example", overlay=false)
static array<float> closes = array.new_float(50, close)
array.shift(closes)
array.push(closes, close)
// Where does the latest close rank among the last 50?
plot(array.percentrank(closes, array.length(closes) - 1), title="Percent Rank", color=color.blue)
```

### id

function:array.percentrank

## array.pop (function)

Removes the last element of the array and returns it.

### syntax

```
array.pop(series array id) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.pop Example", overlay=false)
values = array.from(1.0, 2.0, 3.0)
lastValue = array.pop(values)
// lastValue is 3.0 and the array now holds 1.0, 2.0
plot(lastValue + array.length(values), title="3 + 2", color=color.blue)
```

### id

function:array.pop

## array.push (function)

Appends `value` to the end of the array, growing it by one element.

### syntax

```
array.push(series array id, series <type of the array's elements> value) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to append.

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.push Example", overlay=false)
static array<float> closes = array.new_float(0)
array.push(closes, close)
plot(array.length(closes), title="Elements Pushed", color=color.blue)
```

### id

function:array.push

## array.range (function)

Returns the difference between the largest and the smallest element.

The result has the element type of the array: `int` for an int array, `float` for a float array.

### syntax

```
array.range(series array id) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.range Example", overlay=false)
prices = array.from(open, high, low, close)
plot(array.range(prices), title="Bar Range", color=color.blue)
```

### id

function:array.range

## array.remove (function)

Removes the element at `index`. It returns nothing. The elements after it move down one index.

To keep the element, read it with `array.get` before the call.

### syntax

```
array.remove(series array id, series int index) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `index`: series int
  Index of the element to remove.
  types: series int, simple int, input int, const int, literal int

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.remove Example", overlay=false)
values = array.from(10.0, 20.0, 30.0)
removed = array.get(values, 1)
array.remove(values, 1)
// removed is 20.0 and the array now holds 10.0, 30.0
plot(removed, title="Removed Value", color=color.blue)
```

### id

function:array.remove

## array.removeAll (function)

Removes all elements from the array, leaving it empty.

### syntax

```
array.removeAll(series array id) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.removeAll Example", overlay=false)
values = array.from(1.0, 2.0, 3.0)
array.removeAll(values)
plot(array.length(values), title="Length After removeAll (0)", color=color.blue)
```

### id

function:array.removeAll

## array.reverse (function)

Reverses the order of the elements, in place.

### syntax

```
array.reverse(series array id) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.reverse Example", overlay=false)
values = array.from(1.0, 2.0, 3.0)
array.reverse(values)
plot(array.get(values, 0), title="First After Reverse (3)", color=color.blue)
```

### id

function:array.reverse

## array.set (function)

Replaces the element at `index` with `value`. The array keeps its size.

### syntax

```
array.set(series array id, series int index, series <type of the array's elements> value) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `index`: series int
  Index of the element to replace.
  types: series int, simple int, input int, const int, literal int
- `value`: series <type of the array's elements>
  The value to put at `index`.

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.set Example", overlay=true)
static array<float> last = array.new_float(1, 0.0)
array.set(last, 0, close)
plot(array.get(last, 0), title="Stored Close", color=color.blue)
```

### id

function:array.set

## array.shift (function)

Removes the first element of the array and returns it. The remaining elements move down one index.

Paired with `array.push`, it keeps a fixed-length window of recent values.

### syntax

```
array.shift(series array id) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.shift Example", overlay=true)
// A rolling window of the last 5 closes
static array<float> window = array.new_float(5, close)
array.shift(window)
array.push(window, close)
plot(array.avg(window), title="5-Bar Average", color=color.blue)
```

### id

function:array.shift

## array.slice (function)

Returns the part of the array from `index_from` up to, but not including, `index_to`.

The slice has its own length and shares the original's element slots over that range: replacing an element in one (with `array.set`, for example) shows in the other. The two lengths are independent, but an operation that shifts or overwrites shared slots (removing an element from the slice, for example) can change the original's contents too, and adding elements may move one of them to separate storage. Use `array.copy` on the slice when you need an independent array.

### syntax

```
array.slice(series array id, series int index_from, series int index_to) → series array
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `index_from?`: series int
  Index of the first element of the slice. Optional.
  types: series int, simple int, input int, const int, literal int
  default: 0
- `index_to?`: series int
  Index at which the slice ends. That element is not included. Optional.
  types: series int, simple int, input int, const int, literal int
  default: na

### returnedType

series array

### example

```lipi
//@lipi=2
indicator("array.slice Example", overlay=false)
values = array.from(10.0, 20.0, 30.0, 40.0, 50.0)
middle = array.slice(values, 1, 4)
// middle holds 20.0, 30.0, 40.0
plot(array.avg(middle), title="Average of Middle Three", color=color.blue)
```

### id

function:array.slice

## array.some (function)

Returns true when at least one element is true. It takes a bool, int or float array: a number counts as true when it is not zero. `na` elements are skipped, and for an empty array the result is false.

### syntax

```
array.some(series array id) → series bool
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series bool

### example

```lipi
//@lipi=2
indicator("array.some Example", overlay=true)
gaps = array.from(open > high[1], open < low[1])
anyGap = array.some(gaps)
bgcolor(anyGap ? color.new(color.orange, 0.2) : na)
```

### id

function:array.some

## array.sort (function)

Sorts the array in place. `order` is `order.ascending` (the default) or `order.descending`.

### syntax

```
array.sort(series array id, series string order) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `order?`: series string
  Sort order: `order.ascending` (the default) or `order.descending`. Optional.
  types: series string, simple string, input string, const string, literal string
  values: order.ascending, order.descending
  default: order.ascending

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.sort Example", overlay=false)
values = array.from(3.0, 1.0, 2.0)
array.sort(values, order.descending)
plot(array.get(values, 0), title="Largest First (3)", color=color.blue)
```

### id

function:array.sort

## array.sort_indices (function)

Returns an int array of indexes that would sort the array, leaving the array itself unchanged. `order` is `order.ascending` (the default) or `order.descending`.

### syntax

```
array.sort_indices(series array id, series string order) → series array<int>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `order?`: series string
  Sort order: `order.ascending` (the default) or `order.descending`. Optional.
  types: series string, simple string, input string, const string, literal string
  values: order.ascending, order.descending
  default: order.ascending

### returnedType

series array<int>

### example

```lipi
//@lipi=2
indicator("array.sort_indices Example", overlay=true)
prices = array.from(open, high, low, close)
idx = array.sort_indices(prices, order.ascending)
// The first index points at the smallest price
plot(array.get(prices, array.get(idx, 0)), title="Lowest of OHLC", color=color.red)
```

### id

function:array.sort_indices

## array.standardize (function)

Returns a new array of z-scores: each element minus the mean, divided by the standard deviation. The original array is not changed.

### syntax

```
array.standardize(series array id) → series array<float>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series array<float>

### example

```lipi
//@lipi=2
indicator("array.standardize Example", overlay=false)
static array<float> closes = array.new_float(20, close)
array.shift(closes)
array.push(closes, close)
z = array.standardize(closes)
plot(array.last(z), title="Z-Score of Latest Close", color=color.blue)
```

### id

function:array.standardize

## array.stdev (function)

Returns the standard deviation of the array's elements.

`biased` chooses the estimate: true (the default) divides by the number of elements, false by one less.

### syntax

```
array.stdev(series array id, series bool biased) → series float
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `biased?`: series bool
  Determines which estimate should be used. Optional. The default is true.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: true

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("array.stdev Example", overlay=false)
static array<float> closes = array.new_float(20, close)
array.shift(closes)
array.push(closes, close)
plot(array.stdev(closes), title="20-Bar Standard Deviation", color=color.blue)
```

### id

function:array.stdev

## array.sum (function)

Returns the sum of the array's elements.

The result has the element type of the array: `int` for an int array, `float` for a float array.

### syntax

```
array.sum(series array id) → series <type of the array's elements>
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array

### returnedType

series <type of the array's elements>

### example

```lipi
//@lipi=2
indicator("array.sum Example", overlay=false)
static array<float> vols = array.new_float(10, 0.0)
array.shift(vols)
array.push(vols, volume)
plot(array.sum(vols), title="10-Bar Volume Total", color=color.blue)
```

### id

function:array.sum

## array.unshift (function)

Inserts `value` at the beginning of the array. The existing elements move up one index.

### syntax

```
array.unshift(series array id, series <type of the array's elements> value) → void
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `value`: series <type of the array's elements>
  The value to insert at the beginning.

### returnedType

void

### example

```lipi
//@lipi=2
indicator("array.unshift Example", overlay=false)
values = array.from(2.0, 3.0)
array.unshift(values, 1.0)
// values is now 1.0, 2.0, 3.0
plot(array.get(values, 0), title="First Element", color=color.blue)
```

### id

function:array.unshift

## array.variance (function)

Returns the variance of the array's elements.

`biased` chooses the estimate: true (the default) divides by the number of elements, false by one less.

### syntax

```
array.variance(series array id, series bool biased) → series float
```

### args

- `id`: series array
  The array.
  types: series array, simple array, input array, const array, literal array
- `biased?`: series bool
  Determines which estimate should be used. Optional. The default is true.
  types: series bool, series int, simple int, input int, const int, literal int, series float, simple float, input float, const float, literal float, simple bool, input bool, const bool, literal bool
  default: true

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("array.variance Example", overlay=false)
static array<float> closes = array.new_float(20, close)
array.shift(closes)
array.push(closes, close)
plot(array.variance(closes), title="20-Bar Variance", color=color.blue)
```

### id

function:array.variance
