# Self-check, before every script answer

The hosted service checks every script with GoCharting's compiler and also fixes some layout in code. You have neither, so check these yourself.

## Against the reference

- Every function, variable, type, constant and keyword you used is in `references/lang/index.md`, spelled exactly; nothing is invented.
- Every call passes the arguments its signature requires, in order, with the right types and qualifiers (`const`, `input`, `simple`, `series`).
- Every opening brace has its closing brace, including the last block at the end of the script.
- Calls that must be at the global scope (the plot family, `hline`, `fill`, `bgcolor`, `barcolor`, `alertcondition`) are not inside a block or a function.
- Every declared type matches the value assigned to it; a variable first set to `na` has an explicit type.
- Colour opacity runs from 0 (invisible) to 1 (solid).

## Layout the hosted service fixes in code (you must write it this way)

- Line 1 is exactly `//@lipi=2`, and it appears once.
- One statement per line: no `;` between statements, and the `{` and `}` of a block are not on one line with the statements inside it.
- The header lines of `references/output.md` appear exactly once.

## About your answer

- Do not say the script compiles, works or was tested. Say it is ready to paste into the GoCharting editor.
- The lists after the script name only behaviour, in plain words for a trader; no function names and no name mapping.
