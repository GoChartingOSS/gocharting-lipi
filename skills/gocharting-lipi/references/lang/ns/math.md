Contents: math (library) · math.abs (function) · math.abs (function) · math.abs (function) · math.abs (function) · math.abs (function) · math.abs (function) · math.abs (function) · math.abs (function) · math.acos (function) · math.acos (function) · math.acos (function) · math.acos (function) · math.asin (function) · math.asin (function) · math.asin (function) · math.asin (function) · math.atan (function) · math.atan (function) · math.atan (function) · math.atan (function) · math.avg (function) · math.avg (function) · math.avg (function) · math.avg (function) · math.ceil (function) · math.ceil (function) · math.ceil (function) · math.ceil (function) · math.cos (function) · math.cos (function) · math.cos (function) · math.cos (function) · math.e (constant) · math.exp (function) · math.exp (function) · math.exp (function) · math.exp (function) · math.floor (function) · math.floor (function) · math.floor (function) · math.floor (function) · math.log (function) · math.log (function) · math.log (function) · math.log (function) · math.log10 (function) · math.log10 (function) · math.log10 (function) · math.log10 (function) · math.max (function) · math.max (function) · math.max (function) · math.max (function) · math.max (function) · math.max (function) · math.max (function) · math.max (function) · math.min (function) · math.min (function) · math.min (function) · math.min (function) · math.min (function) · math.min (function) · math.min (function) · math.min (function) · math.phi (constant) · math.pi (constant) · math.pow (function) · math.pow (function) · math.pow (function) · math.pow (function) · math.random (function) · math.round (function) · math.round (function) · math.round (function) · math.round (function) · math.round (function) · math.round (function) · math.round (function) · math.round (function) · math.round_to_mintick (function) · math.round_to_mintick (function) · math.round_to_mintick (function) · math.round_to_mintick (function) · math.rphi (constant) · math.sign (function) · math.sign (function) · math.sign (function) · math.sign (function) · math.sin (function) · math.sin (function) · math.sin (function) · math.sin (function) · math.sqrt (function) · math.sqrt (function) · math.sqrt (function) · math.sqrt (function) · math.sum (function) · math.tan (function) · math.tan (function) · math.tan (function) · math.tan (function) · math.todegrees (function) · math.todegrees (function) · math.todegrees (function) · math.todegrees (function) · math.toradians (function) · math.toradians (function) · math.toradians (function) · math.toradians (function)

# math

## math (library)

Twenty-three arithmetic and trigonometric functions, and four constants: `math.pi`, `math.e`, `math.phi` and `math.rphi`.

`math.log` is the natural logarithm (base e); `math.log10` is the base-10 logarithm.

### example

```lipi
//@lipi=2
indicator("math Library Example", overlay=false)
// Percentage change, rounded to 2 decimals and capped at +/-10
pct = (close - close[1]) / close[1] * 100
capped = math.max(-10, math.min(10, math.round(pct, 2)))
plot(capped, title="Change % (capped)", color=color.blue)
```

### id

library:math

## math.abs (function)

The absolute value of `number`: its magnitude, with the sign removed.

### syntax

```
math.abs(const int number) → const int
```

### args

- `number`: const int
  The number to use in the calculation.
  types: const int, literal int

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("math.abs Example", overlay=false)
change = math.abs(close - open)
plot(change, title="Candle Body Size", color=color.blue)
```

### id

function:math.abs~1

## math.abs (function)

The absolute value of `number`: its magnitude, with the sign removed.

### syntax

```
math.abs(input int number) → input int
```

### args

- `number`: input int
  The number to use in the calculation.
  types: input int, const int, literal int

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("math.abs Example", overlay=false)
change = math.abs(close - open)
plot(change, title="Candle Body Size", color=color.blue)
```

### id

function:math.abs~2

## math.abs (function)

The absolute value of `number`: its magnitude, with the sign removed.

### syntax

```
math.abs(simple int number) → simple int
```

### args

- `number`: simple int
  The number to use in the calculation.
  types: simple int, input int, const int, literal int

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("math.abs Example", overlay=false)
change = math.abs(close - open)
plot(change, title="Candle Body Size", color=color.blue)
```

### id

function:math.abs~3

## math.abs (function)

The absolute value of `number`: its magnitude, with the sign removed.

### syntax

```
math.abs(series int number) → series int
```

### args

- `number`: series int
  The number to use in the calculation.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("math.abs Example", overlay=false)
change = math.abs(close - open)
plot(change, title="Candle Body Size", color=color.blue)
```

### id

function:math.abs~4

## math.abs (function)

The absolute value of `number`: its magnitude, with the sign removed.

### syntax

```
math.abs(const float number) → const float
```

### args

- `number`: const float
  The number to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.abs Example", overlay=false)
change = math.abs(close - open)
plot(change, title="Candle Body Size", color=color.blue)
```

### id

function:math.abs~5

## math.abs (function)

The absolute value of `number`: its magnitude, with the sign removed.

### syntax

```
math.abs(input float number) → input float
```

### args

- `number`: input float
  The number to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.abs Example", overlay=false)
change = math.abs(close - open)
plot(change, title="Candle Body Size", color=color.blue)
```

### id

function:math.abs~6

## math.abs (function)

The absolute value of `number`: its magnitude, with the sign removed.

### syntax

```
math.abs(simple float number) → simple float
```

### args

- `number`: simple float
  The number to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.abs Example", overlay=false)
change = math.abs(close - open)
plot(change, title="Candle Body Size", color=color.blue)
```

### id

function:math.abs~7

## math.abs (function)

The absolute value of `number`: its magnitude, with the sign removed.

### syntax

```
math.abs(series float number) → series float
```

### args

- `number`: series float
  The number to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.abs Example", overlay=false)
change = math.abs(close - open)
plot(change, title="Candle Body Size", color=color.blue)
```

### id

function:math.abs~8

## math.acos (function)

The arccosine of `angle`, in radians.

It is defined for a value from -1 to 1.

### syntax

```
math.acos(const float angle) → const float
```

### args

- `angle`: const float
  The value, in radians, to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.acos Example", overlay=false)
angle = math.acos(0.5)
plot(math.todegrees(angle), title="acos(0.5) in Degrees (60)", color=color.blue)
```

### id

function:math.acos~1

## math.acos (function)

The arccosine of `angle`, in radians.

It is defined for a value from -1 to 1.

### syntax

```
math.acos(input float angle) → input float
```

### args

- `angle`: input float
  The value, in radians, to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.acos Example", overlay=false)
angle = math.acos(0.5)
plot(math.todegrees(angle), title="acos(0.5) in Degrees (60)", color=color.blue)
```

### id

function:math.acos~2

## math.acos (function)

