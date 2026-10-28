Contents: strategy (library) · strategy.account_currency (variable) · strategy.cancel (function) · strategy.cancel_all (function) · strategy.close (function) · strategy.close_all (function) · strategy.closedtrades (variable) · strategy.closedtrades_commission (function) · strategy.closedtrades_entry_bar_index (function) · strategy.closedtrades_entry_comment (function) · strategy.closedtrades_entry_id (function) · strategy.closedtrades_entry_price (function) · strategy.closedtrades_entry_time (function) · strategy.closedtrades_exit_bar_index (function) · strategy.closedtrades_exit_price (function) · strategy.closedtrades_exit_time (function) · strategy.closedtrades_max_drawdown (function) · strategy.closedtrades_max_runup (function) · strategy.closedtrades_profit (function) · strategy.closedtrades_size (function) · strategy.commission_cash_per_contract (constant) · strategy.commission_cash_per_order (constant) · strategy.commission_percent (constant) · strategy.entry (function) · strategy.equity (variable) · strategy.exit (function) · strategy.fixed (constant) · strategy.grossloss (variable) · strategy.grossprofit (variable) · strategy.initial_capital (variable) · strategy.long (constant) · strategy.losstrades (variable) · strategy.max_drawdown (variable) · strategy.max_runup (variable) · strategy.netprofit (variable) · strategy.oca_cancel (constant) · strategy.oca_none (constant) · strategy.oca_reduce (constant) · strategy.openprofit (variable) · strategy.opentrades (variable) · strategy.opentrades_entry_bar_index (function) · strategy.opentrades_entry_comment (function) · strategy.opentrades_entry_id (function) · strategy.opentrades_entry_price (function) · strategy.opentrades_entry_time (function) · strategy.opentrades_max_drawdown (function) · strategy.opentrades_max_runup (function) · strategy.opentrades_profit (function) · strategy.opentrades_size (function) · strategy.order (function) · strategy.position_avg_price (variable) · strategy.position_size (variable) · strategy.short (constant) · strategy.wintrades (variable)

# strategy

## strategy (library)

Functions, variables and constants for strategies: scripts declared with `strategy()` that place simulated orders. Orders are placed with `strategy.entry`, `strategy.order`, `strategy.exit`, `strategy.close` and `strategy.close_all`, and cancelled with `strategy.cancel` and `strategy.cancel_all`.

Performance is read through variables such as `strategy.netprofit`, `strategy.equity` and `strategy.position_size`, and trade by trade through the `strategy.closedtrades_*` and `strategy.opentrades_*` functions. Constants such as `strategy.long`, `strategy.fixed` and `strategy.commission_percent` configure orders and the strategy itself.

### example

```lipi
//@lipi=2
strategy("strategy Library Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
fast = talib.ema(close, 9)
slow = talib.ema(close, 21)
if talib.crossover(fast, slow) {
    strategy.entry("Long", strategy.long)
}
if strategy.position_size > 0 {
    strategy.exit("Exit", from_entry="Long", limit=strategy.position_avg_price * 1.03, stop=strategy.position_avg_price * 0.98)
}
plot(fast, title="Fast EMA", color=color.green)
plot(slow, title="Slow EMA", color=color.red)
```

### id

library:strategy

## strategy.account_currency (variable)

The currency the strategy's figures are reported in, as a string.

### type

series string

### example

```lipi
//@lipi=2
strategy("strategy.account_currency Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
if barstate.islast {
    label.new(bar_index, high, text="account_currency: " + strategy.account_currency)
}
```

### id

variable:strategy.account_currency

## strategy.cancel (function)

Cancels the pending order named `id`: a limit or stop order that has not filled yet.

### syntax

```
strategy.cancel(series string id) → void
```

### args

- `id`: series string
  The `id` of the pending order to cancel.
  types: series string, simple string, input string, const string, literal string

### returnedType

void

### example

```lipi
//@lipi=2
strategy("strategy.cancel Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
// A buy limit 1% below the close, cancelled if not filled within the bar
if close > open {
    strategy.entry("Dip Buy", strategy.long, limit=close * 0.99)
} else {
    strategy.cancel("Dip Buy")
}
```

