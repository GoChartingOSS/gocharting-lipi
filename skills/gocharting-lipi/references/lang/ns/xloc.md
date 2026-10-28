# xloc

## xloc (library)

Named constants for how drawing x-coordinates are interpreted: bar index or UNIX time.

### example

```lipi
//@lipi=2
indicator("xloc Library Example", overlay=true)
if barstate.islast {
    label.new(bar_index - 5, high[5], text="By bar index", xloc=xloc.bar_index)
    label.new(time[10], high[10], text="By time", xloc=xloc.bar_time)
}
```

### id

library:xloc

## xloc.bar_index (constant)

X-coordinate is a bar index.

### type

const string

### example

```lipi
//@lipi=2
indicator("xloc.bar_index Example", overlay=true)
if barstate.islast {
    // x is a bar index: 10 bars ago
    label.new(bar_index - 10, high[10], text="10 bars ago", xloc=xloc.bar_index)
}
```

### id

constant:xloc.bar_index

## xloc.bar_time (constant)

X-coordinate is a UNIX timestamp in milliseconds.

### type

const string

### example

```lipi
//@lipi=2
indicator("xloc.bar_time Example", overlay=true)
if barstate.islast {
    // x is a UNIX time in milliseconds: the time of the bar 10 bars ago
    label.new(time[10], high[10], text="10 bars ago", xloc=xloc.bar_time)
}
```

### id

constant:xloc.bar_time
