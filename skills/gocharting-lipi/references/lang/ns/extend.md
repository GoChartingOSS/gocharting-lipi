Contents: extend (library) · extend.both (constant) · extend.left (constant) · extend.none (constant) · extend.right (constant)

# extend

## extend (library)

Named constants that control whether line/box drawings extend past their endpoints (none, left, right, both).

### example

```lipi
//@lipi=2
indicator("extend Library Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], low[20], bar_index, low, color=color.red, extend=extend.right)
    line.new(bar_index[20], high[20], bar_index, high, color=color.green, extend=extend.both)
}
```

### id

library:extend

## extend.both (constant)

Extend the drawing in both directions.

### type

const string

### example

```lipi
//@lipi=2
indicator("extend.both Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], low[20], bar_index, high, color=color.blue, extend=extend.both)
}
```

### id

constant:extend.both

## extend.left (constant)

Extend the drawing to the left of the first point.

### type

const string

### example

```lipi
//@lipi=2
indicator("extend.left Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], low[20], bar_index, high, color=color.blue, extend=extend.left)
}
```

### id

constant:extend.left

## extend.none (constant)

Do not extend the drawing past its endpoints.

### type

const string

### example

```lipi
//@lipi=2
indicator("extend.none Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], low[20], bar_index, high, color=color.blue, extend=extend.none)
}
```

### id

constant:extend.none

## extend.right (constant)

Extend the drawing to the right of the second point.

### type

const string

### example

```lipi
//@lipi=2
indicator("extend.right Example", overlay=true)
if barstate.islast {
    line.new(bar_index[20], low[20], bar_index, high, color=color.blue, extend=extend.right)
}
```

### id

constant:extend.right
