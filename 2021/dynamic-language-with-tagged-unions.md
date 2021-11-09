# Dynamic language with first class tagged unions?

I can imagine convinient syntax for tagged unions in TypeScript-like language which would be really useful, take this hypothethical example:

```typescript
function withInferredTaggedUnion(): ReturnType {
    if (hasPets) {
        return User {
            age: 25 Years,
            height: 170 Cm,
            pets: Pets ["Jimmy", "Duffy"]
        }
    } else {
        return User {
            age: 25 Years,
            height: 170 Cm
        }
    }
    return ValidationError { age: "Not old enough!" }
}

// Type of the above function could be inferred as:
type ReturnType =
    | User {
            age: Years,
            height: Cm,
            pets?: Pets string[]
        }
    | ValidationError { age: string }

```

This kind of first class support would allow obvious way to define errors and edge cases in dynamic languages. Pattern matching, and thus handling and catching error cases, on the tags would be easy.
