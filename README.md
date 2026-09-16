APON (Agentic Programming Object Notation) is a purely functional, lazily evaluated, and dynamically typed language. It was created with AI agent coding in mind, allowing agents to write precise, declarative responses that can configure outside systems or execute commands.

Unlike general-purpose programming languages, APON is designed entirely around data flow and reproducibility. At its core is JSON, which AI agents are already used to, but it adds features inspired by other declarative and functional languages.

- Purely Functional: Everything in APON is an expression, and values are completely immutable. Functions always produce the exact same output given the same inputs. 
- Declarative: You don't write sequential steps (e.g., "do this, then do that"). Instead, you describe the desired final state of a response.
- Lazy Evaluation: APON will not compute an expression until its value is strictly needed. This makes responses highly efficient. 
- Reproducible: Because dependencies are tracked explicitly through data, building an APON expression will result in the exact same byte-for-byte output regardless of the machine running it.

APON is a superset of JSON, so all valid JSON is valid APON.

APON syntax is heavily inspired by functional languages like Nix. It treats functions as first-class citizens and relies heavily on key-value collections. 

- Primitives: Supports integers, floats, booleans, strings, and nulls. 
- Arrays: Written with square brackets and separated by commas. `[1, 2, 3]`
- Objects: These are key-value dictionaries, written with curly braces.

Example:

```apon
{
  "status": "success",
  "data": {
    "id": 1234,
    "sentiment": "positive",
    "confidence_score": 0.96,
    "summary": "The user is highly satisfied with the new update, specifically praising the faster loading speeds and sleek UI overhaul.",
    "key_phrases": [
      "faster loading speeds",
      "sleek UI overhaul",
      "absolute game-changer"
    ],
    "locked": false,
    "parent": null
  }
}
```

Unlike in JSON, trailing commas are allowed for any expression that is sequenced with commas such as objects, arrays, etc.

Variables can be declared with the pattern `let nane = value in`. Multiple variables can be declared at once seperated by commas. 

```apon
let a = 1, b = 2 in
{
  "a": a,
  "b": b,
}
```

The key of an object can be an expression if enclosed in square brackets. The expression must evaluate to a string.

```apon
let key = "message" in
{
  [key]: "This is the message."
}
```

Functions are declared using vertical bar notation. They can be declared in any expression that expects a function type. Like true lambda functions, it can only have one expression which is its return value. 

```apon
let addOne = |x| x + 1 in
{
  "answer": addOne(1)
}
```

Basic operators found in most other programmming languages are available: `+ - * / ! == != > < >= <= && || & | ^ ~`.

APON also has keyword expressions for boolean logic and pattern matching.

`if then else`

```apon
let
  status = 404,
in
  if status == 200 then
    "Success"
  else if status == 404 then
    "Not Found"
  else if status == 500 then
    "Internal Server Error"
  else
    "Unknown Status"
```

`match case then`

```apon
|n|
  match n
  case 1 then "One!"
  case 2 then "Two!"
  case 3 then "Three!"
  case _ then "Something else!"
```

Types are declared using the keyword `type` followed by a type expression. Values can be asserted to be a certain type using the keyword `as`. 

```apon
let
  User = type {
    "id": number,
    "name": string,
    "role": "admin" | "user",
    "email"?: string,
  },
in
{
  "id": 1,
  "name": "Alice",
  "role": "admin",
} as User
```

Types are normally inferred, but they can be explicitly declared for `let` variables and function parameters with a colon after the name. 

```apon
let
  a: number = 1,
  addOne: number -> number = |x| x + 1,
in
{ "answer": addOne(a) }
```

This is a rough outline of the language so far. Feedback is welcomed: either through the [issues](https://github.com/lemlac/apon/issues) page or contact me directly via [email](mailto:13686726+lemlac@users.noreply.github.com).
