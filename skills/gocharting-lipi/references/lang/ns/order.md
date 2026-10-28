# order

## order (library)

The two sort orders, `order.ascending` and `order.descending`, for `array.sort` and `array.sort_indices`.

### example

```lipi
//@lipi=2
indicator("order Library Example", overlay=true)
prices = array.from(open, high, low, close)
array.sort(prices, order.descending)
plot(array.get(prices, 0), title="Highest of OHLC", color=color.green)
```

### id

library:order

## order.ascending (constant)

Sort order from the smallest value to the largest, for `array.sort` and `array.sort_indices`.

### type

const string

### example

```lipi
//@lipi=2
indicator("order.ascending Example", overlay=false)
values = array.from(3.0, 1.0, 2.0)
array.sort(values, order.ascending)
plot(array.get(values, 0), title="Smallest (1)", color=color.blue)
```

### id

constant:order.ascending

## order.descending (constant)

Sort order from the largest value to the smallest, for `array.sort` and `array.sort_indices`.

### type

const string

### example

```lipi
//@lipi=2
indicator("order.descending Example", overlay=false)
values = array.from(3.0, 1.0, 2.0)
array.sort(values, order.descending)
plot(array.get(values, 0), title="Largest (3)", color=color.blue)
```

### id

constant:order.descending