### id

function:strategy.cancel

## strategy.cancel_all (function)

Cancels every pending order that has not filled yet.

### syntax

```
strategy.cancel_all() → void
```

### returnedType

void

### example

```lipi
//@lipi=2
strategy("strategy.cancel_all Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if close > open {
    strategy.entry("Breakout", strategy.long, stop=high * 1.01)
}
// Cancel all waiting orders when volume dries up
if volume < talib.sma(volume, 20) * 0.5 {
    strategy.cancel_all()
}
```

### id

function:strategy.cancel_all

## strategy.close (function)

Closes the position opened by the entry named `id` with a market order. `qty` closes only part of it; `comment` labels the closing order.

### syntax

```
strategy.close(series string id, series float qty, series string comment) → void
```

### args

- `id`: series string
  The `id` of the entry whose position is closed.
  types: series string, simple string, input string, const string, literal string
- `qty?`: series float
  The quantity to close. If given, only part of the position is closed. A `qty` of zero or less, or `na`, closes the whole open quantity of the entry.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `comment?`: series string
  Comment that labels the closing order.
  types: series string, simple string, input string, const string, literal string
  default: ""

### returnedType

void

### example

```lipi
//@lipi=2
strategy("strategy.close Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
// Close after the position has been open for 10 bars
if strategy.opentrades > 0 and bar_index - strategy.opentrades_entry_bar_index(0) >= 10 {
    strategy.close("Long", comment="Time exit")
}
```

### id

function:strategy.close

## strategy.close_all (function)

Closes the whole open position, whatever entries it came from, with a market order.

### syntax

```
strategy.close_all(series string comment) → void
```

### args

- `comment?`: series string
  Comment that labels the closing order.
  types: series string, simple string, input string, const string, literal string
  default: ""

### returnedType

void

### example

```lipi
//@lipi=2
strategy("strategy.close_all Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
// Flatten everything when a new session starts
if session.isfirst and strategy.position_size != 0 {
    strategy.close_all(comment="New session")
}
```

### id

function:strategy.close_all

## strategy.closedtrades (variable)

The number of trades closed so far.

### type

series int

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.closedtrades, title="Closedtrades", color=color.blue)
```

### id

variable:strategy.closedtrades

## strategy.closedtrades_commission (function)

For the closed trade number `trade_num`, returns the commission paid on the trade, in the account currency.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`.

### syntax

```
strategy.closedtrades_commission(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_commission Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_commission(strategy.closedtrades - 1) : na
plot(value, title="Commission", color=color.blue)
```

### id

function:strategy.closedtrades_commission

## strategy.closedtrades_entry_bar_index (function)

For the closed trade number `trade_num`, returns the bar index of the bar on which the entry order was placed (where `strategy.entry` or `strategy.order` ran), not the bar on which it filled; the two differ when the order fills on a later bar.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`. The result is `na` for a number that is not a closed trade, and for a trade that has dropped out of the 1000 most recent closed trades kept.

### syntax

```
strategy.closedtrades_entry_bar_index(series int trade_num) → series int
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_entry_bar_index Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_entry_bar_index(strategy.closedtrades - 1) : na
plot(value, title="Entry Bar Index", color=color.blue)
```

### id

function:strategy.closedtrades_entry_bar_index

## strategy.closedtrades_entry_comment (function)

For the closed trade number `trade_num`, returns the comment of the entry order that opened the trade.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`.

### syntax

```
strategy.closedtrades_entry_comment(series int trade_num) → series string
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series string

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_entry_comment Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
if barstate.islast and strategy.closedtrades > 0 {
    label.new(bar_index, high, text="Last closed trade: " + strategy.closedtrades_entry_comment(strategy.closedtrades - 1))
}
```

### id

function:strategy.closedtrades_entry_comment

## strategy.closedtrades_entry_id (function)

