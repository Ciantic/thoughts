# Network API's need tagged unions

This is evolving thought. I really like a form of total programming, where each error is catched and handled.

I have been frustrated with many of the API schema languages. Such as GraphQL and gRPC which don't seem to have convinient support for tagged unions.

Almost all network API's have error type or few per each end point. Tagged unions if they can be easily defined, are effortless to use, so much so that almost _all_ end points should have tagged union as a return type.

For instance Haskell, F# and Rust all get this right, because they have convinient way to define tagged unions. Other ways I've seen seems to be too hard, or worse, have multiple and incompatible ways to define tagged unions.

Languages and schemas are closely related, so I ask, where are the schema languages which emphasises on tagged unions as return types?