The arccosine of `angle`, in radians.

It is defined for a value from -1 to 1.

### syntax

```
math.acos(simple float angle) → simple float
```

### args

- `angle`: simple float
  The value, in radians, to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.acos Example", overlay=false)
angle = math.acos(0.5)
plot(math.todegrees(angle), title="acos(0.5) in Degrees (60)", color=color.blue)
```

### id

function:math.acos~3

## math.acos (function)

The arccosine of `angle`, in radians.

It is defined for a value from -1 to 1.

### syntax

```
math.acos(series float angle) → series float
```

### args

- `angle`: series float
  The value, in radians, to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.acos Example", overlay=false)
angle = math.acos(0.5)
plot(math.todegrees(angle), title="acos(0.5) in Degrees (60)", color=color.blue)
```

### id

function:math.acos~4

## math.asin (function)

The arcsine of `angle`, in radians.

It is defined for a value from -1 to 1.

### syntax

```
math.asin(const float angle) → const float
```

### args

- `angle`: const float
  The value, in radians, to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.asin Example", overlay=false)
angle = math.asin(0.5)
plot(math.todegrees(angle), title="asin(0.5) in Degrees (30)", color=color.blue)
```

### id

function:math.asin~1

## math.asin (function)

The arcsine of `angle`, in radians.

It is defined for a value from -1 to 1.

### syntax

```
math.asin(input float angle) → input float
```

### args

- `angle`: input float
  The value, in radians, to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.asin Example", overlay=false)
angle = math.asin(0.5)
plot(math.todegrees(angle), title="asin(0.5) in Degrees (30)", color=color.blue)
```

### id

function:math.asin~2

## math.asin (function)

The arcsine of `angle`, in radians.

It is defined for a value from -1 to 1.

### syntax

```
math.asin(simple float angle) → simple float
```

### args

- `angle`: simple float
  The value, in radians, to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.asin Example", overlay=false)
angle = math.asin(0.5)
plot(math.todegrees(angle), title="asin(0.5) in Degrees (30)", color=color.blue)
```

### id

function:math.asin~3

## math.asin (function)

The arcsine of `angle`, in radians.

It is defined for a value from -1 to 1.

### syntax

```
math.asin(series float angle) → series float
```

### args

- `angle`: series float
  The value, in radians, to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.asin Example", overlay=false)
angle = math.asin(0.5)
plot(math.todegrees(angle), title="asin(0.5) in Degrees (30)", color=color.blue)
```

### id

function:math.asin~4

## math.atan (function)

The arctangent of `angle`, in radians.

It is defined for every number.

### syntax

```
math.atan(const float angle) → const float
```

### args

- `angle`: const float
  The value, in radians, to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.atan Example", overlay=false)
// Slope of a 10-bar change, as an angle
slopeAngle = math.todegrees(math.atan((close - close[10]) / 10))
plot(slopeAngle, title="Slope Angle", color=color.blue)
```

### id

function:math.atan~1

## math.atan (function)

The arctangent of `angle`, in radians.

It is defined for every number.

### syntax

```
math.atan(input float angle) → input float
```

### args

- `angle`: input float
  The value, in radians, to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.atan Example", overlay=false)
// Slope of a 10-bar change, as an angle
slopeAngle = math.todegrees(math.atan((close - close[10]) / 10))
plot(slopeAngle, title="Slope Angle", color=color.blue)
```

### id

function:math.atan~2

## math.atan (function)

The arctangent of `angle`, in radians.

It is defined for every number.

### syntax

```
math.atan(simple float angle) → simple float
```

### args

- `angle`: simple float
  The value, in radians, to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.atan Example", overlay=false)
// Slope of a 10-bar change, as an angle
slopeAngle = math.todegrees(math.atan((close - close[10]) / 10))
plot(slopeAngle, title="Slope Angle", color=color.blue)
```

### id

function:math.atan~3

## math.atan (function)

The arctangent of `angle`, in radians.

It is defined for every number.

### syntax

```
math.atan(series float angle) → series float
```

### args

- `angle`: series float
  The value, in radians, to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.atan Example", overlay=false)
// Slope of a 10-bar change, as an angle
slopeAngle = math.todegrees(math.atan((close - close[10]) / 10))
plot(slopeAngle, title="Slope Angle", color=color.blue)
```

### id

function:math.atan~4

## math.avg (function)

The arithmetic mean of the numbers you pass: their sum divided by how many there are.

It averages the arguments in the one call. It does not average a value across bars, and it takes no length argument.

### syntax

```
math.avg(const float number0, number1, ...) → const float
```

### args

- `number0, number1, ...`: const float
  A sequence of numbers to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("Math Avg Example", overlay=true)
val1 = close
val2 = open
avgValue = math.avg(val1, val2)
plot(avgValue, color=color.blue, title="Average")
```

### id

function:math.avg~1

## math.avg (function)

The arithmetic mean of the numbers you pass: their sum divided by how many there are.

It averages the arguments in the one call. It does not average a value across bars, and it takes no length argument.

### syntax

```
math.avg(input float number0, number1, ...) → input float
```

### args

- `number0, number1, ...`: input float
  A sequence of numbers to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("Math Avg Example", overlay=true)
val1 = close
val2 = open
avgValue = math.avg(val1, val2)
plot(avgValue, color=color.blue, title="Average")
```

### id

function:math.avg~2

## math.avg (function)

The arithmetic mean of the numbers you pass: their sum divided by how many there are.

It averages the arguments in the one call. It does not average a value across bars, and it takes no length argument.

### syntax

```
math.avg(simple float number0, number1, ...) → simple float
```

### args

- `number0, number1, ...`: simple float
  A sequence of numbers to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("Math Avg Example", overlay=true)
val1 = close
val2 = open
avgValue = math.avg(val1, val2)
plot(avgValue, color=color.blue, title="Average")
```

### id

function:math.avg~3

## math.avg (function)

The arithmetic mean of the numbers you pass: their sum divided by how many there are.

It averages the arguments in the one call. It does not average a value across bars, and it takes no length argument.

### syntax

```
math.avg(series float number0, number1, ...) → series float
```

### args

- `number0, number1, ...`: series float
  A sequence of numbers to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("Math Avg Example", overlay=true)
val1 = close
val2 = open
avgValue = math.avg(val1, val2)
plot(avgValue, color=color.blue, title="Average")
```

### id

function:math.avg~4

## math.ceil (function)

The smallest whole number that is not less than `number`.

The result is an int, not a float.

### syntax

```
math.ceil(const float number) → const int
```

### args

- `number`: const float
  The number to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("math.ceil Example", overlay=false)