For the closed trade number `trade_num`, returns the `id` of the entry order that opened the trade.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`.

### syntax

```
strategy.closedtrades_entry_id(series int trade_num) → series string
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series string

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_entry_id Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
if barstate.islast and strategy.closedtrades > 0 {
    label.new(bar_index, high, text="Last closed trade: " + strategy.closedtrades_entry_id(strategy.closedtrades - 1))
}
```

### id

function:strategy.closedtrades_entry_id

## strategy.closedtrades_entry_price (function)

For the closed trade number `trade_num`, returns the price at which the trade was entered.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`.

### syntax

```
strategy.closedtrades_entry_price(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_entry_price Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_entry_price(strategy.closedtrades - 1) : na
plot(value, title="Entry Price", color=color.blue)
```

### id

function:strategy.closedtrades_entry_price

## strategy.closedtrades_entry_time (function)

For the closed trade number `trade_num`, returns the UNIX time, in milliseconds, at which the trade was entered.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`.

### syntax

```
strategy.closedtrades_entry_time(series int trade_num) → series int
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_entry_time Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_entry_time(strategy.closedtrades - 1) : na
plot(value, title="Entry Time", color=color.blue)
```

### id

function:strategy.closedtrades_entry_time

## strategy.closedtrades_exit_bar_index (function)

For the closed trade number `trade_num`, returns the bar index at which the trade was closed. In this build it is always 0: the broker does not record the exit bar. `strategy.closedtrades_exit_time` holds the time of the exit.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`. The result is `na` for a number that is not a closed trade, and for a trade that has dropped out of the 1000 most recent closed trades kept.

### syntax

```
strategy.closedtrades_exit_bar_index(series int trade_num) → series int
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_exit_bar_index Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_exit_bar_index(strategy.closedtrades - 1) : na
plot(value, title="Exit Bar Index", color=color.blue)
```

### id

function:strategy.closedtrades_exit_bar_index

## strategy.closedtrades_exit_price (function)

