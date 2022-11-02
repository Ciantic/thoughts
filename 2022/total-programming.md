# Total Programming separate from Functional Programming

I've noticed that people praise functional programming paradigm because of total programming features, and rarely because of functional programming features. These are not mutually exclusive as total programming has no strict defintion. However I find this separation very useful.

Total programming avoids partial functions and favor total functions. Partial functions can throw unexpected errors, loop infinitely and unless they are handled it might terminate whole program or it gets stuck. To avoid these languages have tools such as checking nullness and errors, exhaustively matching all branches, avoiding infinitely running programs... This form of total programming gives good guarantees for correctness and avoiding errors, reason it's usually praised.

Total programming uses types such as: Option, Maybe, NonEmpty, Result, Either. I've listed a few from Haskell and Rust. However these are just total programming tools, they are not describing functional programming. To use them effectively though, you need some aspects of functional programming.

What is then functional programming? I'm not expert enough to give you full definition, but I was going through Haskell courses in my university and the teacher didn't think Rust was particularily good functional language as it didn't emphasise on function composition like Haskell does. However Rust does have good total programming tools.

It stuck me, and I mentally keep these separate. When you talk about writing correct code and use types that help you build exhaustively checked programs: Option, Either, NonEmpty, Result, etc. it's total programming you are talking about. When you talk about composing functions from other functions you are talking about functional programming.
