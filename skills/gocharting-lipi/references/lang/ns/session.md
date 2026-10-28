# session

## session (library)

Two values about the session the current bar falls in: its date, and whether this is the session's first bar.

Both are series, so unlike the interval values they change as the script moves through bars.

### example

```lipi
//@lipi=2
indicator("session Library Example", overlay=true)
// Mark the first bar of every session
bgcolor(session.isfirst ? color.new(color.blue, 0.3) : na)
```

### id

library:session

## session.date (variable)

The date of the session the current bar falls in.

Session values are series, not simple: this one changes as your script moves through bars.

### type

series string

### example

```lipi
//@lipi=2
indicator("Session-based CVD (Fixed)", overlay=false)
// Persistent variable
static customCVD = 0
isNewSession = session.date != session.date[1]
// Reset on new session, accumulate otherwise
customCVD := isNewSession ? 0 : customCVD + orderflow.delta
plot(customCVD, title="Session CVD", style=plotStyle.line, color=color.orange)
```

### id

variable:session.date

## session.isfirst (variable)

True on the first bar of a session.

This is the flag to reach for when something has to reset once per session. The cumulative delta function reads it for exactly that purpose, seeding its running total from zero rather than carrying the previous bar's total forward.

### type

series bool

### example

```lipi
//@lipi=2
indicator("CVD with session.first", overlay=false)
// Initialize persistent variable
static customCVD = 0
// Check if it's the first candle of the session
if session.isfirst {
    customCVD := 0
} else  {
    customCVD := customCVD + orderflow.delta
}
plot(customCVD, title="Session CVD", color=color.blue)
```

### id

variable:session.isfirst