For the closed trade number `trade_num`, returns the price at which the trade was closed.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`.

### syntax

```
strategy.closedtrades_exit_price(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_exit_price Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_exit_price(strategy.closedtrades - 1) : na
plot(value, title="Exit Price", color=color.blue)
```

### id

function:strategy.closedtrades_exit_price

## strategy.closedtrades_exit_time (function)

For the closed trade number `trade_num`, returns the UNIX time, in milliseconds, at which the trade was closed.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`.

### syntax

```
strategy.closedtrades_exit_time(series int trade_num) → series int
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_exit_time Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_exit_time(strategy.closedtrades - 1) : na
plot(value, title="Exit Time", color=color.blue)
```

### id

function:strategy.closedtrades_exit_time

## strategy.closedtrades_max_drawdown (function)

For the closed trade number `trade_num`, returns the largest loss the trade showed while it was open, in the account currency. In this build it is always 0 for a closed trade: the figure measured while the trade was open is not carried into the closed-trade record. `strategy.opentrades_max_drawdown` and `strategy.opentrades_max_runup` are measured.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`. The result is `na` for a number that is not a closed trade, and for a trade that has dropped out of the 1000 most recent closed trades kept.

### syntax

```
strategy.closedtrades_max_drawdown(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_max_drawdown Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_max_drawdown(strategy.closedtrades - 1) : na
plot(value, title="Max Drawdown", color=color.blue)
```

### id

function:strategy.closedtrades_max_drawdown

## strategy.closedtrades_max_runup (function)

For the closed trade number `trade_num`, returns the largest profit the trade showed while it was open, in the account currency. In this build it is always 0 for a closed trade: the figure measured while the trade was open is not carried into the closed-trade record. `strategy.opentrades_max_drawdown` and `strategy.opentrades_max_runup` are measured.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`. The result is `na` for a number that is not a closed trade, and for a trade that has dropped out of the 1000 most recent closed trades kept.

### syntax

```
strategy.closedtrades_max_runup(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_max_runup Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_max_runup(strategy.closedtrades - 1) : na
plot(value, title="Max Runup", color=color.blue)
```

### id

function:strategy.closedtrades_max_runup

## strategy.closedtrades_profit (function)

For the closed trade number `trade_num`, returns the profit of the trade, in the account currency; a loss is negative.

Trades are numbered from 0 in the order they were closed, so the most recent is `strategy.closedtrades - 1`.

### syntax

```
strategy.closedtrades_profit(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_profit Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_profit(strategy.closedtrades - 1) : na
plot(value, title="Profit", color=color.blue)
```

### id

function:strategy.closedtrades_profit

## strategy.closedtrades_size (function)

For the closed trade number `trade_num`, returns the size of the trade. The size is never negative: a short trade has a positive size, because the direction is stored apart from the quantity.

### syntax

```
strategy.closedtrades_size(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the closed trade. Trades are numbered from 0 in the order they were closed.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.closedtrades_size Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.closedtrades > 0 ? strategy.closedtrades_size(strategy.closedtrades - 1) : na
plot(value, title="Size", color=color.blue)
```

### id

function:strategy.closedtrades_size

## strategy.commission_cash_per_contract (constant)

A commission type for the `commission_type` argument of `strategy()`: `commission_value` is an amount, in the account currency, charged per contract traded.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.commission_cash_per_contract Example", overlay=true, initial_capital=10000, commission_type=strategy.commission_cash_per_contract, commission_value=0.5)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
```

### id

constant:strategy.commission_cash_per_contract

## strategy.commission_cash_per_order (constant)

A commission type for the `commission_type` argument of `strategy()`: `commission_value` is a fixed amount, in the account currency, charged for each trade opened and for each trade closed. An order that closes several open trades, or part of one, is charged once for each trade it closes.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.commission_cash_per_order Example", overlay=true, initial_capital=10000, commission_type=strategy.commission_cash_per_order, commission_value=2)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
```

### id

constant:strategy.commission_cash_per_order

## strategy.commission_percent (constant)

A commission type for the `commission_type` argument of `strategy()`: `commission_value` is a percentage of each order's value.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.commission_percent Example", overlay=true, initial_capital=10000, commission_type=strategy.commission_percent, commission_value=0.1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
```

### id

constant:strategy.commission_percent

## strategy.entry (function)

Opens a position, or adds to one, in `direction` (`strategy.long` or `strategy.short`). An entry in the opposite direction to the current position first closes that position, then reverses it.

`id` names the entry so that `strategy.close` and `strategy.exit` can refer to it. Without `limit` or `stop` it is a market order; with `limit` or `stop` it waits for that price. `qty` overrides the default quantity set in `strategy()`.

### syntax

```
strategy.entry(series string id, series string direction, series float qty, series float limit, series float stop, series string oca_name, series string oca_type, series string comment) → void
```

### args

- `id`: series string
  Name of the entry. `strategy.close` and `strategy.exit` refer to the entry by this name.
  types: series string, simple string, input string, const string, literal string
- `direction`: series string
  The direction of the entry: `strategy.long` or `strategy.short`.
  types: series string, simple string, input string, const string, literal string
  values: strategy.long, strategy.short
- `qty?`: series float
  The quantity of the order. It overrides the default quantity set in `strategy()`. A `qty` of zero or less, or `na`, is ignored and the default quantity is used. With `default_qty_type` set to "cash" or "percent_of_equity", a market order has no price and stops the script with the error "Invalid order quantity"; give the order a `limit` or `stop`, or a `qty` above zero.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `limit?`: series float
  The limit price of the order. The order waits for that price.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `stop?`: series float
  The stop price of the order. The order waits for that price.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `oca_name?`: series string
  Name of the one-cancels-all group the order belongs to.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `oca_type?`: series string
  The one-cancels-all type: `strategy.oca_none`, `strategy.oca_cancel` or `strategy.oca_reduce`.
  types: series string, simple string, input string, const string, literal string
  values: strategy.oca_cancel, strategy.oca_none, strategy.oca_reduce
  default: strategy.oca_none
- `comment?`: series string
  Comment of the entry order.
  types: series string, simple string, input string, const string, literal string
  default: ""

### returnedType

void

### example

```lipi
//@lipi=2
strategy("strategy.entry Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.entry("Short", strategy.short)
}
```

### id

function:strategy.entry

## strategy.equity (variable)

The strategy's current equity: initial capital plus net profit plus open profit.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.equity Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.equity, title="Equity", color=color.blue)
```

### id

variable:strategy.equity

## strategy.exit (function)

Places exit orders for an open position: a take-profit, a stop-loss, or both. `from_entry` names the entry to exit; leave it out to exit all entries.

Prices can be given as levels (`limit` for the take-profit, `stop` for the stop-loss) or as distances in ticks from the entry price (`profit` and `loss`). When both kinds are given for the same side, the one that would fill first is used.

### syntax

```
strategy.exit(series string id, series string from_entry, series float qty, series float profit, series float limit, series float loss, series float stop, series string oca_name, series string comment) → void
```

### args

- `id`: series string
  Name of the exit order.
  types: series string, simple string, input string, const string, literal string
- `from_entry?`: series string
  Name of the entry to exit. If left out, all entries are exited.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `qty?`: series float
  The quantity to exit. Left out, the whole open quantity of `from_entry` (or of the position) is exited. With `default_qty_type` set to "cash" or "percent_of_equity", leaving it out stops the script with the error "Invalid order quantity": pass `qty`. A `qty` of zero or less stops the script with the same error.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `profit?`: series float
  The take-profit as a distance in ticks from the entry price. A tick is `syminfo.minmove`.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `limit?`: series float
  The take-profit as a price level.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `loss?`: series float
  The stop-loss as a distance in ticks from the entry price. A tick is `syminfo.minmove`.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `stop?`: series float
  The stop-loss as a price level.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `oca_name?`: series string
  Name of the one-cancels-all group the order belongs to.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `comment?`: series string
  Comment of the exit order.
  types: series string, simple string, input string, const string, literal string
  default: ""

### returnedType

void

### example

```lipi
//@lipi=2
strategy("strategy.exit Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
// Take profit 2% above and stop 1% below the average entry price
if strategy.position_size > 0 {
    strategy.exit("Exit Long", from_entry="Long", limit=strategy.position_avg_price * 1.02, stop=strategy.position_avg_price * 0.99)
}
```

### id

function:strategy.exit

## strategy.fixed (constant)

A position-size type for the `default_qty_type` argument of `strategy()`: `default_qty_value` is a fixed number of contracts, shares or units per order.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.fixed Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=10)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
```

### id

constant:strategy.fixed

## strategy.grossloss (variable)

The total of the profits of all closed trades that did not make a profit, so it is zero or negative: a trade that lost 10 adds -10.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.grossloss Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.grossloss, title="Grossloss", color=color.blue)
```

### id

variable:strategy.grossloss

## strategy.grossprofit (variable)

The total profit of all winning closed trades.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.grossprofit Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.grossprofit, title="Grossprofit", color=color.blue)
```

### id

variable:strategy.grossprofit

## strategy.initial_capital (variable)

The initial capital set in `strategy()`.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.initial_capital Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.initial_capital, title="Initial Capital", color=color.blue)
```