roundedUp = math.ceil(close)
plot(roundedUp, title="Close Rounded Up", color=color.blue)
```

### id

function:math.ceil~1

## math.ceil (function)

The smallest whole number that is not less than `number`.

The result is an int, not a float.

### syntax

```
math.ceil(input float number) → input int
```

### args

- `number`: input float
  The number to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("math.ceil Example", overlay=false)
roundedUp = math.ceil(close)
plot(roundedUp, title="Close Rounded Up", color=color.blue)
```

### id

function:math.ceil~2

## math.ceil (function)

The smallest whole number that is not less than `number`.

The result is an int, not a float.

### syntax

```
math.ceil(simple float number) → simple int
```

### args

- `number`: simple float
  The number to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("math.ceil Example", overlay=false)
roundedUp = math.ceil(close)
plot(roundedUp, title="Close Rounded Up", color=color.blue)
```

### id

function:math.ceil~3

## math.ceil (function)

The smallest whole number that is not less than `number`.

The result is an int, not a float.

### syntax

```
math.ceil(series float number) → series int
```

### args

- `number`: series float
  The number to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("math.ceil Example", overlay=false)
roundedUp = math.ceil(close)
plot(roundedUp, title="Close Rounded Up", color=color.blue)
```

### id

function:math.ceil~4

## math.cos (function)

The cosine of `angle`, where the angle is in radians.

### syntax

```
math.cos(const float angle) → const float
```

### args

- `angle`: const float
  Angle, in radians.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.cos Example", overlay=false)
wave = math.cos(bar_index * math.pi / 10)
plot(wave, title="Cosine Wave", color=color.blue)
```

### id

function:math.cos~1

## math.cos (function)

The cosine of `angle`, where the angle is in radians.

### syntax

```
math.cos(input float angle) → input float
```

### args

- `angle`: input float
  Angle, in radians.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.cos Example", overlay=false)
wave = math.cos(bar_index * math.pi / 10)
plot(wave, title="Cosine Wave", color=color.blue)
```

### id

function:math.cos~2

## math.cos (function)

The cosine of `angle`, where the angle is in radians.

### syntax

```
math.cos(simple float angle) → simple float
```

### args

- `angle`: simple float
  Angle, in radians.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.cos Example", overlay=false)
wave = math.cos(bar_index * math.pi / 10)
plot(wave, title="Cosine Wave", color=color.blue)
```

### id

function:math.cos~3

## math.cos (function)

The cosine of `angle`, where the angle is in radians.

### syntax

```
math.cos(series float angle) → series float
```

### args

- `angle`: series float
  Angle, in radians.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.cos Example", overlay=false)
wave = math.cos(bar_index * math.pi / 10)
plot(wave, title="Cosine Wave", color=color.blue)
```

### id

function:math.cos~4

## math.e (constant)

Euler's number: the base of the natural logarithm, 2.718281828459045.

### type

const float

### example

```lipi
//@lipi=2
indicator("math.e Example", overlay=false)
// math.log(math.e) is 1
plot(math.log(math.e), title="ln(e)", color=color.blue)
```

### id

constant:math.e

## math.exp (function)

Euler's number raised to the power of `number`.

It is the inverse of math.log.

### syntax

```
math.exp(const float number) → const float
```

### args

- `number`: const float
  The number to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.exp Example", overlay=false)
growth = math.exp(0.01 * (bar_index % 100))
plot(growth, title="Exponential Growth", color=color.blue)
```

### id

function:math.exp~1

## math.exp (function)

Euler's number raised to the power of `number`.

It is the inverse of math.log.

### syntax

```
math.exp(input float number) → input float
```

### args

- `number`: input float
  The number to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.exp Example", overlay=false)
growth = math.exp(0.01 * (bar_index % 100))
plot(growth, title="Exponential Growth", color=color.blue)
```

### id

function:math.exp~2

## math.exp (function)

Euler's number raised to the power of `number`.

It is the inverse of math.log.

### syntax

```
math.exp(simple float number) → simple float
```

### args

- `number`: simple float
  The number to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.exp Example", overlay=false)
growth = math.exp(0.01 * (bar_index % 100))
plot(growth, title="Exponential Growth", color=color.blue)
```

### id

function:math.exp~3

## math.exp (function)

Euler's number raised to the power of `number`.

It is the inverse of math.log.

### syntax

```
math.exp(series float number) → series float
```

### args

- `number`: series float
  The number to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.exp Example", overlay=false)
growth = math.exp(0.01 * (bar_index % 100))
plot(growth, title="Exponential Growth", color=color.blue)
```

### id

function:math.exp~4

## math.floor (function)

The largest whole number that is not greater than `number`.

The result is an int, not a float.

### syntax

```
math.floor(const float number) → const int
```

### args

- `number`: const float
  The number to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("math.floor Example", overlay=false)
roundedDown = math.floor(close)
plot(roundedDown, title="Close Rounded Down", color=color.blue)
```

### id

function:math.floor~1

## math.floor (function)

The largest whole number that is not greater than `number`.

The result is an int, not a float.

### syntax

```
math.floor(input float number) → input int
```

### args

- `number`: input float
  The number to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("math.floor Example", overlay=false)
roundedDown = math.floor(close)
plot(roundedDown, title="Close Rounded Down", color=color.blue)
```

### id

function:math.floor~2

## math.floor (function)

The largest whole number that is not greater than `number`.

The result is an int, not a float.

### syntax

```
math.floor(simple float number) → simple int
```

### args

- `number`: simple float
  The number to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("math.floor Example", overlay=false)
roundedDown = math.floor(close)
plot(roundedDown, title="Close Rounded Down", color=color.blue)
```

### id

function:math.floor~3

## math.floor (function)

The largest whole number that is not greater than `number`.

The result is an int, not a float.

### syntax

```
math.floor(series float number) → series int
```

### args

- `number`: series float
  The number to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("math.floor Example", overlay=false)
roundedDown = math.floor(close)
plot(roundedDown, title="Close Rounded Down", color=color.blue)
```

### id

function:math.floor~4

## math.log (function)

The natural logarithm of `number`: its logarithm to base e.

It is defined for a number greater than zero. For base 10, use `math.log10`.

### syntax

```
math.log(const float number) → const float
```

### args

- `number`: const float
  The number to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### notes

- The compiler also accepts `math.log10`. `math.log2` is rejected.

### example

```lipi
//@lipi=2
indicator("math.log Example", overlay=false)
// Log return from the previous bar
logReturn = math.log(close / close[1])
plot(logReturn, title="Log Return", color=color.blue)
```

### id

function:math.log~1

## math.log (function)

The natural logarithm of `number`: its logarithm to base e.

It is defined for a number greater than zero. For base 10, use `math.log10`.

### syntax

```
math.log(input float number) → input float
```

### args

- `number`: input float
  The number to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### notes

