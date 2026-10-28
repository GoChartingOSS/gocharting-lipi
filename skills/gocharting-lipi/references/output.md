# How to answer with a script

Give the script in one fenced code block, starting with these lines, in this order, exactly (this is what GoCharting's hosted service delivers):

1. `//@lipi=2`
2. Converting only: every licence, copyright or author line from the top of the user's source, unchanged (a line in another comment style
   becomes a `//` comment). Leave this out when there is none, and always when creating.
3. `// AI converter v0.5`
4. The banner, as a `//` comment:
   - converting: `// Converted automatically by AI from code you supplied. It may behave differently. Review and test before use. Not financial advice.`
   - creating: `// Created automatically by AI from your description. It may not do what you described. Review and test before use. Not financial advice.`
5. The script.

After the code block:

- The lists the workflow names (leave out an empty one).
- This reminder, as written: converting: *Compiling is not proof it behaves like your original. Test it on the chart before trading on it.* creating: *Compiling is not proof it does what you described. Test it on the chart before trading on it.*
- Then: "Paste it into the GoCharting script editor. If it reports an error, paste the error here and I will fix it."