### id

variable:strategy.initial_capital

## strategy.long (constant)

The long direction, for the `direction` argument of `strategy.entry` and `strategy.order`: buy to open or add to a long position.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.long Example", overlay=true, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
```

### id

constant:strategy.long

## strategy.losstrades (variable)

The number of closed trades whose profit is zero or negative: a trade that closes at break-even counts here, so `strategy.wintrades` plus `strategy.losstrades` equals `strategy.closedtrades`.

### type

series int

### example

```lipi
//@lipi=2
strategy("strategy.losstrades Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.losstrades, title="Losstrades", color=color.blue)
```

### id

variable:strategy.losstrades

## strategy.max_drawdown (variable)

The largest peak-to-trough fall in equity so far.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.max_drawdown Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.max_drawdown, title="Max Drawdown", color=color.blue)
```

### id

variable:strategy.max_drawdown

## strategy.max_runup (variable)

The largest trough-to-peak rise in equity so far.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.max_runup Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.max_runup, title="Max Runup", color=color.blue)
```

### id

variable:strategy.max_runup

## strategy.netprofit (variable)

The total profit of all closed trades, net of commission; a loss is negative. In this build the commission of an entry is deducted when the trade opens, so the value falls at the entry, before the trade closes; the commission of the exit is deducted when it closes.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.netprofit Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.netprofit, title="Netprofit", color=color.blue)
```