- The compiler also accepts `math.log10`. `math.log2` is rejected.

### example

```lipi
//@lipi=2
indicator("math.log Example", overlay=false)
// Log return from the previous bar
logReturn = math.log(close / close[1])
plot(logReturn, title="Log Return", color=color.blue)
```

### id

function:math.log~2

## math.log (function)

The natural logarithm of `number`: its logarithm to base e.

It is defined for a number greater than zero. For base 10, use `math.log10`.

### syntax

```
math.log(simple float number) → simple float
```

### args

- `number`: simple float
  The number to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### notes

- The compiler also accepts `math.log10`. `math.log2` is rejected.

### example

```lipi
//@lipi=2
indicator("math.log Example", overlay=false)
// Log return from the previous bar
logReturn = math.log(close / close[1])
plot(logReturn, title="Log Return", color=color.blue)
```

### id

function:math.log~3

## math.log (function)

The natural logarithm of `number`: its logarithm to base e.

It is defined for a number greater than zero. For base 10, use `math.log10`.

### syntax

```
math.log(series float number) → series float
```

### args

- `number`: series float
  The number to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### notes

- The compiler also accepts `math.log10`. `math.log2` is rejected.

### example

```lipi
//@lipi=2
indicator("math.log Example", overlay=false)
// Log return from the previous bar
logReturn = math.log(close / close[1])
plot(logReturn, title="Log Return", color=color.blue)
```

### id

function:math.log~4

## math.log10 (function)

The base-10 logarithm of `number`.

It is defined for a number greater than zero; otherwise the result is `na`.

### syntax

```
math.log10(const float number) → const float
```

### args

- `number`: const float
  The number to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.log10 Example", overlay=false)
plot(math.log10(close), title="Log10 Close", color=color.blue)
```

### id

function:math.log10~1

## math.log10 (function)

The base-10 logarithm of `number`.

It is defined for a number greater than zero; otherwise the result is `na`.

### syntax

```
math.log10(input float number) → input float
```

### args

- `number`: input float
  The number to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.log10 Example", overlay=false)
plot(math.log10(close), title="Log10 Close", color=color.blue)
```

### id

function:math.log10~2

## math.log10 (function)

The base-10 logarithm of `number`.

It is defined for a number greater than zero; otherwise the result is `na`.

### syntax

```
math.log10(simple float number) → simple float
```

### args

- `number`: simple float
  The number to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.log10 Example", overlay=false)
plot(math.log10(close), title="Log10 Close", color=color.blue)
```

### id

function:math.log10~3

## math.log10 (function)

The base-10 logarithm of `number`.

It is defined for a number greater than zero; otherwise the result is `na`.

### syntax

```
math.log10(series float number) → series float
```

### args

- `number`: series float
  The number to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.log10 Example", overlay=false)
plot(math.log10(close), title="Log10 Close", color=color.blue)
```

### id

function:math.log10~4

## math.max (function)

The largest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.max(const int number0, number1, ...) → const int
```

### args

- `number0, number1, ...`: const int
  A list of numbers to perform the calculation on.
  types: const int, literal int

### returnedType

const int

### returnDesc

The greatest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.max", overlay=true)
plot(math.max(open,close))
```

### id

function:math.max~1

## math.max (function)

The largest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.max(input int number0, number1, ...) → input int
```

### args

- `number0, number1, ...`: input int
  A list of numbers to perform the calculation on.
  types: input int, const int, literal int

### returnedType

input int

### returnDesc

The greatest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.max", overlay=true)
plot(math.max(open,close))
```

### id

function:math.max~2

## math.max (function)

The largest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.max(simple int number0, number1, ...) → simple int
```

### args

- `number0, number1, ...`: simple int
  A list of numbers to perform the calculation on.
  types: simple int, input int, const int, literal int

### returnedType

simple int

### returnDesc

The greatest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.max", overlay=true)
plot(math.max(open,close))
```

### id

function:math.max~3

## math.max (function)

The largest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.max(series int number0, number1, ...) → series int
```

### args

- `number0, number1, ...`: series int
  A list of numbers to perform the calculation on.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### returnDesc

The greatest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.max", overlay=true)
plot(math.max(open,close))
```

### id

function:math.max~4

## math.max (function)

The largest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.max(const float number0, number1, ...) → const float
```

### args

- `number0, number1, ...`: const float
  A list of numbers to perform the calculation on.
  types: const float, const int, literal int, literal float

### returnedType

const float

### returnDesc

The greatest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.max", overlay=true)
plot(math.max(open,close))
```

### id

function:math.max~5

## math.max (function)

The largest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.max(input float number0, number1, ...) → input float
```

### args

- `number0, number1, ...`: input float
  A list of numbers to perform the calculation on.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### returnDesc

The greatest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.max", overlay=true)
plot(math.max(open,close))
```

### id

function:math.max~6

## math.max (function)

The largest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.max(simple float number0, number1, ...) → simple float
```

### args

- `number0, number1, ...`: simple float
  A list of numbers to perform the calculation on.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### returnDesc

The greatest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.max", overlay=true)
plot(math.max(open,close))
```

### id

function:math.max~7

## math.max (function)

The largest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.max(series float number0, number1, ...) → series float
```

### args

- `number0, number1, ...`: series float
  A list of numbers to perform the calculation on.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### returnDesc

The greatest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.max", overlay=true)
plot(math.max(open,close))
```

### id

function:math.max~8

## math.min (function)

The smallest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.min(const int number0, number1, ...) → const int
```

### args

- `number0, number1, ...`: const int
  A list of numbers to perform the calculation on.
  types: const int, literal int

### returnedType

const int

### returnDesc

The smallest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.min", overlay=true)
plot(math.min(open,close))
```

### id

function:math.min~1

## math.min (function)

The smallest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.min(input int number0, number1, ...) → input int
```

### args

- `number0, number1, ...`: input int
  A list of numbers to perform the calculation on.
  types: input int, const int, literal int

### returnedType

input int

### returnDesc

The smallest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.min", overlay=true)
plot(math.min(open,close))
```

### id

function:math.min~2

## math.min (function)

The smallest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.min(simple int number0, number1, ...) → simple int
```

### args

- `number0, number1, ...`: simple int
  A list of numbers to perform the calculation on.
  types: simple int, input int, const int, literal int

### returnedType

simple int

### returnDesc

The smallest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.min", overlay=true)
plot(math.min(open,close))
```

### id

function:math.min~3

## math.min (function)

The smallest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.min(series int number0, number1, ...) → series int
```

### args

- `number0, number1, ...`: series int
  A list of numbers to perform the calculation on.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### returnDesc

The smallest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.min", overlay=true)
plot(math.min(open,close))
```

### id

function:math.min~4

## math.min (function)

