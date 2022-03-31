# Learn Nushell

#### Survival kit

Help:

    > help
    > help commands
    > help <command name>

Types

    > echo 3
    int
    > echo 3.14 | describe
    float

### Literals

Basically, you need to quote string literals only when you need to avoid the
interpretation as another type, so that most strings can be typed "fast" (this
is for a large what makes a programming language a shell langage IMHO!). 
(You *can* always quote strings, you just don't need to). So for example:

    > echo "Hello!" | describe
    string
    > echo Hello! | describe
    string
    > echo 1 | describe
    int
    > echo "1" | describe
    string



### Types

(explore with `describe`).

Atomic types (`bool`, `int`, `float` `string`, etc.) work pretty much as you expect
in this regard.

    > true | describe
    bool
    > 1 | describe
    int
    > 3.14 | describe
    float
    > "Hello!" | describe
    string

Or equivalently

    > [true, 1, 3.14, "Hello!"] | each { |it| $it | describe}
    ╭───┬────────╮
    │ 0 │ bool   │
    │ 1 │ int    │
    │ 2 │ float  │
    │ 3 │ string │
    ╰───┴────────╯

**TODO:**

  - dates

  - duration

  - filesizes

  - ranges



Records are first class nice and parametrized wrt the types of their attributes:

    > {status: true, code: 42}
    ╭────────┬──────╮
    │ status │ true │
    │ code   │ 42   │
    ╰────────┴──────╯
    > {status: true, code: 42} | describe
    record<status: bool, code: int>

Lists are "funky" ; they are heterogeneous / untyped:

    > [1 2 3] | describe
    list<unknown>
    > [true 1 Hello!]


Tables are actually lists:

    > [[a b]; [1 2] [3 4]]
    ╭───┬───┬───╮
    │ # │ a │ b │
    ├───┼───┼───┤
    │ 0 │ 1 │ 2 │
    │ 1 │ 3 │ 4 │
    ╰───┴───┴───╯
    > [[a b]; [1 2] [3 4]] | describe
    list<unknown>

"Classic" lists are actually the same thing as 1d tables with the empty string 
as a column name:

    > [1 2 3]
    ╭───┬───╮
    │ 0 │ 1 │
    │ 1 │ 2 │
    │ 2 │ 3 │
    ╰───┴───╯
    > [[""]; [1] [2] [3]]
    ╭───┬───╮
    │ 0 │ 1 │
    │ 1 │ 2 │
    │ 2 │ 3 │
    ╰───┴───╯

### ⚠️ Spaces matter

Consider

    > 1 + 1
    2

But

    > 1+1
    1+1

Consider

    > let x = 1

    > let x=1
    Error: nu::parser::missing_positional (link)

    × Missing required positional argument.
    ╭─[entry #33:1:1]
    1 │ let x=1
    ·        ▲
    ·        ╰── missing initial_value
    ╰────
    help: Usage: let <var_name> = <initial_value>

### Identifiers

What are the valid identifiers? Apparently we can have some pretty wild 
identifiers with symbols in them:

    > let x= = 1
    > echo $x=
    1