### id

variable:strategy.netprofit

## strategy.oca_cancel (constant)

A one-cancels-all type, for the `oca_type` argument of `strategy.entry` and `strategy.order`. When one order of the group fills, the other orders of the same group are cancelled.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.oca_cancel Example", overlay=true, initial_capital=10000)
// Two breakout entries in one group: the first to fill decides
if strategy.position_size == 0 {
    strategy.entry("Up", strategy.long, stop=high + syminfo.mintick, oca_name="Breakout", oca_type=strategy.oca_cancel)
    strategy.entry("Down", strategy.short, stop=low - syminfo.mintick, oca_name="Breakout", oca_type=strategy.oca_cancel)
}
```

### id

constant:strategy.oca_cancel

## strategy.oca_none (constant)

A one-cancels-all type, for the `oca_type` argument of `strategy.entry` and `strategy.order`. The order is not part of a one-cancels-all group; it is filled independently of other orders.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.oca_none Example", overlay=true, initial_capital=10000)
// Two breakout entries in one group: the first to fill decides
if strategy.position_size == 0 {
    strategy.entry("Up", strategy.long, stop=high + syminfo.mintick, oca_name="Breakout", oca_type=strategy.oca_none)
    strategy.entry("Down", strategy.short, stop=low - syminfo.mintick, oca_name="Breakout", oca_type=strategy.oca_none)
}
```

### id

constant:strategy.oca_none

## strategy.oca_reduce (constant)

A one-cancels-all type, for the `oca_type` argument of `strategy.entry` and `strategy.order`. When one order of the group fills, the quantity of the other orders of the same group is reduced by the filled quantity.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.oca_reduce Example", overlay=true, initial_capital=10000)
// Two breakout entries in one group: the first to fill decides
if strategy.position_size == 0 {
    strategy.entry("Up", strategy.long, stop=high + syminfo.mintick, oca_name="Breakout", oca_type=strategy.oca_reduce)
    strategy.entry("Down", strategy.short, stop=low - syminfo.mintick, oca_name="Breakout", oca_type=strategy.oca_reduce)
}
```

### id

constant:strategy.oca_reduce

## strategy.openprofit (variable)

The current, unrealised profit of the open position; a loss is negative.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.openprofit Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.openprofit, title="Openprofit", color=color.blue)
```

### id

variable:strategy.openprofit

## strategy.opentrades (variable)

The number of trades open now (entries not yet closed).

### type

series int

### example

```lipi
//@lipi=2
strategy("strategy.opentrades Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.opentrades, title="Opentrades", color=color.blue)
```

### id

variable:strategy.opentrades

## strategy.opentrades_entry_bar_index (function)

For the open trade number `trade_num`, returns the bar index of the bar on which the entry order was placed (where `strategy.entry` or `strategy.order` ran), not the bar on which it filled; the two differ when the order fills on a later bar.

Trades are numbered from 0 in the order they were opened, so the most recent is `strategy.opentrades - 1`.

### syntax

```
strategy.opentrades_entry_bar_index(series int trade_num) → series int
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_entry_bar_index Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.opentrades > 0 ? strategy.opentrades_entry_bar_index(strategy.opentrades - 1) : na
plot(value, title="Entry Bar Index", color=color.blue)
```

### id

function:strategy.opentrades_entry_bar_index

## strategy.opentrades_entry_comment (function)

For the open trade number `trade_num`, returns the comment of the entry order that opened the trade.

Trades are numbered from 0 in the order they were opened, so the most recent is `strategy.opentrades - 1`.

### syntax