The smallest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.min(const float number0, number1, ...) → const float
```

### args

- `number0, number1, ...`: const float
  A list of numbers to perform the calculation on.
  types: const float, const int, literal int, literal float

### returnedType

const float

### returnDesc

The smallest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.min", overlay=true)
plot(math.min(open,close))
```

### id

function:math.min~5

## math.min (function)

The smallest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.min(input float number0, number1, ...) → input float
```

### args

- `number0, number1, ...`: input float
  A list of numbers to perform the calculation on.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### returnDesc

The smallest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.min", overlay=true)
plot(math.min(open,close))
```

### id

function:math.min~6

## math.min (function)

The smallest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.min(simple float number0, number1, ...) → simple float
```

### args

- `number0, number1, ...`: simple float
  A list of numbers to perform the calculation on.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### returnDesc

The smallest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.min", overlay=true)
plot(math.min(open,close))
```

### id

function:math.min~7

## math.min (function)

The smallest of the numbers you pass.

It compares the arguments in the one call. It does not look back over bars, and it takes no length argument.

### syntax

```
math.min(series float number0, number1, ...) → series float
```

### args

- `number0, number1, ...`: series float
  A list of numbers to perform the calculation on.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### returnDesc

The smallest of the given numbers.

### example

```lipi
//@lipi=2
indicator("math.min", overlay=true)
plot(math.min(open,close))
```

### id

function:math.min~8

## math.phi (constant)

The golden ratio: the positive number whose square is one greater than itself, 1.618033988749895.

### type

const float

### example

```lipi
//@lipi=2
indicator("math.phi Example", overlay=true)
// A level at the golden ratio of the 50-bar range
hi = talib.highest(high, 50)
lo = talib.lowest(low, 50)
plot(lo + (hi - lo) / math.phi, title="Golden Ratio Level", color=color.orange)
```

### id

constant:math.phi

## math.pi (constant)

Archimedes' constant: the ratio of a circle's circumference to its diameter, 3.141592653589793.

### type

const float

### example

```lipi
//@lipi=2
indicator("math.pi Example", overlay=false)
// A sine wave with a 20-bar period
plot(math.sin(2 * math.pi * bar_index / 20), title="Sine Wave", color=color.blue)
```

### id

constant:math.pi

## math.pow (function)

`base` raised to the power of `exponent`.

The language has no exponentiation operator: a token for one exists in the lexer but no rule reaches it, so source containing `^` does not parse. This function is how you raise a number to a power.

### syntax

```
math.pow(const float base, const float exponent) → const float
```

### args

- `base`: const float
  Specify the base to use.
  types: const float, const int, literal int, literal float
- `exponent`: const float
  Specifies the exponent.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.pow Example", overlay=false)
squared = math.pow(close - open, 2)
plot(squared, title="Squared Body", color=color.blue)
```

### id

function:math.pow~1

## math.pow (function)

`base` raised to the power of `exponent`.

The language has no exponentiation operator: a token for one exists in the lexer but no rule reaches it, so source containing `^` does not parse. This function is how you raise a number to a power.

### syntax

```
math.pow(input float base, input float exponent) → input float
```

### args

- `base`: input float
  Specify the base to use.
  types: input float, input int, const int, literal int, const float, literal float
- `exponent`: input float
  Specifies the exponent.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.pow Example", overlay=false)
squared = math.pow(close - open, 2)
plot(squared, title="Squared Body", color=color.blue)
```

### id

function:math.pow~2

## math.pow (function)

`base` raised to the power of `exponent`.

The language has no exponentiation operator: a token for one exists in the lexer but no rule reaches it, so source containing `^` does not parse. This function is how you raise a number to a power.

### syntax

```
math.pow(simple float base, simple float exponent) → simple float
```

### args

- `base`: simple float
  Specify the base to use.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
- `exponent`: simple float
  Specifies the exponent.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.pow Example", overlay=false)
squared = math.pow(close - open, 2)
plot(squared, title="Squared Body", color=color.blue)
```

### id

function:math.pow~3

## math.pow (function)

`base` raised to the power of `exponent`.

The language has no exponentiation operator: a token for one exists in the lexer but no rule reaches it, so source containing `^` does not parse. This function is how you raise a number to a power.

### syntax

```
math.pow(series float base, series float exponent) → series float
```

### args

- `base`: series float
  Specify the base to use.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `exponent`: series float
  Specifies the exponent.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.pow Example", overlay=false)
squared = math.pow(close - open, 2)
plot(squared, title="Squared Body", color=color.blue)
```

### id

function:math.pow~4

## math.random (function)

Gives your script a random float, bounded below by `min` and above by `max`.

Both bounds are optional. There is no seed argument, so a result cannot be reproduced. Keep the value out of anything a reader is meant to compare between runs.

It has a single form, series. A series value is refused wherever a narrower form is required, so this result cannot fill a const, input or simple argument - a script's title, for instance.

### syntax

```
math.random(series float min, series float max) → series float
```

### args

- `min?`: series float
  The lower bound of the range of random values. The value is included in the range. The default is 0.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: 0
