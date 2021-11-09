# Dynamic language with first class tagged unions?

I can imagine convinient syntax for tagged unions in TypeScript-like language which would be really useful, take this hypothethical example:

```typescript
function withInferredTaggedUnion(): ReturnType {
    if (hasPets) {
        return User {
            id: "123e4567-e89b-12d3-a456-426614174000" UUID,
            age: 25 Years,
            height: 170 Cm,
            pets: Pets ["Jimmy", "Duffy"]
        }
    } else if (oldEnough) {
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
            id: string UUID,
            age: number Years,
            height: number Cm,
            pets?: Pets string[]
        }
    | ValidationError { age: string }

```

In example above the user defined tags are: `UUID`, `User`, `ValidationError`, `Years` and `Cm`. They need not be predefined in dynamic language, but are attached on the values e.g. strings, objects, numbers or arrays. It's notable that these tags are _not_ constructors of anykind, they are just name tags used in pattern matching etc.

Some rules are in order, e.g. with numbers or strings the tag is suffix, e.g. `5 Years` or `"123e4567-e89b-12d3-a456-426614174000" UUID` but with arrays or objects they are prefixes `User {}` or `Pets ["Jimmy", "Duffy"]`.

First class support for tags would allow obvious way to define errors and edge cases in dynamic languages. Pattern matching, and thus handling and catching error cases, on the tags would be easy.