```
strategy.opentrades_entry_comment(series int trade_num) → series string
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series string

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_entry_comment Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
if barstate.islast and strategy.opentrades > 0 {
    label.new(bar_index, high, text="Latest open trade: " + strategy.opentrades_entry_comment(strategy.opentrades - 1))
}
```

### id

function:strategy.opentrades_entry_comment

## strategy.opentrades_entry_id (function)

For the open trade number `trade_num`, returns the `id` of the entry order that opened the trade.

Trades are numbered from 0 in the order they were opened, so the most recent is `strategy.opentrades - 1`.

### syntax

```
strategy.opentrades_entry_id(series int trade_num) → series string
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series string

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_entry_id Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
if barstate.islast and strategy.opentrades > 0 {
    label.new(bar_index, high, text="Latest open trade: " + strategy.opentrades_entry_id(strategy.opentrades - 1))
}
```

### id

function:strategy.opentrades_entry_id

## strategy.opentrades_entry_price (function)

For the open trade number `trade_num`, returns the price at which the trade was entered.

Trades are numbered from 0 in the order they were opened, so the most recent is `strategy.opentrades - 1`.

### syntax

```
strategy.opentrades_entry_price(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_entry_price Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.opentrades > 0 ? strategy.opentrades_entry_price(strategy.opentrades - 1) : na
plot(value, title="Entry Price", color=color.blue)
```

### id

function:strategy.opentrades_entry_price

## strategy.opentrades_entry_time (function)

For the open trade number `trade_num`, returns the UNIX time, in milliseconds, at which the trade was entered.

Trades are numbered from 0 in the order they were opened, so the most recent is `strategy.opentrades - 1`.

### syntax

```
strategy.opentrades_entry_time(series int trade_num) → series int
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series int

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_entry_time Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.opentrades > 0 ? strategy.opentrades_entry_time(strategy.opentrades - 1) : na
plot(value, title="Entry Time", color=color.blue)
```

### id

function:strategy.opentrades_entry_time

## strategy.opentrades_max_drawdown (function)

For the open trade number `trade_num`, returns the largest fall of the trade's profit from its highest profit so far, in the account currency. The highest profit starts at 0, so for a trade that has never been in profit this is its largest loss.

Trades are numbered from 0 in the order they were opened, so the most recent is `strategy.opentrades - 1`.

### syntax

```
strategy.opentrades_max_drawdown(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_max_drawdown Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.opentrades > 0 ? strategy.opentrades_max_drawdown(strategy.opentrades - 1) : na
plot(value, title="Max Drawdown", color=color.blue)
```

### id

function:strategy.opentrades_max_drawdown

## strategy.opentrades_max_runup (function)

For the open trade number `trade_num`, returns the highest profit the trade has shown so far, in the account currency (0 until the trade is in profit).

Trades are numbered from 0 in the order they were opened, so the most recent is `strategy.opentrades - 1`.

### syntax

```
strategy.opentrades_max_runup(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_max_runup Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.opentrades > 0 ? strategy.opentrades_max_runup(strategy.opentrades - 1) : na
plot(value, title="Max Runup", color=color.blue)
```

### id

function:strategy.opentrades_max_runup

## strategy.opentrades_profit (function)

For the open trade number `trade_num`, returns the current, unrealised profit of the trade, in the account currency; a loss is negative.

Trades are numbered from 0 in the order they were opened, so the most recent is `strategy.opentrades - 1`.

### syntax

```
strategy.opentrades_profit(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_profit Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.opentrades > 0 ? strategy.opentrades_profit(strategy.opentrades - 1) : na
plot(value, title="Profit", color=color.blue)
```

### id

function:strategy.opentrades_profit

## strategy.opentrades_size (function)

For the open trade number `trade_num`, returns the size of the trade. The size is never negative: a short trade has a positive size, because the direction is stored apart from the quantity.

### syntax

```
strategy.opentrades_size(series int trade_num) → series float
```

### args

- `trade_num`: series int
  Number of the open trade. Trades are numbered from 0 in the order they were opened.
  types: series int, simple int, input int, const int, literal int