- `max?`: series float
  The upper bound of the range of random values. The value is not included in the range. The default is 1.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: 1

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.random Example", overlay=false)
noise = math.random(-1, 1)
plot(noise, title="Random Value", color=color.gray)
```

### id

function:math.random

## math.round (function)

Rounds `number` to the nearest whole number and returns an int.

Pass a `precision` as well and the function keeps decimal places instead: the result is then a float, not an int. That change of return type is the practical difference between the two forms, so pick the form by what you need back - an int to count with, a float to plot.

In the series form the precision is itself series, so how many places you keep can differ from bar to bar.

### syntax

```
math.round(const float number) → const int
```

### args

- `number`: const float
  The value to be rounded.
  types: const float, const int, literal int, literal float

### returnedType

const int

### example

```lipi
//@lipi=2
indicator("math.round Example", overlay=false)
rounded = math.round(close, 2)
plot(rounded, title="Close to 2 Decimals", color=color.blue)
```

### id

function:math.round~1

## math.round (function)

Rounds `number` to the nearest whole number and returns an int.

Pass a `precision` as well and the function keeps decimal places instead: the result is then a float, not an int. That change of return type is the practical difference between the two forms, so pick the form by what you need back - an int to count with, a float to plot.

In the series form the precision is itself series, so how many places you keep can differ from bar to bar.

### syntax

```
math.round(input float number) → input int
```

### args

- `number`: input float
  The value to be rounded.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input int

### example

```lipi
//@lipi=2
indicator("math.round Example", overlay=false)
rounded = math.round(close, 2)
plot(rounded, title="Close to 2 Decimals", color=color.blue)
```

### id

function:math.round~2

## math.round (function)

Rounds `number` to the nearest whole number and returns an int.

Pass a `precision` as well and the function keeps decimal places instead: the result is then a float, not an int. That change of return type is the practical difference between the two forms, so pick the form by what you need back - an int to count with, a float to plot.

In the series form the precision is itself series, so how many places you keep can differ from bar to bar.

### syntax

```
math.round(simple float number) → simple int
```

### args

- `number`: simple float
  The value to be rounded.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple int

### example

```lipi
//@lipi=2
indicator("math.round Example", overlay=false)
rounded = math.round(close, 2)
plot(rounded, title="Close to 2 Decimals", color=color.blue)
```

### id

function:math.round~3

## math.round (function)

Rounds `number` to the nearest whole number and returns an int.

Pass a `precision` as well and the function keeps decimal places instead: the result is then a float, not an int. That change of return type is the practical difference between the two forms, so pick the form by what you need back - an int to count with, a float to plot.

In the series form the precision is itself series, so how many places you keep can differ from bar to bar.

### syntax

```
math.round(series float number) → series int
```

### args

- `number`: series float
  The value to be rounded.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series int

### example

```lipi
//@lipi=2
indicator("math.round Example", overlay=false)
rounded = math.round(close, 2)
plot(rounded, title="Close to 2 Decimals", color=color.blue)
```

### id

function:math.round~4

## math.round (function)

Rounds `number` to the nearest whole number and returns an int.

Pass a `precision` as well and the function keeps decimal places instead: the result is then a float, not an int. That change of return type is the practical difference between the two forms, so pick the form by what you need back - an int to count with, a float to plot.

In the series form the precision is itself series, so how many places you keep can differ from bar to bar.

### syntax

```
math.round(const float number, const int precision) → const float
```

### args

- `number`: const float
  The value to be rounded.
  types: const float, const int, literal int, literal float
- `precision`: const int
  Decimal places to which `number` is rounded.
  types: const int, literal int

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.round Example", overlay=false)
rounded = math.round(close, 2)
plot(rounded, title="Close to 2 Decimals", color=color.blue)
```

### id

function:math.round~5

## math.round (function)

Rounds `number` to the nearest whole number and returns an int.

Pass a `precision` as well and the function keeps decimal places instead: the result is then a float, not an int. That change of return type is the practical difference between the two forms, so pick the form by what you need back - an int to count with, a float to plot.

In the series form the precision is itself series, so how many places you keep can differ from bar to bar.

### syntax

```
math.round(input float number, input int precision) → input float
```

### args

- `number`: input float
  The value to be rounded.
  types: input float, input int, const int, literal int, const float, literal float
- `precision`: input int
  Decimal places to which `number` is rounded.
  types: input int, const int, literal int

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.round Example", overlay=false)
rounded = math.round(close, 2)
plot(rounded, title="Close to 2 Decimals", color=color.blue)
```

### id

function:math.round~6

## math.round (function)

Rounds `number` to the nearest whole number and returns an int.

Pass a `precision` as well and the function keeps decimal places instead: the result is then a float, not an int. That change of return type is the practical difference between the two forms, so pick the form by what you need back - an int to count with, a float to plot.

In the series form the precision is itself series, so how many places you keep can differ from bar to bar.

### syntax

```
math.round(simple float number, simple int precision) → simple float
```

### args

- `number`: simple float
  The value to be rounded.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float
- `precision`: simple int
  Decimal places to which `number` is rounded.
  types: simple int, input int, const int, literal int

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.round Example", overlay=false)
rounded = math.round(close, 2)
plot(rounded, title="Close to 2 Decimals", color=color.blue)
```

### id

function:math.round~7

## math.round (function)

Rounds `number` to the nearest whole number and returns an int.

Pass a `precision` as well and the function keeps decimal places instead: the result is then a float, not an int. That change of return type is the practical difference between the two forms, so pick the form by what you need back - an int to count with, a float to plot.

In the series form the precision is itself series, so how many places you keep can differ from bar to bar.

### syntax

```
math.round(series float number, series int precision) → series float
```

### args

- `number`: series float
  The value to be rounded.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `precision`: series int
  Decimal places to which `number` is rounded.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.round Example", overlay=false)
rounded = math.round(close, 2)
plot(rounded, title="Close to 2 Decimals", color=color.blue)
```

### id

function:math.round~8

## math.round_to_mintick (function)

Rounds `number` to the nearest multiple of `syminfo.mintick` for the chart symbol.

Uses `floor(number / mintick + 0.5) * mintick`. Returns `na` when the input is `na` or when `syminfo.mintick` is not available.

### syntax

```
math.round_to_mintick(const float number) → const float
```

### args

- `number`: const float
  Value to round to the instrument's minimum tick size.
  types: const float, const int, literal int, literal float

### returnedType

const float

### returnDesc

Rounded float on the symbol's tick grid.

### example

```lipi
//@lipi=2
indicator("math.round_to_mintick Example", overlay=true)
plot(math.round_to_mintick(close), title="Close on tick grid")
```

### id

function:math.round_to_mintick~1

## math.round_to_mintick (function)

Rounds `number` to the nearest multiple of `syminfo.mintick` for the chart symbol.

Uses `floor(number / mintick + 0.5) * mintick`. Returns `na` when the input is `na` or when `syminfo.mintick` is not available.

### syntax

```
math.round_to_mintick(input float number) → input float
```

### args

- `number`: input float
  Value to round to the instrument's minimum tick size.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### returnDesc

Rounded float on the symbol's tick grid.

### example

```lipi
//@lipi=2
indicator("math.round_to_mintick Example", overlay=true)
plot(math.round_to_mintick(close), title="Close on tick grid")
```

### id

function:math.round_to_mintick~2

## math.round_to_mintick (function)

Rounds `number` to the nearest multiple of `syminfo.mintick` for the chart symbol.

Uses `floor(number / mintick + 0.5) * mintick`. Returns `na` when the input is `na` or when `syminfo.mintick` is not available.

### syntax

```
math.round_to_mintick(simple float number) → simple float
```

### args

- `number`: simple float
  Value to round to the instrument's minimum tick size.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### returnDesc

Rounded float on the symbol's tick grid.

### example

```lipi
//@lipi=2
indicator("math.round_to_mintick Example", overlay=true)
plot(math.round_to_mintick(close), title="Close on tick grid")
```

### id

function:math.round_to_mintick~3

## math.round_to_mintick (function)

Rounds `number` to the nearest multiple of `syminfo.mintick` for the chart symbol.

Uses `floor(number / mintick + 0.5) * mintick`. Returns `na` when the input is `na` or when `syminfo.mintick` is not available.

### syntax

```
math.round_to_mintick(series float number) → series float
```

### args

- `number`: series float
  Value to round to the instrument's minimum tick size.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### returnDesc

Rounded float on the symbol's tick grid.

### example

```lipi
//@lipi=2
indicator("math.round_to_mintick Example", overlay=true)
plot(math.round_to_mintick(close), title="Close on tick grid")
```

### id

function:math.round_to_mintick~4

## math.rphi (constant)

The golden ratio conjugate: the reciprocal of the golden ratio, 0.6180339887498948.

### type

const float

### example

```lipi
//@lipi=2
indicator("math.rphi Example", overlay=true)
// A 0.618 retracement of the 50-bar range
hi = talib.highest(high, 50)
lo = talib.lowest(low, 50)
plot(hi - (hi - lo) * math.rphi, title="0.618 Retracement", color=color.orange)
```

### id

constant:math.rphi

## math.sign (function)

The sign of `number`: -1 for a negative number and 1 for a positive one.

The result is a float, not an int. Every other member that reduces a number to a whole value - math.ceil, math.floor, the one-argument math.round - returns an int, so this one is worth reading twice.

### syntax

```
math.sign(const float number) → const float
```

### args

- `number`: const float
  The number to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.sign Example", overlay=false)
direction = math.sign(close - close[1])
plot(direction, title="Direction (-1, 0, 1)", color=color.blue)
```

