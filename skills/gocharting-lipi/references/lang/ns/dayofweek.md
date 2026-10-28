Contents: dayofweek (library) · dayofweek.friday (constant) · dayofweek.monday (constant) · dayofweek.saturday (constant) · dayofweek.sunday (constant) · dayofweek.thursday (constant) · dayofweek.tuesday (constant) · dayofweek.wednesday (constant)

# dayofweek

## dayofweek (library)

Named weekday constants for comparisons with the `dayofweek` series or `dayofweek(time)`:

`dayofweek.sunday` (`1`), `dayofweek.monday` (`2`), `dayofweek.tuesday` (`3`), `dayofweek.wednesday` (`4`), `dayofweek.thursday` (`5`), `dayofweek.friday` (`6`), `dayofweek.saturday` (`7`).

### example

```lipi
//@lipi=2
indicator("dayofweek constants", overlay=true)
weekend = array.from(dayofweek.saturday, dayofweek.sunday)
isWeekend = array.includes(weekend, dayofweek)
bgcolor(isWeekend ? color.new(color.gray, 0.1) : na)
```

### id

library:dayofweek

## dayofweek.friday (constant)

Weekday constant for Friday, an int with the value 6. Compare it with the `dayofweek` series or with `dayofweek(time)`.

### type

const int

### example

```lipi
//@lipi=2
indicator("dayofweek.friday Example")
isDay = dayofweek == dayofweek.friday
plot(isDay ? 1 : 0, title="Friday")
```

### id

constant:dayofweek.friday

## dayofweek.monday (constant)

Weekday constant for Monday, an int with the value 2. Compare it with the `dayofweek` series or with `dayofweek(time)`.

### type

const int

### example

```lipi
//@lipi=2
indicator("dayofweek.monday Example")
isDay = dayofweek == dayofweek.monday
plot(isDay ? 1 : 0, title="Monday")
```

### id

constant:dayofweek.monday

## dayofweek.saturday (constant)

Weekday constant for Saturday, an int with the value 7. Compare it with the `dayofweek` series or with `dayofweek(time)`.

### type

const int

### example

```lipi
//@lipi=2
indicator("dayofweek.saturday Example")
isDay = dayofweek == dayofweek.saturday
plot(isDay ? 1 : 0, title="Saturday")
```

### id

constant:dayofweek.saturday

## dayofweek.sunday (constant)

Weekday constant for Sunday, an int with the value 1. Compare it with the `dayofweek` series or with `dayofweek(time)`.

### type

const int

### example

```lipi
//@lipi=2
indicator("dayofweek.sunday Example")
isDay = dayofweek == dayofweek.sunday
plot(isDay ? 1 : 0, title="Sunday")
```

### id

constant:dayofweek.sunday

## dayofweek.thursday (constant)

Weekday constant for Thursday, an int with the value 5. Compare it with the `dayofweek` series or with `dayofweek(time)`.

### type

const int

### example

```lipi
//@lipi=2
indicator("dayofweek.thursday Example")
isDay = dayofweek == dayofweek.thursday
plot(isDay ? 1 : 0, title="Thursday")
```

### id

constant:dayofweek.thursday

## dayofweek.tuesday (constant)

Weekday constant for Tuesday, an int with the value 3. Compare it with the `dayofweek` series or with `dayofweek(time)`.

### type

const int

### example

```lipi
//@lipi=2
indicator("dayofweek.tuesday Example")
isDay = dayofweek == dayofweek.tuesday
plot(isDay ? 1 : 0, title="Tuesday")
```

### id

constant:dayofweek.tuesday

## dayofweek.wednesday (constant)

Weekday constant for Wednesday, an int with the value 4. Compare it with the `dayofweek` series or with `dayofweek(time)`.

### type

const int

### example

```lipi
//@lipi=2
indicator("dayofweek.wednesday Example")
isDay = dayofweek == dayofweek.wednesday
plot(isDay ? 1 : 0, title="Wednesday")
```

### id

constant:dayofweek.wednesday