### returnedType

series float

### example

```lipi
//@lipi=2
strategy("strategy.opentrades_size Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
value = strategy.opentrades > 0 ? strategy.opentrades_size(strategy.opentrades - 1) : na
plot(value, title="Size", color=color.blue)
```

### id

function:strategy.opentrades_size

## strategy.order (function)

Places an order without any position logic: a buy adds to the position and a sell subtracts from it, whatever the current position is. Unlike `strategy.entry`, it does not reverse a position automatically and it is not limited by `pyramiding`.

### syntax

```
strategy.order(series string id, series string direction, series float qty, series float limit, series float stop, series string oca_name, series string oca_type, series string comment) → void
```

### args

- `id`: series string
  Name of the order.
  types: series string, simple string, input string, const string, literal string
- `direction`: series string
  The direction of the order: `strategy.long` (a buy) or `strategy.short` (a sell).
  types: series string, simple string, input string, const string, literal string
  values: strategy.long, strategy.short
- `qty?`: series float
  The quantity of the order. A `qty` of zero or less, or `na`, is ignored and the default quantity is used. With `default_qty_type` set to "cash" or "percent_of_equity" and no `qty` above zero, a market order has no price and stops the script with the error "Invalid order quantity"; give the order a `limit` or `stop`, or a `qty` above zero.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `limit?`: series float
  The limit price of the order. The order waits for that price.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `stop?`: series float
  The stop price of the order. The order waits for that price.
  types: series float, series int, simple int, input int, const int, literal int, simple float, input float, const float, literal float
  default: na
- `oca_name?`: series string
  Name of the one-cancels-all group the order belongs to.
  types: series string, simple string, input string, const string, literal string
  default: ""
- `oca_type?`: series string
  The one-cancels-all type: `strategy.oca_none`, `strategy.oca_cancel` or `strategy.oca_reduce`.
  types: series string, simple string, input string, const string, literal string
  values: strategy.oca_cancel, strategy.oca_none, strategy.oca_reduce
  default: strategy.oca_none
- `comment?`: series string
  Comment of the order.
  types: series string, simple string, input string, const string, literal string
  default: ""

### returnedType

void

### example

```lipi
//@lipi=2
strategy("strategy.order Example", overlay=true, initial_capital=10000, default_qty_type=strategy.fixed, default_qty_value=1)
// Buy one unit on every up bar, sell one on every down bar
if close > open {
    strategy.order("Buy", strategy.long, qty=1)
} else if close < open {
    strategy.order("Sell", strategy.short, qty=1)
}
```

### id

function:strategy.order

## strategy.position_avg_price (variable)

The average entry price of the current position. It is 0, not `na`, when the position is flat.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.position_avg_price Example", overlay=true, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.position_avg_price, title="Average Entry Price", color=color.orange, style=plotStyle.linebr)
```

### id

variable:strategy.position_avg_price

## strategy.position_size (variable)

The size of the current position: positive when long, negative when short, 0 when flat.

### type

series float

### example

```lipi
//@lipi=2
strategy("strategy.position_size Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.position_size, title="Position Size", color=color.blue)
```

### id

variable:strategy.position_size

## strategy.short (constant)

The short direction, for the `direction` argument of `strategy.entry` and `strategy.order`: sell to open or add to a short position.

### type

const string

### example

```lipi
//@lipi=2
strategy("strategy.short Example", overlay=true, initial_capital=10000)
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.entry("Short", strategy.short)
}
```

### id

constant:strategy.short

## strategy.wintrades (variable)

The number of closed trades that made a profit.

### type

series int

### example

```lipi
//@lipi=2
strategy("strategy.wintrades Example", overlay=false, initial_capital=10000)
if talib.crossover(close, talib.sma(close, 20)) {
    strategy.entry("Long", strategy.long)
}
if talib.crossunder(close, talib.sma(close, 20)) {
    strategy.close("Long")
}
plot(strategy.wintrades, title="Wintrades", color=color.blue)
```

### id

variable:strategy.wintrades
