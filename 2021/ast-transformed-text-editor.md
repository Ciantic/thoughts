# AST transformed text editor

Idea is quiet simple. For instance you could edit JSX directly in JS file, if just the editor had support to transform between two AST's, and then format it nicely.

E.g. You open JS file, it transforms it to JSX, reformats it as a text. The rule required is that you cannot save the file unless it's valid AST as it needs to be transformed back to JS.

This would allow cool other experiments. Like having C# transformed to F#-like AST, and let the saving do the trick for converting it back to C#. Notably, F# is way more than syntax, but you could remove parentheses etc.

It would allow pretty fast experiments in an well established language, e.g. I'd like to see C#'s if-statements to be experessions which can be assignable to a variable. Like it's possible in Rust.

I wonder how easy this would be to implement in VSCode so that it would also keep the auto-completion and other Language Server features somewhat functional.
