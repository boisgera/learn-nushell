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

There is a missing data type, whose single instance is accessible via the
special variable named `nothing`. 

    > $nothing
    > $nothing | describe
    nothing

But `nothing` itself is not a literal:

    > nothing
    Error: nu::shell::external_command (link)

    × External command
    ╭─[entry #1:1:1]
    1 │ nothing
    · ───┬───
    ·    ╰── can't run executable
    ╰────
    help: No such file or directory (os error 2)


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

    > [true, 1, 3.14, "Hello!"] | each {|it| $it | describe}
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

So, yes, tables are lists of stuff of unknown type are are not say, 
lists of records of a known type, so not *really* a dataframe: in a given
column you can have different types for example:

    > [[a b]; [1 true] [3.1 "Hello!"]]
    ╭───┬──────┬────────╮
    │ # │  a   │   b    │
    ├───┼──────┼────────┤
    │ 0 │    1 │ true   │
    │ 1 │ 3.10 │ Hello! │
    ╰───┴──────┴────────╯

You get the record (and its type) only when you effectively get the data from
the table:

    > [[a b]; [1 true] [3.1 "Hello!"]] | get 0
    ╭───┬──────╮
    │ a │ 1    │
    │ b │ true │
    ╰───┴──────╯
    > [[a b]; [1 true] [3.1 "Hello!"]] | get 0 | describe
    record<a: int, b: bool>

So a table is a list of records; if the type of the record values are not
consistent this is not a problem and if the key do not correspond, this
is simply treated as missing data (type `nothing`):

    > [{a: 1, b:2}, {a: 1, b: 7}]               03/31/2022 10:59:34 AM
    ╭───┬───┬───╮
    │ # │ a │ b │
    ├───┼───┼───┤
    │ 0 │ 1 │ 2 │
    │ 1 │ 1 │ 7 │
    ╰───┴───┴───╯
    > [{a: 1, b:2}, {a: 1, b: 7, c:6}]          03/31/2022 11:01:54 AM
    ╭───┬───┬───┬────╮
    │ # │ a │ b │ c  │
    ├───┼───┼───┼────┤
    │ 0 │ 1 │ 2 │ ❎ │
    │ 1 │ 1 │ 7 │  6 │
    ╰───┴───┴───┴────╯

Note that

    > [{a: 1, b:2}, {a: 1, b: 7, c:6}] | get c.1
    6
    > [{a: 1, b:2}, {a: 1, b: 7, c:6}] | get c.0
    > [{a: 1, b:2}, {a: 1, b: 7, c:6}] | get c.0 | describe
    nothing


If you don't have this structure (one of the list elements is not a record),
then the stuff is not displayed as a table but as a list:

    > [{a: 1, b:2}, {a: 1, b: 7, c:6}, [7]]
    ╭───┬───────────────────╮
    │ 0 │ {record 2 fields} │
    │ 1 │ {record 3 fields} │
    │ 2 │ [list 1 item]     │
    ╰───┴───────────────────╯

So tables are not a first-class citizen: they are a kind of list that happen
to match a minimal structure.

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
