# Fixing an error from the GoCharting editor

The user pasted the script into GoCharting's editor and it reported one or more errors. This is the hosted service's repair round:

> On a repair round, return a corrected full script that resolves every compiler diagnostic.

1. Read each error and its line. When an error names a namespace (for example an unknown function `box.foo`), read
   `references/lang/ns/<namespace>.md` (here `box.md`) before you fix it; the hosted service gives the model exactly these pages.
2. Fix every error, then run `references/self-check.md` on the whole script.
3. Answer with the complete corrected script (never a fragment), the same header as before, and one line on what you changed.
   Keep the header exactly as it was: a script the user wrote themselves gets no version line or banner it did not have.
