# Reason Projects Ideas

This repo lists some of the stuff I personally find very compelled to build. Unfortunately I'm limited by time and energy (and skills, tbh), so I'm making this list in case anyone find these interesting.

Feel free to contribute!

### Ppx macro that turns any function into a CLI command
Reason (OCaml)'s function has all the features we want in a terminal tool's interface:
- labelled arguments (which turn into CLI flags) with optional renaming (flag shortcut)
- types, which turn `list string` into a CLI flag that accepts... a list of strings
- optional arguments, with/without default value.
- Doc block comments, to explain each parameter

As a bonus, we get free manpage and shell autocomplete!

### Inline [power assert](https://github.com/power-assert-js/power-assert)
Sometimes I don't really want full-blown unit tests. In addition to the guarantees the type system provides, I'd like to tackle on a few example use-cases for a function. Heck, some do this already in the form of comments. Jane Street's [Core_kernel](https://github.com/janestreet/core_kernel/blob/master/src/core_array.ml#L302) already does the inline part (not executed in production, naturally); I'd like that, but with power assert's crazy good-looking output.

Examples are great. We'd also be able to extract these tests and display them in the API docs.

### API search by giving example input & output
*See: http://www.wilfred.me.uk/blog/2016/07/30/example-driven-development*. Another one, built on top of types, would be Haskell's [Hoogle](https://www.haskell.org/hoogle/) and OCaml's very own [OCamlScope](https://github.com/camlspotter/ocamloscope).

Given `"hello"`, what's the function that'll give me the output `"Hello"`? (`String.capitalize`).

Naively, we'd iterate through all the functions in our database and execute each. This is expensive; a few optimizations:
- filter by input and output type. This will reduce the search space by a huge amount
- cache computation
- restrict the input to a few values per type, e.g. "hello", "hi world", "" for strings
- restrict the functions to a set of popular ones

Furthermore, If the user provides `["hello", "world"]` as input and "hello world" as output, we'd filter down to `String.concat` and `outputHelloWorld` (random custom function), then allow the user to further filter down by another argument (e.g. `" "`, in order to get to `String.concat` here).

### `Obj.magic` to bypass the type checker temporarily
Type `Obj.magic` type acts like an `any` type. We can have a special mode that annotates all of the values of a file as `Obj.magic`, and iterate like a dynamic language.

### Check in the AST
Reason gets this closer than most languages. Check in the AST, diff using the AST, and reify the AST into a concrete syntax using the built-in `refmt`. No more syntax debates in the future: your visual preference stays local. Heck, nobody checks in their editor theme and mandates the whole team to use it, right?

For those who want a pure AST editor, this is the transition step toward that idea.

### Browser extension to toggle between syntaxes
Similar to the idea above, but easier to achieve: we could use `refmt`, compiled to JS, to parse OCaml syntax in an online code snippet and turn it into Reason syntax, and vice-versa.

### [GraphQL type system](http://graphql.org/docs/typesystem/), using actual types
GraphQL schemas are built like [this](http://graphql.org/blog/#building-the-graphql-schema). With ppx and OCaml's type system, we can generate the introspection tools through `type myShape = {foo: int}` rather than through an informal, hand-rolled type system a-la `let myShape = graphQLSchema ({field: "foo", type: "int"})`.

### Add yours here!