### id

function:math.sign~1

## math.sign (function)

The sign of `number`: -1 for a negative number and 1 for a positive one.

The result is a float, not an int. Every other member that reduces a number to a whole value - math.ceil, math.floor, the one-argument math.round - returns an int, so this one is worth reading twice.

### syntax

```
math.sign(input float number) → input float
```

### args

- `number`: input float
  The number to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.sign Example", overlay=false)
direction = math.sign(close - close[1])
plot(direction, title="Direction (-1, 0, 1)", color=color.blue)
```

### id

function:math.sign~2

## math.sign (function)

The sign of `number`: -1 for a negative number and 1 for a positive one.

The result is a float, not an int. Every other member that reduces a number to a whole value - math.ceil, math.floor, the one-argument math.round - returns an int, so this one is worth reading twice.

### syntax

```
math.sign(simple float number) → simple float
```

### args

- `number`: simple float
  The number to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.sign Example", overlay=false)
direction = math.sign(close - close[1])
plot(direction, title="Direction (-1, 0, 1)", color=color.blue)
```

### id

function:math.sign~3

## math.sign (function)

The sign of `number`: -1 for a negative number and 1 for a positive one.

The result is a float, not an int. Every other member that reduces a number to a whole value - math.ceil, math.floor, the one-argument math.round - returns an int, so this one is worth reading twice.

### syntax

```
math.sign(series float number) → series float
```

### args

- `number`: series float
  The number to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.sign Example", overlay=false)
direction = math.sign(close - close[1])
plot(direction, title="Direction (-1, 0, 1)", color=color.blue)
```

### id

function:math.sign~4

## math.sin (function)

The sine of `angle`, where the angle is in radians.

### syntax

```
math.sin(const float angle) → const float
```

### args

- `angle`: const float
  Angle, in radians.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.sin Example", overlay=false)
wave = math.sin(bar_index * math.pi / 10)
plot(wave, title="Sine Wave", color=color.blue)
```

### id

function:math.sin~1

## math.sin (function)

The sine of `angle`, where the angle is in radians.

### syntax

```
math.sin(input float angle) → input float
```

### args

- `angle`: input float
  Angle, in radians.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.sin Example", overlay=false)
wave = math.sin(bar_index * math.pi / 10)
plot(wave, title="Sine Wave", color=color.blue)
```

### id

function:math.sin~2

## math.sin (function)

The sine of `angle`, where the angle is in radians.

### syntax

```
math.sin(simple float angle) → simple float
```

### args

- `angle`: simple float
  Angle, in radians.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.sin Example", overlay=false)
wave = math.sin(bar_index * math.pi / 10)
plot(wave, title="Sine Wave", color=color.blue)
```

### id

function:math.sin~3

## math.sin (function)

The sine of `angle`, where the angle is in radians.

### syntax

```
math.sin(series float angle) → series float
```

### args

- `angle`: series float
  Angle, in radians.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.sin Example", overlay=false)
wave = math.sin(bar_index * math.pi / 10)
plot(wave, title="Sine Wave", color=color.blue)
```

### id

function:math.sin~4

## math.sqrt (function)

The square root of `number`.

It is defined for a number that is not negative.

### syntax

```
math.sqrt(const float number) → const float
```

### args

- `number`: const float
  The number to use in the calculation.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.sqrt Example", overlay=false)
// Volatility scaled by the square root of time
scaled = talib.stdev(close, 20) * math.sqrt(20)
plot(scaled, title="Scaled Volatility", color=color.blue)
```

### id

function:math.sqrt~1

## math.sqrt (function)

The square root of `number`.

It is defined for a number that is not negative.

### syntax

```
math.sqrt(input float number) → input float
```

### args

- `number`: input float
  The number to use in the calculation.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.sqrt Example", overlay=false)
// Volatility scaled by the square root of time
scaled = talib.stdev(close, 20) * math.sqrt(20)
plot(scaled, title="Scaled Volatility", color=color.blue)
```

### id

function:math.sqrt~2

## math.sqrt (function)

The square root of `number`.

It is defined for a number that is not negative.

### syntax

```
math.sqrt(simple float number) → simple float
```

### args

- `number`: simple float
  The number to use in the calculation.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.sqrt Example", overlay=false)
// Volatility scaled by the square root of time
scaled = talib.stdev(close, 20) * math.sqrt(20)
plot(scaled, title="Scaled Volatility", color=color.blue)
```

### id

function:math.sqrt~3

## math.sqrt (function)

The square root of `number`.

It is defined for a number that is not negative.

### syntax

```
math.sqrt(series float number) → series float
```

### args

- `number`: series float
  The number to use in the calculation.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.sqrt Example", overlay=false)
