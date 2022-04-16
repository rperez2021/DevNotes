---
id: semzjhvlz30vhbvhva7750a
title: ASI
desc: 'Automatic Semicolon Insertion'
updated: 1650087801369
created: 1650087511620
---

- empty statement
- `var` statement
- expression statement
- `do-while` statement
- `continue` statement
- `break` statement
- `return` statement
- `throw` statement

1. When an offending token is encountered that is not allowed by the grammar, a semicolon is inserted before it if:
    - The token is separated from the previous token by at least one LineTerminator.
    - The token is `}`
2. When the end of the input stream of tokens is encountered and the parser is unable to parse the input token stream as a single complete Program, then a semicolon is automatically inserted at the end of the input stream.
3. This case occurs when a token is allowed by some production of the grammar, but the production is a restricted production, a semicolon is automatically inserted before the restricted token.
