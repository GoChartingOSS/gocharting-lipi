Contents: global · array · barstate · box · chart · chartPoint · color · dayofweek · extend · format · input · interval · label · line · linefill · math · order · orderflow · polyline · position · session · str · strategy · syminfo · ta · table · talib · text · xloc · yloc

Lipi 2 reference 2.7, generated 2026-10-25, compiler build df7b3b14

## global

operator ! — Logical NOT.
operator != — Not equal to.
operator % — Modulo: the remainder of dividing the left operand by the right one.
operator %= — Modulo assignment.
operator && — Logical AND.
operator * — Multiplication.
operator *= — Multiply assignment.
operator + — Addition.
operator += — Add assignment.
operator - — Subtraction or unary minus.
operator -= — Subtract assignment.
operator / — Division.
operator /= — Divide assignment.
operator := — Reassignment operator.
operator < — Less than.
operator <= — Less than or equal to.
operator = — for assignment.
operator == — Equal to.
operator > — Greater than.
operator >= — Greater than or equal to.
operator ? — Ternary conditional operator.
annotation @lipi= — Source annotation that selects which Lipi compiler stack runs the script.
alert(message: series string) → void — Raises an alert from inside your own logic, with a message you build.
alertcondition(condition: series bool, title?: const string, message?: const string) → void — Declares a condition the platform can offer to the reader.
keyword and — True when both of its operands are true.
variable bar_index: series int — The index of the bar being evaluated.
barcolor(color?: series color, title?: const string, offset?: input int, display?: input display) → void — Recolours the chart's own price bars.
bgcolor(color?: series color, title?: const string, offset?: input int, force_overlay?: const bool, display?: input display) → void — Shades the pane's background.
type bool — A true-or-false value.
bool(value: const bool) → const bool — Declares a value as a bool.
bool(value: input bool) → input bool — Declares a value as a bool.
bool(value: simple bool) → simple bool — Declares a value as a bool.
bool(value: series bool) → series bool — Declares a value as a bool.
box(value: series box) → series box — Converts `value` to the `box` type.
keyword break — Leaves the innermost `for` or `while` loop at once.
keyword case — Starts one block of a `switch`: `case <value>:` runs its block when the value of the `switch` equals `<value>`.
variable close: series float — The bar's closing price.
color(value: const color) → const color — Converts a value to a colour.
color(value: input color) → input color — Converts a value to a colour.
color(value: simple color) → simple color — Converts a value to a colour.
color(value: series color) → series color — Converts a value to a colour.
keyword const — A qualifier written before the type of a parameter of your own function.
keyword continue — Skips the rest of the current pass of the innermost `for` or `while` loop and starts the next pass.
variable dayofmonth: series int — The day of the month of the bar being evaluated.
dayofmonth(time: series int, timezone?: series string) → series int — The day of the month of a time you supply.
variable dayofweek: series int — The day of the week of the bar being evaluated, as an int series.
dayofweek(time: series int, timezone?: series string) → series int — The day of the week of a time you supply, as an int series.
keyword def — Declares a **type function** (method on a type): the **first parameter** is the receiver — its declared type is the type the method belongs to.
keyword default — Runs its block when no `case` of the `switch` matches.
type display — Controls where a plot or indicator output is visible in the UI (pane, price scale, status line, data window).
enum display — Controls where a plot or indicator output is visible in the UI (pane, price scale, status line, data window).
keyword else — Runs a block when the condition of the `if` before it is false.
keyword enum — Declares an enum of your own, as a braced block of members, one per line.
constant false: const bool — The bool value false.
fill(h1: series hline, h2: series hline, color?: series color, title?: const string, fillgaps?: const bool, display?: input display) → void — Shades the band between two plots, or between two horizontal lines.
fill(h1: series hline, h2: series hline, top_value: series float, bottom_value: series float, top_color: series color, bottom_color: series color, title?: const string, display?: input display, fillgaps?: const bool, editable?: input bool) → void — Shades the band between two plots, or between two horizontal lines.
fill(p1: series plot, p2: series plot, title?: const string, color?: series color, fillgaps?: const bool, display?: input display) → void — Shades the band between two plots, or between two horizontal lines.
fill(plot1: series plot, plot2: series plot, top_value: series float, bottom_value: series float, top_color: series color, bottom_color: series color, title?: const string, display?: input display, fillgaps?: const bool, editable?: input bool) → void — Shades the band between two plots, or between two horizontal lines.
fixnan(value: series int) → series int — Takes a series and hands back a series of the same type, with `na` values dealt with.
fixnan(value: series float) → series float — Takes a series and hands back a series of the same type, with `na` values dealt with.
fixnan(value: series bool) → series bool — Takes a series and hands back a series of the same type, with `na` values dealt with.
fixnan(value: series color) → series color — Takes a series and hands back a series of the same type, with `na` values dealt with.
type float — A number with a fractional part, written `1.5`.
float(value: const float) → const float — Converts a value to a float.
float(value: input float) → input float — Converts a value to a float.
float(value: simple float) → simple float — Converts a value to a float.
float(value: series float) → series float — Converts a value to a float.
type font — Font family constants for text drawn on boxes, labels, and table cells.
enum font — Font family constants for text drawn on boxes, labels, and table cells.
keyword for in — Loops over each element of an array.
keyword for to — Counts from a start value to an end value, using a counter variable.
keyword func — Declares an ordinary user function (not a type method).
variable high: series float — The bar's highest traded price.
variable hl2: series float — The bar's high and low, averaged: its midpoint.
variable hlc3: series float — The bar's high, low and close, averaged.
variable hlcc4: series float — The bar's high, low and close with the close counted twice, averaged.
type hline — The value `hline` gives back once it has drawn a horizontal level.
hline(price: input float, title?: const string, color?: input color, linewidth?: input int, style?: input hlineStyle, display?: input display, format?: input string) → series hline — Draws a horizontal line at a fixed price.
type hlineStyle — Three line styles for a horizontal level: `solid`, `dashed` and `dotted`.
enum hlineStyle — Three line styles for a horizontal level: `solid`, `dashed` and `dotted`.
variable hour: series int — The hour of the bar being evaluated.
hour(time: series int, timezone?: series string) → series int — The hour of a time you supply.
keyword if — Chooses which block of statements runs.
indicator(title: const string, shorttitle?: const string, overlay?: const bool, format?: const string, precision?: const int, scale?: const scale, calc_on_every_tick?: const bool, max_lines_count?: const int, max_labels_count?: const int, max_boxes_count?: const int, calc_bars_count?: const int, max_polylines_count?: const int, behind_chart?: const bool) → void — Declares the script and names it.
input(defval: const color, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input color — Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.
input(defval: const string, title?: const string, options?: [const string...], tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input string — Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.
input(defval: const int, title?: const string, options?: [const int...], tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input int — Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.
input(defval: const float, title?: const string, options?: [const float...], tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input float — Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.
input(defval: series float, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → series float — Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.
input(defval: const bool, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input bool — Declares a setting the reader can change from the chart, picking its kind from the type of the default value you hand it.
type int — A whole number.
int(value: const float) → const int — Converts a value to an `int`.
int(value: input float) → input int — Converts a value to an `int`.
int(value: simple float) → simple int — Converts a value to an `int`.
int(value: series float) → series int — Converts a value to an `int`.
keyword intra — The second of the two persistence keywords the grammar accepts, and the only other one.
label(value: series label) → series label — Converts `value` to the `label` type.
variable last_bar_index: series int — Bar index of the last bar on the chart (the rightmost bar), including the realtime tip when one is forming.
variable last_bar_time: series int — Open time of the last bar on the chart, in UNIX milliseconds (same convention as `time`).
line(value: series line) → series line — Converts `value` to the `line` type.
linefill(value: series linefill) → series linefill — Converts `value` to the `linefill` type.
type location — Five places a marker can sit: `abovebar`, `belowbar`, `top`, `bottom` and `absolute`.
enum location — Five places a marker can sit: `abovebar`, `belowbar`, `top`, `bottom` and `absolute`.
variable low: series float — The bar's lowest traded price.
variable minute: series int — The minute of the bar being evaluated.
minute(time: series int, timezone?: series string) → series int — The minute of a time you supply.
variable month: series int — The month of the bar being evaluated.
month(time: series int, timezone?: series string) → series int — The month of a time you supply.
constant na: const na — Stands for a missing value.
na(value: series <any_type>) → series bool — Tests whether a value is absent.
keyword not — Negates the expression that follows it.
nz(value: series int, alt?: series int) → series int — Takes a value and an alternative of the same type, and stands in for the value where it is absent.
nz(value: series float, alt?: series float) → series float — Takes a value and an alternative of the same type, and stands in for the value where it is absent.
nz(value: series string, alt?: series string) → series string — Takes a value and an alternative of the same type, and stands in for the value where it is absent.
nz(value: series bool, alt?: series bool) → series bool — Takes a value and an alternative of the same type, and stands in for the value where it is absent.
nz(value: series color, alt?: series color) → series color — Takes a value and an alternative of the same type, and stands in for the value where it is absent.
variable ohlc4: series float — The bar's four values, open, high, low and close, averaged with equal weight.
variable oi: series float — Open interest for the bar.
variable open: series float — The opening price of the bar your script is being evaluated on.
keyword or — True when either of its operands is true.
type plot — The value `plot` gives back once it has drawn a series.
plot(series: series float, title?: const string, color?: series color, linewidth?: input int, style?: input plotStyle, trackprice?: input bool, histbase?: input float, offset?: input int, force_overlay?: const bool, display?: input display, format?: input string) → series plot — Draws a series on the chart, one point per bar.
type plotStyle — The fourteen ways `plot` can draw a series: `line`, `linebr`, `area`, `areabr`, `smoothedArea`, `stepLine`, `stepLinebr`, `stepArea`, `stepAreabr`, `bar`, `histogram`, `scatter`, `triangular` and `cross`.
enum plotStyle — The fourteen ways `plot` can draw a series: `line`, `linebr`, `area`, `areabr`, `smoothedArea`, `stepLine`, `stepLinebr`, `stepArea`, `stepAreabr`, `bar`, `histogram`, `scatter`, `triangular` and `cross`.
plotarrow(series: series float, title?: const string, colorup?: series color, colordown?: series color, offset?: input int, minheight?: input int, maxheight?: input int, force_overlay?: const bool, display?: input display, format?: input string) → void — Draws an arrow on each bar, sized from a number you supply.
plotbar(open: series float, high: series float, low: series float, close: series float, title?: const string, color?: series color, display?: input display, force_overlay?: const bool) → void — Draws bars from the same four required series that `plotcandle` takes.
plotcandle(open: series float, high: series float, low: series float, close: series float, title?: const string, color?: series color, wickcolor?: series color, bordercolor?: series color, force_overlay?: const bool, display?: input display) → void — Draws candles from four series of your own rather than from the chart's bars.
plotchar(series: series float, title?: const string, char?: const string, location?: input location, color?: series color, offset?: input int, text?: const string, textcolor?: series color, size?: input size, force_overlay?: const bool, display?: input display, format?: input string) → void — The same marker as `plotshape`, with one character in place of a shape from the fixed set.
plotchar(series: series bool, title?: const string, char?: const string, location?: input location, color?: series color, offset?: input int, text?: const string, textcolor?: series color, size?: input size, force_overlay?: const bool, display?: input display, format?: input string) → void — The same marker as `plotshape`, with one character in place of a shape from the fixed set.
plotshape(series: series bool, title?: const string, shape?: input shape, location?: input location, color?: series color, offset?: input int, text?: const string, textcolor?: series color, size?: input size, force_overlay?: const bool, display?: input display, format?: input string) → void — Marks the bars on which a condition holds, using a shape from a fixed set.
plotshape(series: series float, title?: const string, shape?: input shape, location?: input location, color?: series color, offset?: input int, text?: const string, textcolor?: series color, size?: input size, force_overlay?: const bool, display?: input display, format?: input string) → void — Marks the bars on which a condition holds, using a shape from a fixed set.
polyline(value: series polyline) → series polyline — Converts `value` to the `polyline` type.
keyword return — Hands a value back from a braced function body.
type scale — Price-scale placement for scripts declared with `indicator()` or `strategy()`.
enum scale — Price-scale placement for scripts declared with `indicator()` or `strategy()`.
variable second: series int — The second of the bar being evaluated.
second(time: series int, timezone?: series string) → series int — The second of a time you supply.
keyword series — A qualifier written before the type of a parameter of your own function.
type shape — The twelve markers `plotshape` can draw: `xcross`, `cross`, `triangleup`, `triangledown`, `flag`, `circle`, `arrowup`, `arrowdown`, `labelup`, `labeldown`, `square` and `diamond`.
enum shape — The twelve markers `plotshape` can draw: `xcross`, `cross`, `triangleup`, `triangledown`, `flag`, `circle`, `arrowup`, `arrowdown`, `labelup`, `labeldown`, `square` and `diamond`.
keyword simple — A qualifier written before the type of a parameter of your own function.
type size — Six sizes for a marker: `auto`, `tiny`, `small`, `normal`, `large` and `huge`.
enum size — Six sizes for a marker: `auto`, `tiny`, `small`, `normal`, `large` and `huge`.
keyword static — Declares a value that survives from one bar to the next.
keyword step — The optional increment of a counted `for` loop: `for i = 0 to 10 step 2`.
strategy(title: const string, shorttitle?: const string, overlay?: const bool, format?: const string, precision?: const int, scale?: const scale, pyramiding?: const int, calc_on_order_fills?: const bool, calc_on_every_tick?: const bool, default_qty_type?: const string, default_qty_value?: const float, initial_capital?: const float, commission_type?: const string, commission_value?: const float, process_orders_on_close?: const bool, max_lines_count?: const int, max_labels_count?: const int, max_boxes_count?: const int, max_polylines_count?: const int, behind_chart?: const bool) → void — Declares the script as a strategy: a script that places simulated orders and reports their performance.
type string — A piece of text, written between double quotes: `"length"`.
string(value: const string) → const string — Converts a value to a string.
string(value: input string) → input string — Converts a value to a string.
string(value: simple string) → simple string — Converts a value to a string.
string(value: series string) → series string — Converts a value to a string.
keyword switch — Chooses one block by the value of an expression.
table(value: series table) → series table — Converts `value` to the `table` type.
variable time: series int — The bar's opening time, as an int series.
time(interval?: series string, session?: series string, bars_back?: series int, interval_bars_back?: series int) → series int — Returns the opening time of the current bar in UNIX milliseconds, measured on `interval` rather than on the chart's own bars.
time(interval?: series string, session?: series string, timezone?: series string, bars_back?: series int, interval_bars_back?: series int) → series int — Returns the opening time of the current bar in UNIX milliseconds, measured on `interval` rather than on the chart's own bars.
variable time_close: series int — The bar's closing time, distinct from `time`.
time_close(interval?: series string, session?: series string, bars_back?: series int, interval_bars_back?: series int) → series int — Returns the closing time of the current bar in UNIX milliseconds, measured on `interval`.
time_close(interval?: series string, session?: series string, timezone?: series string, bars_back?: series int, interval_bars_back?: series int) → series int — Returns the closing time of the current bar in UNIX milliseconds, measured on `interval`.
variable time_sessionday: series int — The UNIX time, in milliseconds, of the trading day the current bar belongs to.
variable timenow: series int — The current time, rather than a time taken from the bar.
timestamp(dateString: const string) → const int — Assembles a time from its parts - the other direction from the eight functions that take a time apart.
timestamp(dateString: series string) → series int — Assembles a time from its parts - the other direction from the eight functions that take a time apart.
timestamp(year: simple int, month: simple int, day: simple int, hour?: simple int, minute?: simple int, second?: simple int) → simple int — Assembles a time from its parts - the other direction from the eight functions that take a time apart.
timestamp(year: series int, month: series int, day: series int, hour?: series int, minute?: series int, second?: series int) → series int — Assembles a time from its parts - the other direction from the eight functions that take a time apart.
timestamp(timezone?: simple string, year: simple int, month: simple int, day: simple int, hour?: simple int, minute?: simple int, second?: simple int) → simple int — Assembles a time from its parts - the other direction from the eight functions that take a time apart.
timestamp(timezone?: series string, year: series int, month: series int, day: series int, hour?: series int, minute?: series int, second?: series int) → series int — Assembles a time from its parts - the other direction from the eight functions that take a time apart.
constant true: const bool — The bool value true.
keyword type — Declares an object type of your own: a name, then a braced block with one typed field per line.
variable volume: series float — The volume traded in the bar.
weekofyear(time: series int, timezone?: series string) → series int — The week of the year of a time you supply.
keyword while — Repeats a block for as long as a condition holds.
variable year: series int — The year of the bar being evaluated.
year(time: series int, timezone?: series string) → series int — The year of a time you supply.
operator || — It evaluates two Boolean expressions and returns true if at least one of them is true.

## array

library array — Functions for creating and working with arrays: ordered, resizable lists of values of one type.
type array — An ordered, resizable list of values of one type, written `array<type>`, as in `array<float>`.
array.abs(id: series array) → series array — Returns a new array holding the absolute value of each element.
array.avg(id: series array) → series float — Returns the mean of the array's elements.
array.binary_search(id: series array, value: series <type of the array's elements>) → series int — Searches an array sorted in ascending order for `value` and returns its index, or -1 when it is not there.
array.binary_search_leftmost(id: series array, value: series <type of the array's elements>) → series int — Searches an array sorted in ascending order.
array.binary_search_rightmost(id: series array, value: series <type of the array's elements>) → series int — Searches an array sorted in ascending order.
array.clear(id: series array) → void — Removes every element, leaving an empty array.
array.concat(id1: series array, id2: series array) → series array — Appends the elements of `id2` to the end of `id1` and returns `id1`.
array.copy(id: series array) → series array — Returns a new array with the same elements.
array.covariance(id1: series array, id2: series array, biased?: series bool) → series float — Returns the covariance of two arrays of the same size.
array.every(id: series array) → series bool — Returns true when every element is true.
array.fill(id: series array, value: series <type of the array's elements>, index_from?: series int, index_to?: series int) → void — Sets elements of the array to `value`.
array.first(id: series array) → series <type of the array's elements> — Returns the first element of the array.
array.from(arg0, arg1, ...: series int) → series array<int> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series float) → series array<float> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series bool) → series array<bool> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series string) → series array<string> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series color) → series array<color> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series label) → series array<label> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series line) → series array<line> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series box) → series array<box> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series linefill) → series array<linefill> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series polyline) → series array<polyline> — Creates an array from the values passed to it, in order.
array.from(arg0, arg1, ...: series table) → series array<table> — Creates an array from the values passed to it, in order.
array.get(id: series array, index: series int) → series <type of the array's elements> — Returns the element at `index`.
array.includes(id: series array, value: series <type of the array's elements>) → series bool — Returns true when `value` is one of the array's elements.
array.indexof(id: series array, value: series <type of the array's elements>) → series int — Returns the index of the first element equal to `value`, or -1 when no element matches.
array.insert(id: series array, index: series int, value: series <type of the array's elements>) → void — Inserts `value` at `index`, moving the element that was there, and every element after it, up one index.
array.join(id: series array, separator?: series string) → series string — Joins the elements into one string, with `separator` between them.
array.last(id: series array) → series <type of the array's elements> — Returns the last element of the array.
array.lastindexof(id: series array, value: series <type of the array's elements>) → series int — Returns the index of the last element equal to `value`, or -1 when no element matches.
array.length(id: series array) → series int — Returns the number of elements in the array.
array.max(id: series array, nth?: series int) → series <type of the array's elements> — Returns the largest element.
array.median(id: series array) → series float — Returns the median of the array's elements: the middle value once they are sorted, or the mean of the two middle values when the count is even.
array.min(id: series array, nth?: series int) → series <type of the array's elements> — Returns the smallest element.
array.mode(id: series array) → series <type of the array's elements> — Returns the most frequent element.
array.new(length?: series int, initial_value?: series <type of the array's elements>) → series array — Creates an array of the given length.
array.new_bool(size?: series int, initial_value?: series bool) → series array<bool> — Creates an array of `bool` elements with `size` elements, each set to `initial_value`.
array.new_box(size?: series int, initial_value?: series box) → series array<box> — Creates an array of `box` IDs with `size` elements, each set to `initial_value`.
array.new_color(size?: series int, initial_value?: series color) → series array<color> — Creates an array of `color` elements with `size` elements, each set to `initial_value`.
array.new_float(size?: series int, initial_value?: series float) → series array<float> — Creates an array of `float` elements with `size` elements, each set to `initial_value`.
array.new_int(size?: series int, initial_value?: series int) → series array<int> — Creates an array of `int` elements with `size` elements, each set to `initial_value`.
array.new_label(size?: series int, initial_value?: series label) → series array<label> — Creates an array of `label` IDs with `size` elements, each set to `initial_value`.
array.new_line(size?: series int, initial_value?: series line) → series array<line> — Creates an array of `line` IDs with `size` elements, each set to `initial_value`.
array.new_linefill(size?: series int, initial_value?: series linefill) → series array<linefill> — Creates an array of `linefill` IDs with `size` elements, each set to `initial_value`.
array.new_string(size?: series int, initial_value?: series string) → series array<string> — Creates an array of `string` elements with `size` elements, each set to `initial_value`.
array.new_table(size?: series int, initial_value?: series table) → series array<table> — Creates an array of `table` IDs with `size` elements, each set to `initial_value`.
array.percentile_linear_interpolation(id: series array, percentage: series float) → series float — Returns the value below which `percentage` percent of the elements fall, interpolating between the two nearest elements.
array.percentile_nearest_rank(id: series array, percentage: series float) → series <type of the array's elements> — Returns the value below which `percentage` percent of the elements fall, using the nearest element rather than interpolating.
array.percentrank(id: series array, index: series int) → series float — Returns the percentile rank of the element at `index`: the percentage of elements that are less than or equal to it.
array.pop(id: series array) → series <type of the array's elements> — Removes the last element of the array and returns it.
array.push(id: series array, value: series <type of the array's elements>) → void — Appends `value` to the end of the array, growing it by one element.
array.range(id: series array) → series <type of the array's elements> — Returns the difference between the largest and the smallest element.
array.remove(id: series array, index: series int) → void — Removes the element at `index`.
array.removeAll(id: series array) → void — Removes all elements from the array, leaving it empty.
array.reverse(id: series array) → void — Reverses the order of the elements, in place.
array.set(id: series array, index: series int, value: series <type of the array's elements>) → void — Replaces the element at `index` with `value`.
array.shift(id: series array) → series <type of the array's elements> — Removes the first element of the array and returns it.
array.slice(id: series array, index_from?: series int, index_to?: series int) → series array — Returns the part of the array from `index_from` up to, but not including, `index_to`.
array.some(id: series array) → series bool — Returns true when at least one element is true.
array.sort(id: series array, order?: series string) → void — Sorts the array in place.
array.sort_indices(id: series array, order?: series string) → series array<int> — Returns an int array of indexes that would sort the array, leaving the array itself unchanged.
array.standardize(id: series array) → series array<float> — Returns a new array of z-scores: each element minus the mean, divided by the standard deviation.
array.stdev(id: series array, biased?: series bool) → series float — Returns the standard deviation of the array's elements.
array.sum(id: series array) → series <type of the array's elements> — Returns the sum of the array's elements.
array.unshift(id: series array, value: series <type of the array's elements>) → void — Inserts `value` at the beginning of the array.
array.variance(id: series array, biased?: series bool) → series float — Returns the variance of the array's elements.

## barstate

library barstate — Seven boolean series that tell your script which kind of bar it is being evaluated on: the first, a new one, a historical one, the last, the last confirmed historical one, one that is still updating, and one that is confirmed.
variable barstate.isconfirmed: series bool — Returns true if the current bar is confirmed (closed).
variable barstate.isfirst: series bool — Your script is being evaluated on the first bar of the chart.
variable barstate.ishistory: series bool — Tells your script whether the bar it is being evaluated on is a historical bar.
variable barstate.islast: series bool — The bar your script is on is the last bar of the chart.
variable barstate.islastconfirmedhistory: series bool — This marks the last confirmed historical bar of the chart, when the market is closed.
variable barstate.isnew: series bool — The bar being evaluated is a new bar.
variable barstate.isrealtime: series bool — The bar under evaluation is a live bar: this is true on every run of that bar, including the run when the bar closes, and false on historical bars.

## box

library box — Functions for creating and mutating rectangular box drawings on the chart.
type box — A rectangular drawing on the chart, defined by two corners.
variable box.all: series array<box> — Array of all currently existing box drawings, from oldest to newest.
box.all() → series array<box> — Returns the array of all existing box objects (same as box.all).
box.copy(id: series box) → series box — Creates a copy of a box.
box.delete(id: series box) → void — Deletes a box.
box.get_bottom(id: series box) → series float — Returns the bottom price of a box.
box.get_left(id: series box) → series int — Returns the left x-coordinate of a box.
box.get_right(id: series box) → series int — Returns the right x-coordinate of a box.
box.get_top(id: series box) → series float — Returns the top price of a box.
box.new(left: series int, top: series float, right: series int, bottom: series float, border_color?: series color, border_width?: series int, border_style?: series string, extend?: series string, xloc?: series string, bgcolor?: series color, text?: series string, size?: series size, textcolor?: series color, texthalign?: series string, textvalign?: series string, textwrap?: series string, text_font_family?: input font, force_overlay?: const bool, text_formatting?: series string) → series box — Creates a box from left/top/right/bottom coordinates, or from two chartPoint corners.
box.new(top_left: series chartPoint, bottom_right: series chartPoint, border_color?: series color, border_width?: series int, border_style?: series string, extend?: series string, xloc?: series string, bgcolor?: series color, text?: series string, size?: series size, textcolor?: series color, texthalign?: series string, textvalign?: series string, textwrap?: series string, text_font_family?: input font, force_overlay?: const bool, text_formatting?: series string) → series box — Creates a box from left/top/right/bottom coordinates, or from two chartPoint corners.
box.set_bgcolor(id: series box, color: series color) → void — Sets a box's background color.
box.set_border_color(id: series box, color: series color) → void — Sets a box's border color.
box.set_border_style(id: series box, style: series string) → void — Sets a box's border style.
box.set_border_width(id: series box, width: series int) → void — Sets a box's border width in pixels.
box.set_bottom(id: series box, bottom: series float) → void — Sets a box's bottom price.
box.set_bottom_right_point(id: series box, point: series chartPoint) → void — Sets a box's bottom-right corner from a chartPoint.
box.set_extend(id: series box, extend: series string) → void — Sets whether a box extends past its corners.
box.set_left(id: series box, left: series int) → void — Sets a box's left x-coordinate.
box.set_lefttop(id: series box, left: series int, top: series float) → void — Sets a box's left x-coordinate and top price.
box.set_right(id: series box, right: series int) → void — Sets a box's right x-coordinate.
box.set_rightbottom(id: series box, right: series int, bottom: series float) → void — Sets a box's right x-coordinate and bottom price.
box.set_text(id: series box, text: series string) → void — Sets a box's text.
box.set_text_color(id: series box, color: series color) → void — Sets a box's text color.
box.set_text_font_family(id: series box, family: input font) → void — Sets a box's text font family.
box.set_text_formatting(id: series box, formatting: series string) → void — Sets a box's text formatting.
box.set_text_halign(id: series box, align: series string) → void — Sets a box's horizontal text alignment.
box.set_text_size(id: series box, size: series size) → void — Sets a box's text size.
box.set_text_valign(id: series box, align: series string) → void — Sets a box's vertical text alignment.
box.set_text_wrap(id: series box, wrap: series string) → void — Sets whether a box's text wraps.
box.set_top(id: series box, top: series float) → void — Sets a box's top price.
box.set_top_left_point(id: series box, point: series chartPoint) → void — Sets a box's top-left corner from a chartPoint.
box.set_xloc(id: series box, left: series int, right: series int, xloc: series string) → void — Sets whether a box's x-coordinates are bar indexes or times.

## chart

library chart — Values that describe the chart the script is drawn on: its colours (`chart.bg_color` and `chart.fg_color`) and its type (`chart.is_standard`, `chart.is_heikinashi`, `chart.is_renko` and the other `chart.is_*` values).
variable chart.bg_color: input color — The background colour of the chart the script is drawn on, as set by the reader.
variable chart.fg_color: input color — A foreground colour that contrasts with the chart's background, for text and lines that must stay readable on both light and dark charts.
variable chart.is_heikinashi: simple bool — True when the chart type is Heikin Ashi.
variable chart.is_kagi: simple bool — True when the chart type is Kagi.
variable chart.is_linebreak: simple bool — True when the chart type is Line Break.
variable chart.is_pnf: simple bool — True when the chart type is Point & Figure.
variable chart.is_range: simple bool — True when the chart type is Range.
variable chart.is_renko: simple bool — True when the chart type is Renko.
variable chart.is_standard: simple bool — True when the chart type is a standard chart type (candles, bars, line or area).

## chartPoint

library chartPoint — Five functions that build a chart point — `new`, `from_time`, `from_index`, `now` and `copy` — for the type of the same name, whose three fields are a time, an index and a price.
type chartPoint — A single position on the chart, described by three fields: time carries when, index carries which bar, and price carries where on the price scale.
chartPoint.copy(id: series chartPoint) → series chartPoint — Hands back a copy of a chart point.
chartPoint.from_index(index: series int, price: series float) → series chartPoint — Builds a chart point from a bar index and a price.
chartPoint.from_time(time: series int, price: series float) → series chartPoint — Builds a chart point from a time and a price.
chartPoint.new(time: series int, index: series int, price: series float) → series chartPoint — Builds a chart point with all three of its fields given: a time, a bar index and a price.
chartPoint.now(price?: series float) → series chartPoint — Builds a chart point from a price alone: you give no time and no bar index, and even the price is optional.

## color

library color — Seven functions: `color.new` and `color.rgb` build a colour, `color.from_gradient` builds one between two colours, and `color.r`, `color.g`, `color.b` and `color.a` read one apart.
type color — A colour.
color.a(color: const color) → const float — Reads the opacity of a colour.
color.a(color: input color) → input float — Reads the opacity of a colour.
color.a(color: simple color) → simple float — Reads the opacity of a colour.
color.a(color: series color) → series float — Reads the opacity of a colour.
constant color.aqua: const color — It is a predefined constant  for #00FFFF color.
color.b(color: const color) → const int — Reads the blue component of a colour.
color.b(color: input color) → input int — Reads the blue component of a colour.
color.b(color: simple color) → simple int — Reads the blue component of a colour.
color.b(color: series color) → series int — Reads the blue component of a colour.
constant color.black: const color — It is a predefined constant  for #000000 color.
constant color.blue: const color — It is a predefined constant  for #0000FF color.
color.from_gradient(value: const float, bottom_value: const float, top_value: const float, bottom_color: const color, top_color: const color) → const color — Returns a color calculated from the linear gradient between bottom_color and top_color based on the relative position of value within the range defined by bottom_value and top_value.
color.from_gradient(value: input float, bottom_value: input float, top_value: input float, bottom_color: input color, top_color: input color) → input color — Returns a color calculated from the linear gradient between bottom_color and top_color based on the relative position of value within the range defined by bottom_value and top_value.
color.from_gradient(value: simple float, bottom_value: simple float, top_value: simple float, bottom_color: simple color, top_color: simple color) → simple color — Returns a color calculated from the linear gradient between bottom_color and top_color based on the relative position of value within the range defined by bottom_value and top_value.
color.from_gradient(value: series float, bottom_value: series float, top_value: series float, bottom_color: series color, top_color: series color) → series color — Returns a color calculated from the linear gradient between bottom_color and top_color based on the relative position of value within the range defined by bottom_value and top_value.
constant color.fuchsia: const color — It is a predefined constant  for #FF00FF color.
color.g(color: const color) → const int — Reads the green component of a colour.
color.g(color: input color) → input int — Reads the green component of a colour.
color.g(color: simple color) → simple int — Reads the green component of a colour.
color.g(color: series color) → series int — Reads the green component of a colour.
constant color.gray: const color — It is a predefined constant  for #808080 color.
constant color.green: const color — It is a predefined constant  for #008000 color.
constant color.lime: const color — It is a predefined constant  for #00FF00 color.
constant color.maroon: const color — It is a predefined constant  for #800000 color.
constant color.navy: const color — It is a predefined constant  for #000080 color.
color.new(color: const color, alpha: const float) → const color — Takes a colour and an opacity, and returns that colour at that opacity.
color.new(color: input color, alpha: input float) → input color — Takes a colour and an opacity, and returns that colour at that opacity.
color.new(color: simple color, alpha: simple float) → simple color — Takes a colour and an opacity, and returns that colour at that opacity.
color.new(color: series color, alpha: series float) → series color — Takes a colour and an opacity, and returns that colour at that opacity.
constant color.olive: const color — It is a predefined constant  for #808000 color.
constant color.orange: const color — It is a predefined constant  for #FFA500 color.
constant color.purple: const color — It is a predefined constant  for #800080 color.
color.r(color: const color) → const int — Reads the red component back out of a colour.
color.r(color: input color) → input int — Reads the red component back out of a colour.
color.r(color: simple color) → simple int — Reads the red component back out of a colour.
color.r(color: series color) → series int — Reads the red component back out of a colour.
constant color.red: const color — It is a predefined constant  for #FF0000 color.
color.rgb(r: const int, g: const int, b: const int, a?: const float) → const color — Builds a colour from red, green and blue components, with an optional opacity.
color.rgb(r: input int, g: input int, b: input int, a?: input float) → input color — Builds a colour from red, green and blue components, with an optional opacity.
color.rgb(r: simple int, g: simple int, b: simple int, a?: simple float) → simple color — Builds a colour from red, green and blue components, with an optional opacity.
color.rgb(r: series int, g: series int, b: series int, a?: series float) → series color — Builds a colour from red, green and blue components, with an optional opacity.
constant color.silver: const color — It is a predefined constant  for #C0C0C0 color.
constant color.teal: const color — It is a predefined constant  for #008080 color.
constant color.white: const color — It is a predefined constant  for #FFFFFF color.
constant color.yellow: const color — It is a predefined constant  for #FFFF00 color.

## dayofweek

library dayofweek — Named weekday constants for comparisons with the `dayofweek` series or `dayofweek(time)`:
constant dayofweek.friday: const int — Weekday constant for Friday, an int with the value 6.
constant dayofweek.monday: const int — Weekday constant for Monday, an int with the value 2.
constant dayofweek.saturday: const int — Weekday constant for Saturday, an int with the value 7.
constant dayofweek.sunday: const int — Weekday constant for Sunday, an int with the value 1.
constant dayofweek.thursday: const int — Weekday constant for Thursday, an int with the value 5.
constant dayofweek.tuesday: const int — Weekday constant for Tuesday, an int with the value 3.
constant dayofweek.wednesday: const int — Weekday constant for Wednesday, an int with the value 4.

## extend

library extend — Named constants that control whether line/box drawings extend past their endpoints (none, left, right, both).
constant extend.both: const string — Extend the drawing in both directions.
constant extend.left: const string — Extend the drawing to the left of the first point.
constant extend.none: const string — Do not extend the drawing past its endpoints.
constant extend.right: const string — Extend the drawing to the right of the second point.

## format

library format — Named formats for script values: `format.inherit`, `format.price`, `format.percent`, `format.volume` and `format.mintick`.
constant format.inherit: const string — A format for script values, for the `format` argument of `indicator` and `strategy`.
constant format.mintick: const string — A format for script values, for the `format` argument of `str.tostring`.
constant format.percent: const string — A format for script values, for the `format` argument of `indicator`, `strategy` and the plot functions (`plot`, `hline`, `plotarrow`, `plotchar`, `plotshape`).
constant format.price: const string — A format for script values, for the `format` argument of `indicator`, `strategy` and the plot functions (`plot`, `hline`, `plotarrow`, `plotchar`, `plotshape`).
constant format.volume: const string — A format for script values, for the `format` argument of `indicator`, `strategy` and the plot functions (`plot`, `hline`, `plotarrow`, `plotchar`, `plotshape`).

## input

library input — Twelve functions, one per kind of setting the reader can change from the chart: bool, colour, enum, float, int, price, session, source, string, text area, time and timeframe.
input.bool(defval: const bool, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input bool — Offers the reader a true-or-false setting and hands back what they chose.
input.color(defval: const color, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input color — Asks the reader for a colour.
input.enum(defval: const enum, title?: const string, options?: [const enum...], tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input enum — Adds a dropdown setting whose choices are the members of an enum you declare.
input.float(defval: const float, title?: const string, minval?: const float, maxval?: const float, step?: const float, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input float — The decimal counterpart of `input.int`, with the same arguments and `const float` in place of `const int`.
input.float(defval: const float, title?: const string, options?: [const float...], tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input float — The decimal counterpart of `input.int`, with the same arguments and `const float` in place of `const int`.
input.int(defval: const int, title?: const string, minval?: const int, maxval?: const int, step?: const int, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input int — A whole-number setting, with optional bounds and an optional increment.
input.int(defval: const int, title?: const string, options?: [const int...], tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input int — A whole-number setting, with optional bounds and an optional increment.
input.price(defval: const float, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input float — A price setting.
input.session(defval: const string, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input string — Asks the reader for a session and gives you back a string.
input.source(defval: series float, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → series float — Lets the reader pick which series the script reads — the close, the high, a midpoint, and so on.
input.string(defval: const string, title?: const string, options?: [const string...], tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input string — A one-line text setting.
input.text_area(defval: const string, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input string — A multi-line text setting, for a message or a note rather than a single word.
input.time(defval: const int, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input int — A time setting, returned as an int.
input.timeframe(defval: const string, title?: const string, tooltip?: const string, inline?: const string, group?: const string, confirm?: const bool, display?: const display) → input string — Asks the reader for a timeframe.

## interval

library interval — Eleven values describing the interval the chart is drawn on: the interval itself, its multiplier, its length in minutes, and eight booleans for what kind of interval it is.
interval.change(interval: series string) → series bool — Returns true on the first bar of each new period of `interval`, for example on the first bar of every day when `interval` is "1D".
interval.from_seconds(seconds: series int) → series string — Returns the interval string for a length in seconds, rounded up to the next supported interval.
interval.in_seconds(interval?: series string) → series int — Returns the length of `interval` in seconds, for example 86400 for "1D".
variable interval.interval: simple string — The interval the chart is drawn on, as a string.
variable interval.isdaily: simple bool — True when the interval is daily.
variable interval.iseod: simple bool — True when the interval is an end-of-day interval: a day, a week or a month.
variable interval.ishourly: simple bool — True when the interval is hourly.
variable interval.isintraday: simple bool — True when the chart's interval is intraday.
variable interval.isminutes: simple bool — True when the interval is measured in minutes.
variable interval.ismonthly: simple bool — True when the interval is monthly.
variable interval.isseconds: simple bool — True when the chart's interval is measured in seconds.
variable interval.isweekly: simple bool — True when the interval is weekly.
variable interval.multiplier: simple int — The multiplier of the chart's interval, as a whole number.
variable interval.timeframe_minutes: simple int — The chart's interval counted in minutes.

## label

library label — Functions for creating and mutating text label drawings on the chart.
type label — A text marker anchored to a bar/price.
variable label.all: series array<label> — Array of all currently existing label drawings, from oldest to newest.
label.all() → series array<label> — Returns the array of all existing label objects (same as label.all).
label.copy(id: series label) → series label — Creates a copy of a label.
label.delete(id: series label) → void — Deletes a label.
label.get_text(id: series label) → series string — Returns a label's text.
label.get_x(id: series label) → series int — Returns a label's x-coordinate.
label.get_y(id: series label) → series float — Returns a label's y-coordinate (price).
label.new(x: series int, y: series float, text?: series string, xloc?: series string, yloc?: series string, color?: series color, style?: series string, textcolor?: series color, size?: series size, textalign?: series string, tooltip?: series string, text_font_family?: input font, force_overlay?: const bool, text_formatting?: series string) → series label — Creates a label at (x, y) with optional text, color, and style.
label.set_color(id: series label, color: series color) → void — Sets a label's background color.
label.set_point(id: series label, point: series chartPoint) → void — Sets a label's position from a chartPoint.
label.set_size(id: series label, size: series size) → void — Sets a label's size.
label.set_style(id: series label, style: series string) → void — Sets a label's style (label.style_*).
label.set_text(id: series label, text: series string) → void — Sets a label's text.
label.set_text_font_family(id: series label, family: input font) → void — Sets a label's font family.
label.set_text_formatting(id: series label, formatting: series string) → void — Sets a label's text formatting.
label.set_textalign(id: series label, textalign: series string) → void — Sets a label's text alignment.
label.set_textcolor(id: series label, textcolor: series color) → void — Sets a label's text color.
label.set_tooltip(id: series label, tooltip: series string) → void — Sets a label's tooltip.
label.set_x(id: series label, x: series int) → void — Sets a label's x-coordinate.
label.set_xloc(id: series label, x: series int, xloc: series string) → void — Sets whether a label's x-coordinate is a bar index or time.
label.set_xy(id: series label, x: series int, y: series float) → void — Sets a label's x and y coordinates.
label.set_y(id: series label, y: series float) → void — Sets a label's y-coordinate (price).
label.set_yloc(id: series label, yloc: series string) → void — Sets a label's vertical location relative to the bar.
constant label.style_arrowdown: const string — Down-arrow marker style.
constant label.style_arrowup: const string — Up-arrow marker style.
constant label.style_circle: const string — Circle marker style.
constant label.style_cross: const string — Cross marker style.
constant label.style_diamond: const string — Diamond marker style.
constant label.style_flag: const string — Flag marker style.
constant label.style_label_center: const string — Centered label bubble.
constant label.style_label_down: const string — Label bubble pointing down.
constant label.style_label_left: const string — Label bubble pointing left.
constant label.style_label_lower_left: const string — Label bubble in the lower-left.
constant label.style_label_lower_right: const string — Label bubble in the lower-right.
constant label.style_label_right: const string — Label bubble pointing right.
constant label.style_label_up: const string — Label bubble pointing up.
constant label.style_label_upper_left: const string — Label bubble in the upper-left.
constant label.style_label_upper_right: const string — Label bubble in the upper-right.
constant label.style_none: const string — Label with no visual style.
constant label.style_square: const string — Square marker style.
constant label.style_text_outline: const string — Text with an outline.
constant label.style_triangledown: const string — Down-pointing triangle marker.
constant label.style_triangleup: const string — Up-pointing triangle marker.
constant label.style_xcross: const string — X-cross marker style.

## line

library line — Functions for creating and mutating line drawings between two chart points.
type line — A line drawing between two chart points.
variable line.all: series array<line> — Array of all currently existing line drawings, from oldest to newest.
line.all() → series array<line> — Returns the array of all existing line objects (same as line.all).
line.copy(id: series line) → series line — Creates a copy of a line.
line.delete(id: series line) → void — Deletes a line.
line.get_price(id: series line, x: series int) → series float — Returns the price of a line at x (interpolated between the two endpoints).
line.get_x1(id: series line) → series int — Returns the first point's x-coordinate.
line.get_x2(id: series line) → series int — Returns the second point's x-coordinate.
line.get_y1(id: series line) → series float — Returns the first point's y-coordinate.
line.get_y2(id: series line) → series float — Returns the second point's y-coordinate.
line.new(x1: series int, y1: series float, x2: series int, y2: series float, xloc?: series string, extend?: series string, color?: series color, style?: series string, width?: series int, forceOverlay?: const bool) → series line — Creates a line between two points.
line.new(first_point: series chartPoint, second_point: series chartPoint, xloc?: series string, extend?: series string, color?: series color, style?: series string, width?: series int, forceOverlay?: const bool) → series line — Creates a line between two points.
line.set_color(id: series line, color: series color) → void — Sets a line's color.
line.set_extend(id: series line, extend: series string) → void — Sets whether a line extends past its endpoints.
line.set_point1(id: series line, point: series chartPoint) → void — Sets a line's first endpoint from a chartPoint.
line.set_point2(id: series line, point: series chartPoint) → void — Sets a line's second endpoint from a chartPoint.
line.set_style(id: series line, style: series string) → void — Sets a line's style (line.style_*).
line.set_width(id: series line, width: series int) → void — Sets a line's width in pixels.
line.set_x1(id: series line, x1: series int) → void — Sets a line's first x-coordinate.
line.set_x2(id: series line, x2: series int) → void — Sets a line's second x-coordinate.
line.set_xloc(id: series line, xloc: series string) → void — Sets whether a line's x-coordinates are bar indexes or times.
line.set_xloc(id: series line, xloc: series string, x1: series int, x2: series int) → void — Sets whether a line's x-coordinates are bar indexes or times.
line.set_xy1(id: series line, x1: series int, y1: series float) → void — Sets a line's first endpoint (x1, y1).
line.set_xy2(id: series line, x2: series int, y2: series float) → void — Sets a line's second endpoint (x2, y2).
line.set_y1(id: series line, y1: series float) → void — Sets a line's first y-coordinate.
line.set_y2(id: series line, y2: series float) → void — Sets a line's second y-coordinate.
constant line.style_arrow_both: const string — Line style with arrows on both points.
constant line.style_arrow_left: const string — Line style with an arrow on the first point.
constant line.style_arrow_right: const string — Line style with an arrow on the second point.
constant line.style_dashed: const string — Dashed line style for line.new / line.set_style.
constant line.style_dotted: const string — Dotted line style for line.new / line.set_style.
constant line.style_solid: const string — Solid line style for line.new / line.set_style.

## linefill

library linefill — Functions for filling the region between two line drawings.
type linefill — A colored fill between two line drawings.
variable linefill.all: series array<linefill> — Array of all currently existing linefill drawings, from oldest to newest.
linefill.all() → series array<linefill> — Returns the array of all existing linefill objects (same as the linefill.all variable).
linefill.delete(id: series linefill) → void — Deletes a linefill.
linefill.get_line1(id: series linefill) → series line — Returns the first line used when the fill was created.
linefill.get_line2(id: series linefill) → series line — Returns the second line used when the fill was created.
linefill.new(line1: series line, line2: series line, color?: series color) → series linefill — Creates a fill between two lines.
linefill.set_color(id: series linefill, color: series color) → void — Sets the fill color of an existing linefill.

## math

library math — Twenty-three arithmetic and trigonometric functions, and four constants: `math.pi`, `math.e`, `math.phi` and `math.rphi`.
math.abs(number: const int) → const int — The absolute value of `number`: its magnitude, with the sign removed.
math.abs(number: input int) → input int — The absolute value of `number`: its magnitude, with the sign removed.
math.abs(number: simple int) → simple int — The absolute value of `number`: its magnitude, with the sign removed.
math.abs(number: series int) → series int — The absolute value of `number`: its magnitude, with the sign removed.
math.abs(number: const float) → const float — The absolute value of `number`: its magnitude, with the sign removed.
math.abs(number: input float) → input float — The absolute value of `number`: its magnitude, with the sign removed.
math.abs(number: simple float) → simple float — The absolute value of `number`: its magnitude, with the sign removed.
math.abs(number: series float) → series float — The absolute value of `number`: its magnitude, with the sign removed.
math.acos(angle: const float) → const float — The arccosine of `angle`, in radians.
math.acos(angle: input float) → input float — The arccosine of `angle`, in radians.
math.acos(angle: simple float) → simple float — The arccosine of `angle`, in radians.
math.acos(angle: series float) → series float — The arccosine of `angle`, in radians.
math.asin(angle: const float) → const float — The arcsine of `angle`, in radians.
math.asin(angle: input float) → input float — The arcsine of `angle`, in radians.
math.asin(angle: simple float) → simple float — The arcsine of `angle`, in radians.
math.asin(angle: series float) → series float — The arcsine of `angle`, in radians.
math.atan(angle: const float) → const float — The arctangent of `angle`, in radians.
math.atan(angle: input float) → input float — The arctangent of `angle`, in radians.
math.atan(angle: simple float) → simple float — The arctangent of `angle`, in radians.
math.atan(angle: series float) → series float — The arctangent of `angle`, in radians.
math.avg(number0, number1, ...: const float) → const float — The arithmetic mean of the numbers you pass: their sum divided by how many there are.
math.avg(number0, number1, ...: input float) → input float — The arithmetic mean of the numbers you pass: their sum divided by how many there are.
math.avg(number0, number1, ...: simple float) → simple float — The arithmetic mean of the numbers you pass: their sum divided by how many there are.
math.avg(number0, number1, ...: series float) → series float — The arithmetic mean of the numbers you pass: their sum divided by how many there are.
math.ceil(number: const float) → const int — The smallest whole number that is not less than `number`.
math.ceil(number: input float) → input int — The smallest whole number that is not less than `number`.
math.ceil(number: simple float) → simple int — The smallest whole number that is not less than `number`.
math.ceil(number: series float) → series int — The smallest whole number that is not less than `number`.
math.cos(angle: const float) → const float — The cosine of `angle`, where the angle is in radians.
math.cos(angle: input float) → input float — The cosine of `angle`, where the angle is in radians.
math.cos(angle: simple float) → simple float — The cosine of `angle`, where the angle is in radians.
math.cos(angle: series float) → series float — The cosine of `angle`, where the angle is in radians.
constant math.e: const float — Euler's number: the base of the natural logarithm, 2.718281828459045.
math.exp(number: const float) → const float — Euler's number raised to the power of `number`.
math.exp(number: input float) → input float — Euler's number raised to the power of `number`.
math.exp(number: simple float) → simple float — Euler's number raised to the power of `number`.
math.exp(number: series float) → series float — Euler's number raised to the power of `number`.
math.floor(number: const float) → const int — The largest whole number that is not greater than `number`.
math.floor(number: input float) → input int — The largest whole number that is not greater than `number`.
math.floor(number: simple float) → simple int — The largest whole number that is not greater than `number`.
math.floor(number: series float) → series int — The largest whole number that is not greater than `number`.
math.log(number: const float) → const float — The natural logarithm of `number`: its logarithm to base e.
math.log(number: input float) → input float — The natural logarithm of `number`: its logarithm to base e.
math.log(number: simple float) → simple float — The natural logarithm of `number`: its logarithm to base e.
math.log(number: series float) → series float — The natural logarithm of `number`: its logarithm to base e.
math.log10(number: const float) → const float — The base-10 logarithm of `number`.
math.log10(number: input float) → input float — The base-10 logarithm of `number`.
math.log10(number: simple float) → simple float — The base-10 logarithm of `number`.
math.log10(number: series float) → series float — The base-10 logarithm of `number`.
math.max(number0, number1, ...: const int) → const int — The largest of the numbers you pass.
math.max(number0, number1, ...: input int) → input int — The largest of the numbers you pass.
math.max(number0, number1, ...: simple int) → simple int — The largest of the numbers you pass.
math.max(number0, number1, ...: series int) → series int — The largest of the numbers you pass.
math.max(number0, number1, ...: const float) → const float — The largest of the numbers you pass.
math.max(number0, number1, ...: input float) → input float — The largest of the numbers you pass.
math.max(number0, number1, ...: simple float) → simple float — The largest of the numbers you pass.
math.max(number0, number1, ...: series float) → series float — The largest of the numbers you pass.
math.min(number0, number1, ...: const int) → const int — The smallest of the numbers you pass.
math.min(number0, number1, ...: input int) → input int — The smallest of the numbers you pass.
math.min(number0, number1, ...: simple int) → simple int — The smallest of the numbers you pass.
math.min(number0, number1, ...: series int) → series int — The smallest of the numbers you pass.
math.min(number0, number1, ...: const float) → const float — The smallest of the numbers you pass.
math.min(number0, number1, ...: input float) → input float — The smallest of the numbers you pass.
math.min(number0, number1, ...: simple float) → simple float — The smallest of the numbers you pass.
math.min(number0, number1, ...: series float) → series float — The smallest of the numbers you pass.
constant math.phi: const float — The golden ratio: the positive number whose square is one greater than itself, 1.618033988749895.
constant math.pi: const float — Archimedes' constant: the ratio of a circle's circumference to its diameter, 3.141592653589793.
math.pow(base: const float, exponent: const float) → const float — `base` raised to the power of `exponent`.
math.pow(base: input float, exponent: input float) → input float — `base` raised to the power of `exponent`.
math.pow(base: simple float, exponent: simple float) → simple float — `base` raised to the power of `exponent`.
math.pow(base: series float, exponent: series float) → series float — `base` raised to the power of `exponent`.
math.random(min?: series float, max?: series float) → series float — Gives your script a random float, bounded below by `min` and above by `max`.
math.round(number: const float) → const int — Rounds `number` to the nearest whole number and returns an int.
math.round(number: input float) → input int — Rounds `number` to the nearest whole number and returns an int.
math.round(number: simple float) → simple int — Rounds `number` to the nearest whole number and returns an int.
math.round(number: series float) → series int — Rounds `number` to the nearest whole number and returns an int.
math.round(number: const float, precision: const int) → const float — Rounds `number` to the nearest whole number and returns an int.
math.round(number: input float, precision: input int) → input float — Rounds `number` to the nearest whole number and returns an int.
math.round(number: simple float, precision: simple int) → simple float — Rounds `number` to the nearest whole number and returns an int.
math.round(number: series float, precision: series int) → series float — Rounds `number` to the nearest whole number and returns an int.
math.round_to_mintick(number: const float) → const float — Rounds `number` to the nearest multiple of `syminfo.mintick` for the chart symbol.
math.round_to_mintick(number: input float) → input float — Rounds `number` to the nearest multiple of `syminfo.mintick` for the chart symbol.
math.round_to_mintick(number: simple float) → simple float — Rounds `number` to the nearest multiple of `syminfo.mintick` for the chart symbol.
math.round_to_mintick(number: series float) → series float — Rounds `number` to the nearest multiple of `syminfo.mintick` for the chart symbol.
constant math.rphi: const float — The golden ratio conjugate: the reciprocal of the golden ratio, 0.6180339887498948.
math.sign(number: const float) → const float — The sign of `number`: -1 for a negative number and 1 for a positive one.
math.sign(number: input float) → input float — The sign of `number`: -1 for a negative number and 1 for a positive one.
math.sign(number: simple float) → simple float — The sign of `number`: -1 for a negative number and 1 for a positive one.
math.sign(number: series float) → series float — The sign of `number`: -1 for a negative number and 1 for a positive one.
math.sin(angle: const float) → const float — The sine of `angle`, where the angle is in radians.
math.sin(angle: input float) → input float — The sine of `angle`, where the angle is in radians.
math.sin(angle: simple float) → simple float — The sine of `angle`, where the angle is in radians.
math.sin(angle: series float) → series float — The sine of `angle`, where the angle is in radians.
math.sqrt(number: const float) → const float — The square root of `number`.
math.sqrt(number: input float) → input float — The square root of `number`.
math.sqrt(number: simple float) → simple float — The square root of `number`.
math.sqrt(number: series float) → series float — The square root of `number`.
math.sum(source: series float, length: series int) → series float — Adds up the last `length` values of `source`.
math.tan(angle: const float) → const float — The tangent of `angle`, where the angle is in radians.
math.tan(angle: input float) → input float — The tangent of `angle`, where the angle is in radians.
math.tan(angle: simple float) → simple float — The tangent of `angle`, where the angle is in radians.
math.tan(angle: series float) → series float — The tangent of `angle`, where the angle is in radians.
math.todegrees(radians: const float) → const float — Converts an angle in radians to the same angle in degrees.
math.todegrees(radians: input float) → input float — Converts an angle in radians to the same angle in degrees.
math.todegrees(radians: simple float) → simple float — Converts an angle in radians to the same angle in degrees.
math.todegrees(radians: series float) → series float — Converts an angle in radians to the same angle in degrees.
math.toradians(degrees: const float) → const float — Converts an angle in degrees to the same angle in radians.
math.toradians(degrees: input float) → input float — Converts an angle in degrees to the same angle in radians.
math.toradians(degrees: simple float) → simple float — Converts an angle in degrees to the same angle in radians.
math.toradians(degrees: series float) → series float — Converts an angle in degrees to the same angle in radians.

## order

library order — The two sort orders, `order.ascending` and `order.descending`, for `array.sort` and `array.sort_indices`.
constant order.ascending: const string — Sort order from the smallest value to the largest, for `array.sort` and `array.sort_indices`.
constant order.descending: const string — Sort order from the largest value to the smallest, for `array.sort` and `array.sort_indices`.

## orderflow

library orderflow — Ten integer series read from a bar's footprint data — buy and sell trade counts, buy and sell volumes, delta with its intra-bar extremes, and the commitment-of-traders high and low — plus one function, `orderflow.cvd()`.
variable orderflow.buy: series int — How many buy trades the bar carried.
variable orderflow.buyvolume: series int — The volume bought in the bar.
variable orderflow.cothigh: series int — The commitment-of-traders high for the bar, taken from the same per-bar footprint summary as the delta figures.
variable orderflow.cotlow: series int — The commitment-of-traders low for the bar.
orderflow.cvd() → series int — Cumulative volume delta.
variable orderflow.delta: series int — The bar's delta as at its close.
variable orderflow.maxdelta: series int — The highest delta the bar reached while it was forming.
variable orderflow.mindelta: series int — The lowest delta the bar reached while it was forming.
variable orderflow.sell: series int — How many sell trades the bar carried.
variable orderflow.sellvolume: series int — The volume sold in the bar.
variable orderflow.trades: series int — The bar's overall trade count.

## polyline

library polyline — Functions for creating and deleting multi-point polyline drawings from an array of chartPoint vertices.
type polyline — A multi-point drawing built from an array of chartPoint values.
variable polyline.all: series array<polyline> — Array of all currently existing polyline drawings, from oldest to newest.
polyline.all() → series array<polyline> — Returns the array of all existing polyline objects (same as the polyline.all variable).
polyline.delete(id: series polyline) → void — Deletes a polyline object.
polyline.new(points: series array<chartPoint>, curved?: series bool, closed?: series bool, xloc?: series string, line_color?: series color, fill_color?: series color, line_style?: series string, line_width?: series int, force_overlay?: const bool) → series polyline — Creates a polyline from an array of chartPoint objects.

## position

library position — Named constants for table placement on the chart pane (top/middle/bottom × left/center/right).
constant position.bottom_center: const string — Table position: bottom-center of the chart pane.
constant position.bottom_left: const string — Table position: bottom-left corner of the chart pane.
constant position.bottom_right: const string — Table position: bottom-right corner of the chart pane.
constant position.middle_center: const string — Table position: center of the chart pane.
constant position.middle_left: const string — Table position: middle-left of the chart pane.
constant position.middle_right: const string — Table position: middle-right of the chart pane.
constant position.top_center: const string — Table position: top-center of the chart pane.
constant position.top_left: const string — Table position: top-left corner of the chart pane.
constant position.top_right: const string — Table position: top-right corner of the chart pane.

## session

library session — Two values about the session the current bar falls in: its date, and whether this is the session's first bar.
variable session.date: series string — The date of the session the current bar falls in.
variable session.isfirst: series bool — True on the first bar of a session.

## str

library str — Seventeen functions for working with text: tests such as `str.contains` and `str.startswith`, transformations such as `str.replace` and `str.substring`, conversions in both directions with `str.tonumber` and `str.tostring`, and `str.format_time` for rendering a time.
str.contains(source: const string, str: const string) → const bool — Tests whether one string occurs inside another.
str.contains(source: input string, str: input string) → input bool — Tests whether one string occurs inside another.
str.contains(source: simple string, str: simple string) → simple bool — Tests whether one string occurs inside another.
str.contains(source: series string, str: series string) → series bool — Tests whether one string occurs inside another.
str.endswith(source: const string, suffix: const string) → const bool — Asks whether a string finishes with a given ending.
str.endswith(source: input string, suffix: input string) → input bool — Asks whether a string finishes with a given ending.
str.endswith(source: simple string, suffix: simple string) → simple bool — Asks whether a string finishes with a given ending.
str.endswith(source: series string, suffix: series string) → series bool — Asks whether a string finishes with a given ending.
str.format_time(time_value: const int, format: const string, timezone?: const string) → const string — Renders a time as text, in a format and a time zone you give.
str.format_time(time_value: input int, format: input string, timezone?: input string) → input string — Renders a time as text, in a format and a time zone you give.
str.format_time(time_value: simple int, format: simple string, timezone?: simple string) → simple string — Renders a time as text, in a format and a time zone you give.
str.format_time(time_value: series int, format: series string, timezone?: series string) → series string — Renders a time as text, in a format and a time zone you give.
str.length(source: const string) → const int — Gives the length of a string as an int.
str.length(source: input string) → input int — Gives the length of a string as an int.
str.length(source: simple string) → simple int — Gives the length of a string as an int.
str.length(source: series string) → series int — Gives the length of a string as an int.
str.lower(source: const string) → const string — Converts a string to lower case.
str.lower(source: input string) → input string — Converts a string to lower case.
str.lower(source: simple string) → simple string — Converts a string to lower case.
str.lower(source: series string) → series string — Converts a string to lower case.
str.match(source: const string, pattern: const string) → const string — Returns the first part of `source` that matches the regular expression `pattern`.
str.match(source: input string, pattern: input string) → input string — Returns the first part of `source` that matches the regular expression `pattern`.
str.match(source: simple string, pattern: simple string) → simple string — Returns the first part of `source` that matches the regular expression `pattern`.
str.match(source: series string, pattern: series string) → series string — Returns the first part of `source` that matches the regular expression `pattern`.
str.pos(source: const string, str: const string) → const int — Reports the position at which one string sits inside another.
str.pos(source: input string, str: input string) → input int — Reports the position at which one string sits inside another.
str.pos(source: simple string, str: simple string) → simple int — Reports the position at which one string sits inside another.
str.pos(source: series string, str: series string) → series int — Reports the position at which one string sits inside another.
str.repeat(source: const string, count: const int, separator?: const string) → const string — Produces a string made of repeated copies of another, with the option of something between the copies.
str.repeat(source: input string, count: input int, separator?: input string) → input string — Produces a string made of repeated copies of another, with the option of something between the copies.
str.repeat(source: simple string, count: simple int, separator?: simple string) → simple string — Produces a string made of repeated copies of another, with the option of something between the copies.
str.repeat(source: series string, count: series int, separator?: series string) → series string — Produces a string made of repeated copies of another, with the option of something between the copies.
str.replace(source: const string, old: const string, new: const string, count?: const int) → const string — Substitutes one piece of text for another inside a string.
str.replace(source: input string, old: input string, new: input string, count?: input int) → input string — Substitutes one piece of text for another inside a string.
str.replace(source: simple string, old: simple string, new: simple string, count?: simple int) → simple string — Substitutes one piece of text for another inside a string.
str.replace(source: series string, old: series string, new: series string, count?: series int) → series string — Substitutes one piece of text for another inside a string.
str.replace_all(source: const string, old: const string, new: const string) → const string — Substitutes new text for every occurrence of the old text.
str.replace_all(source: input string, old: input string, new: input string) → input string — Substitutes new text for every occurrence of the old text.
str.replace_all(source: simple string, old: simple string, new: simple string) → simple string — Substitutes new text for every occurrence of the old text.
str.replace_all(source: series string, old: series string, new: series string) → series string — Substitutes new text for every occurrence of the old text.
str.split(string: const string, separator: const string) → series array<string> — Splits `string` wherever `separator` occurs and returns the pieces as an array of strings.
str.split(string: input string, separator: input string) → series array<string> — Splits `string` wherever `separator` occurs and returns the pieces as an array of strings.
str.split(string: simple string, separator: simple string) → series array<string> — Splits `string` wherever `separator` occurs and returns the pieces as an array of strings.
str.split(string: series string, separator: series string) → series array<string> — Splits `string` wherever `separator` occurs and returns the pieces as an array of strings.
str.startswith(source: const string, prefix: const string) → const bool — The counterpart of str.endswith, looking at the front of the string instead of the back.
str.startswith(source: input string, prefix: input string) → input bool — The counterpart of str.endswith, looking at the front of the string instead of the back.
str.startswith(source: simple string, prefix: simple string) → simple bool — The counterpart of str.endswith, looking at the front of the string instead of the back.
str.startswith(source: series string, prefix: series string) → series bool — The counterpart of str.endswith, looking at the front of the string instead of the back.
str.substring(source: const string, start: const int, end: const int) → const string — Cuts a piece out of a string.
str.substring(source: input string, start: input int, end: input int) → input string — Cuts a piece out of a string.
str.substring(source: simple string, start: simple int, end: simple int) → simple string — Cuts a piece out of a string.
str.substring(source: series string, start: series int, end: series int) → series string — Cuts a piece out of a string.
str.substring(source: const string, start: const int) → const string — Cuts a piece out of a string.
str.substring(source: input string, start: input int) → input string — Cuts a piece out of a string.
str.substring(source: simple string, start: simple int) → simple string — Cuts a piece out of a string.
str.substring(source: series string, start: series int) → series string — Cuts a piece out of a string.
str.tonumber(source: const string) → const float — Reads a number out of a string.
str.tonumber(source: input string) → input float — Reads a number out of a string.
str.tonumber(source: simple string) → simple float — Reads a number out of a string.
str.tonumber(source: series string) → series float — Reads a number out of a string.
str.tostring(source: simple float) → simple string — Renders a value as a string.
str.tostring(source: series float) → series string — Renders a value as a string.
str.tostring(value: simple float, format?: simple string, mintick?: simple float) → simple string — Renders a value as a string.
str.tostring(value: series float, format?: series string, mintick?: simple float) → series string — Renders a value as a string.
str.tostring(source: simple bool) → simple string — Renders a value as a string.
str.tostring(source: series bool) → series string — Renders a value as a string.
str.trim(source: const string) → const string — Removes whitespace from around a string and hands back the result.
str.trim(source: input string) → input string — Removes whitespace from around a string and hands back the result.
str.trim(source: simple string) → simple string — Removes whitespace from around a string and hands back the result.
str.trim(source: series string) → series string — Removes whitespace from around a string and hands back the result.
str.upper(source: const string) → const string — Converts a string to upper case; the other half of the pair with str.lower.
str.upper(source: input string) → input string — Converts a string to upper case; the other half of the pair with str.lower.
str.upper(source: simple string) → simple string — Converts a string to upper case; the other half of the pair with str.lower.
str.upper(source: series string) → series string — Converts a string to upper case; the other half of the pair with str.lower.

## strategy

library strategy — Functions, variables and constants for strategies: scripts declared with `strategy()` that place simulated orders.
variable strategy.account_currency: series string — The currency the strategy's figures are reported in, as a string.
strategy.cancel(id: series string) → void — Cancels the pending order named `id`: a limit or stop order that has not filled yet.
strategy.cancel_all() → void — Cancels every pending order that has not filled yet.
strategy.close(id: series string, qty?: series float, comment?: series string) → void — Closes the position opened by the entry named `id` with a market order.
strategy.close_all(comment?: series string) → void — Closes the whole open position, whatever entries it came from, with a market order.
variable strategy.closedtrades: series int — The number of trades closed so far.
strategy.closedtrades_commission(trade_num: series int) → series float — For the closed trade number `trade_num`, returns the commission paid on the trade, in the account currency.
strategy.closedtrades_entry_bar_index(trade_num: series int) → series int — For the closed trade number `trade_num`, returns the bar index of the bar on which the entry order was placed (where `strategy.entry` or `strategy.order` ran), not the bar on which it filled; the two differ when the order fills on a later bar.
strategy.closedtrades_entry_comment(trade_num: series int) → series string — For the closed trade number `trade_num`, returns the comment of the entry order that opened the trade.
strategy.closedtrades_entry_id(trade_num: series int) → series string — For the closed trade number `trade_num`, returns the `id` of the entry order that opened the trade.
strategy.closedtrades_entry_price(trade_num: series int) → series float — For the closed trade number `trade_num`, returns the price at which the trade was entered.
strategy.closedtrades_entry_time(trade_num: series int) → series int — For the closed trade number `trade_num`, returns the UNIX time, in milliseconds, at which the trade was entered.
strategy.closedtrades_exit_bar_index(trade_num: series int) → series int — For the closed trade number `trade_num`, returns the bar index at which the trade was closed.
strategy.closedtrades_exit_price(trade_num: series int) → series float — For the closed trade number `trade_num`, returns the price at which the trade was closed.
strategy.closedtrades_exit_time(trade_num: series int) → series int — For the closed trade number `trade_num`, returns the UNIX time, in milliseconds, at which the trade was closed.
strategy.closedtrades_max_drawdown(trade_num: series int) → series float — For the closed trade number `trade_num`, returns the largest loss the trade showed while it was open, in the account currency.
strategy.closedtrades_max_runup(trade_num: series int) → series float — For the closed trade number `trade_num`, returns the largest profit the trade showed while it was open, in the account currency.
strategy.closedtrades_profit(trade_num: series int) → series float — For the closed trade number `trade_num`, returns the profit of the trade, in the account currency; a loss is negative.
strategy.closedtrades_size(trade_num: series int) → series float — For the closed trade number `trade_num`, returns the size of the trade.
constant strategy.commission_cash_per_contract: const string — A commission type for the `commission_type` argument of `strategy()`: `commission_value` is an amount, in the account currency, charged per contract traded.
constant strategy.commission_cash_per_order: const string — A commission type for the `commission_type` argument of `strategy()`: `commission_value` is a fixed amount, in the account currency, charged for each trade opened and for each trade closed.
constant strategy.commission_percent: const string — A commission type for the `commission_type` argument of `strategy()`: `commission_value` is a percentage of each order's value.
strategy.entry(id: series string, direction: series string, qty?: series float, limit?: series float, stop?: series float, oca_name?: series string, oca_type?: series string, comment?: series string) → void — Opens a position, or adds to one, in `direction` (`strategy.long` or `strategy.short`).
variable strategy.equity: series float — The strategy's current equity: initial capital plus net profit plus open profit.
strategy.exit(id: series string, from_entry?: series string, qty?: series float, profit?: series float, limit?: series float, loss?: series float, stop?: series float, oca_name?: series string, comment?: series string) → void — Places exit orders for an open position: a take-profit, a stop-loss, or both.
constant strategy.fixed: const string — A position-size type for the `default_qty_type` argument of `strategy()`: `default_qty_value` is a fixed number of contracts, shares or units per order.
variable strategy.grossloss: series float — The total of the profits of all closed trades that did not make a profit, so it is zero or negative: a trade that lost 10 adds -10.
variable strategy.grossprofit: series float — The total profit of all winning closed trades.
variable strategy.initial_capital: series float — The initial capital set in `strategy()`.
constant strategy.long: const string — The long direction, for the `direction` argument of `strategy.entry` and `strategy.order`: buy to open or add to a long position.
variable strategy.losstrades: series int — The number of closed trades whose profit is zero or negative: a trade that closes at break-even counts here, so `strategy.wintrades` plus `strategy.losstrades` equals `strategy.closedtrades`.
variable strategy.max_drawdown: series float — The largest peak-to-trough fall in equity so far.
variable strategy.max_runup: series float — The largest trough-to-peak rise in equity so far.
variable strategy.netprofit: series float — The total profit of all closed trades, net of commission; a loss is negative.
constant strategy.oca_cancel: const string — A one-cancels-all type, for the `oca_type` argument of `strategy.entry` and `strategy.order`.
constant strategy.oca_none: const string — A one-cancels-all type, for the `oca_type` argument of `strategy.entry` and `strategy.order`.
constant strategy.oca_reduce: const string — A one-cancels-all type, for the `oca_type` argument of `strategy.entry` and `strategy.order`.
variable strategy.openprofit: series float — The current, unrealised profit of the open position; a loss is negative.
variable strategy.opentrades: series int — The number of trades open now (entries not yet closed).
strategy.opentrades_entry_bar_index(trade_num: series int) → series int — For the open trade number `trade_num`, returns the bar index of the bar on which the entry order was placed (where `strategy.entry` or `strategy.order` ran), not the bar on which it filled; the two differ when the order fills on a later bar.
strategy.opentrades_entry_comment(trade_num: series int) → series string — For the open trade number `trade_num`, returns the comment of the entry order that opened the trade.
strategy.opentrades_entry_id(trade_num: series int) → series string — For the open trade number `trade_num`, returns the `id` of the entry order that opened the trade.
strategy.opentrades_entry_price(trade_num: series int) → series float — For the open trade number `trade_num`, returns the price at which the trade was entered.
strategy.opentrades_entry_time(trade_num: series int) → series int — For the open trade number `trade_num`, returns the UNIX time, in milliseconds, at which the trade was entered.
strategy.opentrades_max_drawdown(trade_num: series int) → series float — For the open trade number `trade_num`, returns the largest fall of the trade's profit from its highest profit so far, in the account currency.
strategy.opentrades_max_runup(trade_num: series int) → series float — For the open trade number `trade_num`, returns the highest profit the trade has shown so far, in the account currency (0 until the trade is in profit).
strategy.opentrades_profit(trade_num: series int) → series float — For the open trade number `trade_num`, returns the current, unrealised profit of the trade, in the account currency; a loss is negative.
strategy.opentrades_size(trade_num: series int) → series float — For the open trade number `trade_num`, returns the size of the trade.
strategy.order(id: series string, direction: series string, qty?: series float, limit?: series float, stop?: series float, oca_name?: series string, oca_type?: series string, comment?: series string) → void — Places an order without any position logic: a buy adds to the position and a sell subtracts from it, whatever the current position is.
variable strategy.position_avg_price: series float — The average entry price of the current position.
variable strategy.position_size: series float — The size of the current position: positive when long, negative when short, 0 when flat.
constant strategy.short: const string — The short direction, for the `direction` argument of `strategy.entry` and `strategy.order`: sell to open or add to a short position.
variable strategy.wintrades: series int — The number of closed trades that made a profit.

## syminfo

library syminfo — Fourteen properties of the chart's instrument — eight strings, one boolean, two floats and three ints.
variable syminfo.asset_type: simple string — The instrument's asset type.
variable syminfo.currency: simple string — The currency the instrument is quoted in.
variable syminfo.exchange: simple string — The exchange the instrument trades on.
variable syminfo.isindex: simple bool — True when the chart instrument is an index.
variable syminfo.mincontract: simple int — The instrument's minimum contract, as a whole number.
variable syminfo.minmove: simple float — The instrument's tick size, as a float.
variable syminfo.mintick: simple float — The instrument's tick size divided by its price scale: `syminfo.minmove / syminfo.pricescale`.
variable syminfo.pricescale: simple int — The instrument's maximum tick precision, as an int.
variable syminfo.root: simple string — The instrument's root.
variable syminfo.segment: simple string — The segment the instrument belongs to.
variable syminfo.sizescale: simple int — The instrument's size scale, the counterpart of its price scale.
variable syminfo.symbol: simple string — The instrument's symbol, distinct from its ticker.
variable syminfo.ticker: simple string — The chart instrument's ticker.
variable syminfo.timezone: simple string — The instrument's timezone.

## ta

library ta — `ta` is an alias for `talib`.
ta.alma(source: series float, length: series int, offset: series float, sigma: series float) → series float — An Arnaud Legoux moving average of `source` over `length` bars.
ta.atr(length: series int) → series float — Average true range over `length` bars.
ta.barssince(condition: series bool) → series int — Counts the bars that have gone by since `condition` was last true.
ta.bb(source: series float, length: series int, mult: series float) → [series float, series float, series float] — Bollinger bands for `source` over `length` bars, with `mult` setting how far the outer bands sit from the middle one.
ta.bbw(source: series float, length: series int, mult: series float) → series float — Bollinger band width: the same calculation as `talib.bb`, delivered as one number instead of three bands.
ta.cci(source: series float, length: series int) → series float — Commodity Channel Index for `source` over `length` bars.
ta.change(source: series int, length?: series int) → series int — The difference between the current value of `source` and its value `length` bars back.
ta.change(source: series float, length?: series int) → series float — The difference between the current value of `source` and its value `length` bars back.
ta.change(source: series bool, length?: series int) → series bool — The difference between the current value of `source` and its value `length` bars back.
ta.cmo(source: series float, length: series int) → series float — Chande Momentum Oscillator for `source` over `length` bars.
ta.cog(source: series float, length: series int) → series float — Centre of gravity of `source` across a window of `length` bars.
ta.correlation(source1: series float, source2: series float, length: series int) → series float — Correlation between two series, `source1` and `source2`, measured over `length` bars.
ta.cross(source1: series float, source2: series float) → series bool — True on a bar where `source1` and `source2` cross, in either direction.
ta.crossover(source1: series float, source2: series float) → series bool — Flags the bar on which `source1` crosses above `source2`.
ta.crossunder(source1: series float, source2: series float) → series bool — The mirror of `talib.crossover`: true on the bar where `source1` crosses below `source2`.
ta.cum(source: series float) → series float — Accumulates `source` as the script advances through the chart.
ta.dc(length: series int) → [series float, series float, series float] — Donchian channel over `length` bars.
ta.dcw(length: series int) → series float — Donchian channel width over `length` bars, as a single figure.
ta.dev(source: series float, length: series int) → series float — A deviation measure for `source` over `length` bars.
ta.dmi(diLength: series int, adxSmoothing: series int) → [series float, series float, series float] — The directional movement family in one call, calculated from the chart's own bars.
ta.ema(source: series float, length: series int) → series float — Exponential moving average of `source` over `length` bars, weighted so that recent bars count for more than older ones.
ta.falling(source: series float, length: series int) → series bool — Asks the same question as `talib.rising` in the other direction: has `source` been falling across `length` bars?
ta.highest(source: series float, length: series int) → series float — The highest value `source` reached in the last `length` bars.
ta.highestbars(source: series float, length: series int) → series int — Locates the highest value of `source` within the last `length` bars and returns its position rather than its value.
ta.hma(source: series float, length: series int) → series float — Hull moving average of `source` over `length` bars.
ta.kc(source: series float, length: series int, mult: series float, useTrueRange?: series bool) → [series float, series float, series float] — Keltner channels for `source` over `length` bars, with `mult` setting the distance to the outer bands.
ta.kcw(source: series float, length: series int, mult: series float, useTrueRange?: series bool) → series float — Keltner channel width for `source` over `length` bars: one figure in place of the three the channel call returns.
ta.linreg(source: series float, length: series int, offset: series int) → series float — Fits a linear regression to `source` across `length` bars and returns a value from that fit.
ta.lowest(source: series float, length: series int) → series float — The lowest value `source` reached in the last `length` bars.
ta.lowestbars(source: series float, length: series int) → series int — Gives the position of the lowest value of `source` within the last `length` bars, not the value itself.
ta.macd(source: series float, fastlen: series int, slowlen: series int, siglen: series int) → [series float, series float, series float] — Moving average convergence/divergence for `source`, from three lengths: `fastlen`, `slowlen` and `siglen`.
ta.median(source: series float, length: series int) → series float — The middle value of the last `length` values of `source`.
ta.mfi(source: series float, length: series int) → series float — Money Flow Index for `source` over `length` bars.
ta.mode(source: series float, length: series int) → series float — Of the last `length` values of `source`, this reports the one that recurs most often.
ta.nvi() → series float — Negative volume index for the chart's bars.
ta.obv() → series float — On-balance volume for the chart's bars.
ta.percentile_linear_interpolation(source: series float, length: series int, percentile: series float) → series float — The requested `percentile` of `source` over `length` bars, interpolating between the two values that straddle the rank.
ta.percentile_nearest_rank(source: series float, length: series int, percentile: series float) → series float — Takes the requested `percentile` of `source` over `length` bars at the nearest rank, without interpolating.
ta.percentrank(source: series float, length: series int) → series float — Ranks where `source` now stands against the last `length` bars of itself.
ta.pivothigh(source?: series float, leftBars: series int, rightBars: series int) → series float — Looks for a pivot high in `source`, as this build implements it.
ta.pivotlow(source?: series float, leftBars: series int, rightBars: series int) → series float — Looks for a pivot low in `source`, as this build implements it.
ta.psar(start: series float, step: series float, max_step: series float) → series float — Parabolic SAR, controlled by three numbers rather than a bar count: where the calculation starts, how much it moves on each step, and how far it is allowed to go.
ta.pvi() → series float — Positive volume index for the chart's bars, the counterpart of `talib.nvi`.
ta.pvt() → series float — Price-volume trend for the chart's bars.
ta.range(source: series float, length: series int) → series float — How much ground `source` covered over the last `length` bars, expressed as one figure.
ta.rising(source: series float, length: series int) → series bool — Tests whether `source` has been rising across `length` bars.
ta.rma(source: series float, length: series int) → series float — Rolling moving average of `source` over `length` bars.
ta.roc(source: series float, length: series int) → series float — Rate of change of `source` measured across `length` bars.
ta.rsi(source: series float, length: series int) → series float — Relative Strength Index for `source` over `length` bars.
ta.sma(source: series float, length: series int) → series float — Simple moving average of `source` over `length` bars: every bar in the window counts for the same.
ta.stdev(source: series float, length: series int) → series float — Standard deviation of `source` over `length` bars.
ta.stoch(source: series float, high: series float, low: series float, length: series int) → series float — Stochastic reading that places `source` inside the span set by `high` and `low` over `length` bars.
ta.sum(source: series float, length: series int) → series float — Adds up the last `length` values of `source`.
ta.supertrend(multiplier: series float, atrLength: series int) → [series float, series float] — Supertrend from a `multiplier` and an `atrLength`, calculated on the chart's own bars.
ta.swma(source: series float) → series float — Symmetrically weighted moving average of `source` over the last four bars, with the weights 1/6, 2/6, 2/6 and 1/6.
ta.tr(handle_na?: series bool) → series float — True range for the bar the script is on, taken from the chart's own bars.
ta.tsi(source: series float, r: series int, s: series int) → series float — True Strength Index for `source`, smoothed by two lengths, `r` and `s`.
ta.valuewhen(condition: series bool, source: series float, occurrence: simple int) → series float — Reads `source` from the bar on which `condition` was true, going back as far as `occurrence` says.
ta.variance(source: series float, length: series int, biased?: series bool) → series float — Variance of `source` over `length` bars.
ta.vwap(source: series float) → series float — Volume-weighted average price built on `source`.
ta.vwma(source: series float, length: series int) → series float — Volume-weighted moving average of `source` over `length` bars: bars that traded more count for more.
ta.wma(source: series float, length: series int) → series float — Weighted moving average of `source` over `length` bars.
ta.wpr(length: series int) → series float — Williams %R over `length` bars.
ta.wvad(length: series int) → series float — Williams variable accumulation/distribution, calculated on the chart's own bars.

## table

library table — Functions for screen-anchored tables.
type table — A screen-anchored grid (not bar/price anchored).
variable table.all: series array<table> — Array of all currently existing tables, from oldest to newest.
table.all() → series array<table> — Returns the array of all existing table objects (same as the table.all variable).
table.cell(id: series table, column: series int, row: series int, text?: series string, width?: series float, height?: series float, textcolor?: series color, texthalign?: series string, textvalign?: series string, size?: series size, bgcolor?: series color, tooltip?: series string, text_font_family?: input font, text_formatting?: series string) → void — Defines a cell at (column, row).
table.cell_set_bgcolor(id: series table, column: series int, row: series int, color: series color) → void — Sets the background color of an existing cell.
table.cell_set_height(id: series table, column: series int, row: series int, height: series float) → void — Sets the height of an existing cell as a percentage of the pane.
table.cell_set_text(id: series table, column: series int, row: series int, text: series string) → void — Sets the text of an existing cell.
table.cell_set_text_color(id: series table, column: series int, row: series int, color: series color) → void — Sets the text color of an existing cell.
table.cell_set_text_font_family(id: series table, column: series int, row: series int, text_font_family: input font) → void — Sets the font family of an existing cell.
table.cell_set_text_formatting(id: series table, column: series int, row: series int, text_formatting: series string) → void — Sets text formatting of an existing cell (for example none, bold, italic).
table.cell_set_text_halign(id: series table, column: series int, row: series int, texthalign: series string) → void — Sets horizontal text alignment of an existing cell: left, center, or right.
table.cell_set_text_size(id: series table, column: series int, row: series int, size: series size) → void — Sets the text size of an existing cell.
table.cell_set_text_valign(id: series table, column: series int, row: series int, textvalign: series string) → void — Sets vertical text alignment of an existing cell: top, center, or bottom.
table.cell_set_tooltip(id: series table, column: series int, row: series int, tooltip: series string) → void — Sets the tooltip of an existing cell.
table.cell_set_width(id: series table, column: series int, row: series int, width: series float) → void — Sets the width of an existing cell as a percentage of the pane.
table.clear(id: series table, start_column: series int, start_row: series int, end_column: series int, end_row: series int) → void — Removes cells in the inclusive rectangle.
table.delete(id: series table) → void — Deletes a table.
table.merge_cells(id: series table, start_column: series int, start_row: series int, end_column: series int, end_row: series int) → void — Merges the inclusive rectangle from (start_column, start_row) to (end_column, end_row) into the top-left origin cell.
table.new(position: series string, columns: series int, rows: series int, bgcolor?: series color, frame_color?: series color, frame_width?: series int, border_color?: series color, border_width?: series int, force_overlay?: const bool) → series table — Creates a new table at a chart position.
table.set_bgcolor(id: series table, color: series color) → void — Sets the table background color.
table.set_border_color(id: series table, color: series color) → void — Sets the inner cell-border color.
table.set_border_width(id: series table, width: series int) → void — Sets the inner cell-border width in pixels.
table.set_frame_color(id: series table, color: series color) → void — Sets the outer frame color.
table.set_frame_width(id: series table, width: series int) → void — Sets the outer frame width in pixels.
table.set_position(id: series table, position: series string) → void — Moves a table to a new position.

## talib

library talib — Sixty-two named indicator and series functions: moving averages, oscillators, channels, ranges, pivots, window statistics and the volume indices.
talib.alma(source: series float, length: series int, offset: series float, sigma: series float) → series float — An Arnaud Legoux moving average of `source` over `length` bars.
talib.atr(length: series int) → series float — Average true range over `length` bars.
talib.barssince(condition: series bool) → series int — Counts the bars that have gone by since `condition` was last true.
talib.bb(source: series float, length: series int, mult: series float) → [series float, series float, series float] — Bollinger bands for `source` over `length` bars, with `mult` setting how far the outer bands sit from the middle one.
talib.bbw(source: series float, length: series int, mult: series float) → series float — Bollinger band width: the same calculation as `talib.bb`, delivered as one number instead of three bands.
talib.cci(source: series float, length: series int) → series float — Commodity Channel Index for `source` over `length` bars.
talib.change(source: series int, length?: series int) → series int — The difference between the current value of `source` and its value `length` bars back.
talib.change(source: series float, length?: series int) → series float — The difference between the current value of `source` and its value `length` bars back.
talib.change(source: series bool, length?: series int) → series bool — The difference between the current value of `source` and its value `length` bars back.
talib.cmo(source: series float, length: series int) → series float — Chande Momentum Oscillator for `source` over `length` bars.
talib.cog(source: series float, length: series int) → series float — Centre of gravity of `source` across a window of `length` bars.
talib.correlation(source1: series float, source2: series float, length: series int) → series float — Correlation between two series, `source1` and `source2`, measured over `length` bars.
talib.cross(source1: series float, source2: series float) → series bool — True on a bar where `source1` and `source2` cross, in either direction.
talib.crossover(source1: series float, source2: series float) → series bool — Flags the bar on which `source1` crosses above `source2`.
talib.crossunder(source1: series float, source2: series float) → series bool — The mirror of `talib.crossover`: true on the bar where `source1` crosses below `source2`.
talib.cum(source: series float) → series float — Accumulates `source` as the script advances through the chart.
talib.dc(length: series int) → [series float, series float, series float] — Donchian channel over `length` bars.
talib.dcw(length: series int) → series float — Donchian channel width over `length` bars, as a single figure.
talib.dev(source: series float, length: series int) → series float — A deviation measure for `source` over `length` bars.
talib.dmi(diLength: series int, adxSmoothing: series int) → [series float, series float, series float] — The directional movement family in one call, calculated from the chart's own bars.
talib.ema(source: series float, length: series int) → series float — Exponential moving average of `source` over `length` bars, weighted so that recent bars count for more than older ones.
talib.falling(source: series float, length: series int) → series bool — Asks the same question as `talib.rising` in the other direction: has `source` been falling across `length` bars?
talib.highest(source: series float, length: series int) → series float — The highest value `source` reached in the last `length` bars.
talib.highestbars(source: series float, length: series int) → series int — Locates the highest value of `source` within the last `length` bars and returns its position rather than its value.
talib.hma(source: series float, length: series int) → series float — Hull moving average of `source` over `length` bars.
talib.kc(source: series float, length: series int, mult: series float, useTrueRange?: series bool) → [series float, series float, series float] — Keltner channels for `source` over `length` bars, with `mult` setting the distance to the outer bands.
talib.kcw(source: series float, length: series int, mult: series float, useTrueRange?: series bool) → series float — Keltner channel width for `source` over `length` bars: one figure in place of the three the channel call returns.
talib.linreg(source: series float, length: series int, offset: series int) → series float — Fits a linear regression to `source` across `length` bars and returns a value from that fit.
talib.lowest(source: series float, length: series int) → series float — The lowest value `source` reached in the last `length` bars.
talib.lowestbars(source: series float, length: series int) → series int — Gives the position of the lowest value of `source` within the last `length` bars, not the value itself.
talib.macd(source: series float, fastlen: series int, slowlen: series int, siglen: series int) → [series float, series float, series float] — Moving average convergence/divergence for `source`, from three lengths: `fastlen`, `slowlen` and `siglen`.
talib.median(source: series float, length: series int) → series float — The middle value of the last `length` values of `source`.
talib.mfi(source: series float, length: series int) → series float — Money Flow Index for `source` over `length` bars.
talib.mode(source: series float, length: series int) → series float — Of the last `length` values of `source`, this reports the one that recurs most often.
talib.nvi() → series float — Negative volume index for the chart's bars.
talib.obv() → series float — On-balance volume for the chart's bars.
talib.percentile_linear_interpolation(source: series float, length: series int, percentile: series float) → series float — The requested `percentile` of `source` over `length` bars, interpolating between the two values that straddle the rank.
talib.percentile_nearest_rank(source: series float, length: series int, percentile: series float) → series float — Takes the requested `percentile` of `source` over `length` bars at the nearest rank, without interpolating.
talib.percentrank(source: series float, length: series int) → series float — Ranks where `source` now stands against the last `length` bars of itself.
talib.pivothigh(source?: series float, leftBars: series int, rightBars: series int) → series float — Looks for a pivot high in `source`, as this build implements it.
talib.pivotlow(source?: series float, leftBars: series int, rightBars: series int) → series float — Looks for a pivot low in `source`, as this build implements it.
talib.psar(start: series float, step: series float, max_step: series float) → series float — Parabolic SAR, controlled by three numbers rather than a bar count: where the calculation starts, how much it moves on each step, and how far it is allowed to go.
talib.pvi() → series float — Positive volume index for the chart's bars, the counterpart of `talib.nvi`.
talib.pvt() → series float — Price-volume trend for the chart's bars.
talib.range(source: series float, length: series int) → series float — How much ground `source` covered over the last `length` bars, expressed as one figure.
talib.rising(source: series float, length: series int) → series bool — Tests whether `source` has been rising across `length` bars.
talib.rma(source: series float, length: series int) → series float — Rolling moving average of `source` over `length` bars.
talib.roc(source: series float, length: series int) → series float — Rate of change of `source` measured across `length` bars.
talib.rsi(source: series float, length: series int) → series float — Relative Strength Index for `source` over `length` bars.
talib.sma(source: series float, length: series int) → series float — Simple moving average of `source` over `length` bars: every bar in the window counts for the same.
talib.stdev(source: series float, length: series int) → series float — Standard deviation of `source` over `length` bars.
talib.stoch(source: series float, high: series float, low: series float, length: series int) → series float — Stochastic reading that places `source` inside the span set by `high` and `low` over `length` bars.
talib.sum(source: series float, length: series int) → series float — Adds up the last `length` values of `source`.
talib.supertrend(multiplier: series float, atrLength: series int) → [series float, series float] — Supertrend from a `multiplier` and an `atrLength`, calculated on the chart's own bars.
talib.swma(source: series float) → series float — Symmetrically weighted moving average of `source` over the last four bars, with the weights 1/6, 2/6, 2/6 and 1/6.
talib.tr(handle_na?: series bool) → series float — True range for the bar the script is on, taken from the chart's own bars.
talib.tsi(source: series float, r: series int, s: series int) → series float — True Strength Index for `source`, smoothed by two lengths, `r` and `s`.
talib.valuewhen(condition: series bool, source: series float, occurrence: simple int) → series float — Reads `source` from the bar on which `condition` was true, going back as far as `occurrence` says.
talib.variance(source: series float, length: series int, biased?: series bool) → series float — Variance of `source` over `length` bars.
talib.vwap(source: series float) → series float — Volume-weighted average price built on `source`.
talib.vwma(source: series float, length: series int) → series float — Volume-weighted moving average of `source` over `length` bars: bars that traded more count for more.
talib.wma(source: series float, length: series int) → series float — Weighted moving average of `source` over `length` bars.
talib.wpr(length: series int) → series float — Williams %R over `length` bars.
talib.wvad(length: series int) → series float — Williams variable accumulation/distribution, calculated on the chart's own bars.

## text

library text — Named constants for text alignment (`text.align_*`) and formatting (`text.format_*`) used by label, box, and table.
constant text.align_bottom: const string — Vertical text alignment constant that aligns text to the bottom of the container.
constant text.align_center: const string — Text alignment constant that centers text horizontally or vertically in the container.
constant text.align_left: const string — Horizontal text alignment constant that aligns text to the left of the container.
constant text.align_right: const string — Horizontal text alignment constant that aligns text to the right of the container.
constant text.align_top: const string — Vertical text alignment constant that aligns text to the top of the container.
constant text.format_bold: const string — Text formatting constant that renders text in bold.
constant text.format_italic: const string — Text formatting constant that renders text in italic.
constant text.format_none: const string — Text formatting constant that applies no special formatting.

## xloc

library xloc — Named constants for how drawing x-coordinates are interpreted: bar index or UNIX time.
constant xloc.bar_index: const string — X-coordinate is a bar index.
constant xloc.bar_time: const string — X-coordinate is a UNIX timestamp in milliseconds.

## yloc

library yloc — Named constants for how label y-coordinates are interpreted: price, above the bar, or below the bar.
constant yloc.abovebar: const string — Vertical text alignment constant that places a label above the bar.
constant yloc.belowbar: const string — Vertical text alignment constant that places a label below the bar.
constant yloc.price: const string — Vertical location constant that places a label at a specific price level.