// Volatility scaled by the square root of time
scaled = talib.stdev(close, 20) * math.sqrt(20)
plot(scaled, title="Scaled Volatility", color=color.blue)
```

### id

function:math.sqrt~4

## math.sum (function)

Adds up the last `length` values of `source`.

Same behavior as `talib.sum` — a moving window, not a running total (`talib.cum`).

### syntax

```
math.sum(series float source, series int length) → series float
```

### args

- `source`: series float
  The series to add up.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
- `length`: series int
  How many bars the window covers.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### returnDesc

A series float total.

### example

```lipi
//@lipi=2
indicator("Sum of Close Prices", overlay=false)
length = input(10, "Sum Length")
sumClose = math.sum(close, length)
plot(sumClose, color=color.blue, title="Sum of Close Prices")
```

### id

function:math.sum

## math.tan (function)

The tangent of `angle`, where the angle is in radians.

### syntax

```
math.tan(const float angle) → const float
```

### args

- `angle`: const float
  Angle, in radians.
  types: const float, const int, literal int, literal float

### returnedType

const float

### notes

- In this build `math.tan` returns `na` when `angle` is exactly 90 (radians); every other value gives the tangent. As the default of `input.float`, `math.tan(90)` is refused when the script is added to the chart ("Argument `defval` of `input.float()` cannot be `na`."), while `math.tan(89)` is accepted.

### example

```lipi
//@lipi=2
indicator("math.tan Example", overlay=false)
value = math.tan(math.pi / 4)
plot(value, title="tan(45 deg) (1)", color=color.blue)
```

### id

function:math.tan~1

## math.tan (function)

The tangent of `angle`, where the angle is in radians.

### syntax

```
math.tan(input float angle) → input float
```

### args

- `angle`: input float
  Angle, in radians.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### notes

- In this build `math.tan` returns `na` when `angle` is exactly 90 (radians); every other value gives the tangent. As the default of `input.float`, `math.tan(90)` is refused when the script is added to the chart ("Argument `defval` of `input.float()` cannot be `na`."), while `math.tan(89)` is accepted.

### example

```lipi
//@lipi=2
indicator("math.tan Example", overlay=false)
value = math.tan(math.pi / 4)
plot(value, title="tan(45 deg) (1)", color=color.blue)
```

### id

function:math.tan~2

## math.tan (function)

The tangent of `angle`, where the angle is in radians.

### syntax

```
math.tan(simple float angle) → simple float
```

### args

- `angle`: simple float
  Angle, in radians.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### notes

- In this build `math.tan` returns `na` when `angle` is exactly 90 (radians); every other value gives the tangent. As the default of `input.float`, `math.tan(90)` is refused when the script is added to the chart ("Argument `defval` of `input.float()` cannot be `na`."), while `math.tan(89)` is accepted.

### example

```lipi
//@lipi=2
indicator("math.tan Example", overlay=false)
value = math.tan(math.pi / 4)
plot(value, title="tan(45 deg) (1)", color=color.blue)
```

### id

function:math.tan~3

## math.tan (function)

The tangent of `angle`, where the angle is in radians.

### syntax

```
math.tan(series float angle) → series float
```

### args

- `angle`: series float
  Angle, in radians.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### notes

- In this build `math.tan` returns `na` when `angle` is exactly 90 (radians); every other value gives the tangent. As the default of `input.float`, `math.tan(90)` is refused when the script is added to the chart ("Argument `defval` of `input.float()` cannot be `na`."), while `math.tan(89)` is accepted.

### example

```lipi
//@lipi=2
indicator("math.tan Example", overlay=false)
value = math.tan(math.pi / 4)
plot(value, title="tan(45 deg) (1)", color=color.blue)
```

### id

function:math.tan~4

## math.todegrees (function)

Converts an angle in radians to the same angle in degrees.

### syntax

```
math.todegrees(const float radians) → const float
```

### args

- `radians`: const float
  Angle in radians.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.todegrees Example", overlay=false)
degrees = math.todegrees(math.pi)
plot(degrees, title="pi in Degrees (180)", color=color.blue)
```

### id

function:math.todegrees~1

## math.todegrees (function)

Converts an angle in radians to the same angle in degrees.

### syntax

```
math.todegrees(input float radians) → input float
```

### args

- `radians`: input float
  Angle in radians.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.todegrees Example", overlay=false)
degrees = math.todegrees(math.pi)
plot(degrees, title="pi in Degrees (180)", color=color.blue)
```

### id

function:math.todegrees~2

## math.todegrees (function)

Converts an angle in radians to the same angle in degrees.

### syntax

```
math.todegrees(simple float radians) → simple float
```

### args

- `radians`: simple float
  Angle in radians.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.todegrees Example", overlay=false)
degrees = math.todegrees(math.pi)
plot(degrees, title="pi in Degrees (180)", color=color.blue)
```

### id

function:math.todegrees~3

## math.todegrees (function)

Converts an angle in radians to the same angle in degrees.

### syntax

```
math.todegrees(series float radians) → series float
```

### args

- `radians`: series float
  Angle in radians.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.todegrees Example", overlay=false)
degrees = math.todegrees(math.pi)
plot(degrees, title="pi in Degrees (180)", color=color.blue)
```

### id

function:math.todegrees~4

## math.toradians (function)

Converts an angle in degrees to the same angle in radians.

The trigonometric functions take radians, so this is the conversion to reach for before calling them.

### syntax

```
math.toradians(const float degrees) → const float
```

### args

- `degrees`: const float
  Angle in degrees.
  types: const float, const int, literal int, literal float

### returnedType

const float

### example

```lipi
//@lipi=2
indicator("math.toradians Example", overlay=false)
radians = math.toradians(180)
plot(radians, title="180 Degrees in Radians (pi)", color=color.blue)
```

### id

function:math.toradians~1

## math.toradians (function)

Converts an angle in degrees to the same angle in radians.

The trigonometric functions take radians, so this is the conversion to reach for before calling them.

### syntax

```
math.toradians(input float degrees) → input float
```

### args

- `degrees`: input float
  Angle in degrees.
  types: input float, input int, const int, literal int, const float, literal float

### returnedType

input float

### example

```lipi
//@lipi=2
indicator("math.toradians Example", overlay=false)
radians = math.toradians(180)
plot(radians, title="180 Degrees in Radians (pi)", color=color.blue)
```

### id

function:math.toradians~2

## math.toradians (function)

Converts an angle in degrees to the same angle in radians.

The trigonometric functions take radians, so this is the conversion to reach for before calling them.

### syntax

```
math.toradians(simple float degrees) → simple float
```

### args

- `degrees`: simple float
  Angle in degrees.
  types: simple float, simple int, input int, const int, literal int, input float, const float, literal float

### returnedType

simple float

### example

```lipi
//@lipi=2
indicator("math.toradians Example", overlay=false)
radians = math.toradians(180)
plot(radians, title="180 Degrees in Radians (pi)", color=color.blue)
```

### id

function:math.toradians~3

## math.toradians (function)

Converts an angle in degrees to the same angle in radians.

The trigonometric functions take radians, so this is the conversion to reach for before calling them.

### syntax

```
math.toradians(series float degrees) → series float
```

### args

- `degrees`: series float
  Angle in degrees.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float

### returnedType

series float

### example

```lipi
//@lipi=2
indicator("math.toradians Example", overlay=false)
radians = math.toradians(180)
plot(radians, title="180 Degrees in Radians (pi)", color=color.blue)
```

### id

function:math.toradians~4
