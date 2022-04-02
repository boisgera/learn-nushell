# Getting Started

Start Nushell:

    $ nu

Try some classic shell commands and see what happens

    〉git clone git@github.com:nushell/nushell.git
    Cloning into 'nushell'...
    remote: Enumerating objects: 60879, done.
    remote: Counting objects: 100% (3003/3003), done.
    remote: Compressing objects: 100% (1031/1031), done.
    remote: Total 60879 (delta 2070), reused 2457 (delta 1938), pack-reused 57876
    Receiving objects: 100% (60879/60879), 26.02 MiB | 6.68 MiB/s, done.
    Resolving deltas: 100% (42034/42034), done.
    〉ls
    ╭───┬─────────┬──────┬─────────┬──────────╮
    │ # │  name   │ type │  size   │ modified │
    ├───┼─────────┼──────┼─────────┼──────────┤
    │ 0 │ nushell │ dir  │ 4.0 KiB │ now      │
    ╰───┴─────────┴──────┴─────────┴──────────╯
    〉cd nushell 
    nushell〉ls
    ╭────┬───────────────────────┬──────┬───────────┬──────────╮
    │ #  │         name          │ type │   size    │ modified │
    ├────┼───────────────────────┼──────┼───────────┼──────────┤
    │  0 │ CODE_OF_CONDUCT.md    │ file │   3.4 KiB │ now      │
    │  1 │ CONTRIBUTING.md       │ file │   1.7 KiB │ now      │
    │  2 │ Cargo.lock            │ file │ 116.8 KiB │ now      │
    │  3 │ Cargo.toml            │ file │   3.1 KiB │ now      │
    │  4 │ LICENSE               │ file │   1.1 KiB │ now      │
    │  5 │ Makefile.toml         │ file │     449 B │ now      │
    │  6 │ README.build.txt      │ file │     192 B │ now      │
    │  7 │ README.md             │ file │  15.3 KiB │ now      │
    │  8 │ assets                │ dir  │   4.0 KiB │ now      │
    │  9 │ build-all-maclin.sh   │ file │     564 B │ now      │
    │ 10 │ build-all-windows.cmd │ file │     655 B │ now      │
    │ 11 │ build-all.nu          │ file │     576 B │ now      │
    │ 12 │ build.rs              │ file │     127 B │ now      │
    │ 13 │ crates                │ dir  │   4.0 KiB │ now      │
    │ 14 │ docs                  │ dir  │   4.0 KiB │ now      │
    │ 15 │ images                │ dir  │   4.0 KiB │ now      │
    │ 16 │ install-all.ps1       │ file │     921 B │ now      │
    │ 17 │ install-all.sh        │ file │     818 B │ now      │
    │ 18 │ pkg_mgrs              │ dir  │   4.0 KiB │ now      │
    │ 19 │ rustfmt.toml          │ file │      16 B │ now      │
    │ 20 │ samples               │ dir  │   4.0 KiB │ now      │
    │ 21 │ src                   │ dir  │   4.0 KiB │ now      │
    │ 22 │ tests                 │ dir  │   4.0 KiB │ now      │
    │ 23 │ uninstall-all.sh      │ file │     374 B │ now      │
    │ 24 │ wix                   │ dir  │   4.0 KiB │ now      │
    ╰────┴───────────────────────┴──────┴───────────┴──────────╯
    nushell〉cat LICENSE
    MIT License

    Copyright (c) 2019 - 2021 The Nushell Project Developers

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.


You can see the `git` command behaves as usual, 
but that the output of `ls` displays a table, and that's unusual!
Nushell actually provides its own `ls` command, and that's what you have been
using. It is similar, but not identical, to the POSIX `ls` command that you are 
familiar with. To see what this nushell command can do, 
use `ls --help` or `help ls`:

    〉ls --help
    List the files in a directory.

    Usage:
    > ls {flags} (pattern) 

    Flags:
    -h, --help
        Display this help message
    -a, --all
        Show hidden files
    -l, --long
        List all available columns for each entry
    -s, --short-names
        Only print the file names and not the path
    -f, --full-paths
        display paths as absolute paths
    -d, --du
        Display the apparent directory size in place of the directory metadata size

    Parameters:
    (optional) pattern: the glob pattern to use

    Examples:
    List all files in the current directory
    > ls

    List all files in a subdirectory
    > ls subdir

    List all rust files
    > ls *.rs

    List all files and directories whose name do not contain 'bar'
    > ls -s | where name !~ bar

    List all dirs with full path name in your home directory
    > ls -f ~ | where type == dir

    List all dirs in your home directory which have not been modified in 7 days
    > ls -s ~ | where type == dir && modified < ((date now) - 7day)

If you don't know if a command is a classic or a nushell one, use `which`.
For example:

    〉which ls
    ╭───┬─────┬──────────────────────────┬──────────╮
    │ # │ arg │           path           │ built-in │
    ├───┼─────┼──────────────────────────┼──────────┤
    │ 0 │ ls  │ Nushell built-in command │ true     │
    ╰───┴─────┴──────────────────────────┴──────────╯
    〉which git
    ╭───┬─────┬──────────────┬──────────╮
    │ # │ arg │     path     │ built-in │
    ├───┼─────┼──────────────┼──────────┤
    │ 0 │ git │ /usr/bin/git │ false    │
    ╰───┴─────┴──────────────┴──────────╯
    〉which cd
    ╭───┬─────┬──────────────────────────┬──────────╮
    │ # │ arg │           path           │ built-in │
    ├───┼─────┼──────────────────────────┼──────────┤
    │ 0 │ cd  │ Nushell built-in command │ true     │
    ╰───┴─────┴──────────────────────────┴──────────╯
    〉which cat
    ╭───┬─────┬──────────────┬──────────╮
    │ # │ arg │     path     │ built-in │
    ├───┼─────┼──────────────┼──────────┤
    │ 0 │ cat │ /usr/bin/cat │ false    │
    ╰───┴─────┴──────────────┴──────────╯
    〉which which
    ╭───┬───────┬──────────────────────────┬──────────╮
    │ # │  arg  │           path           │ built-in │
    ├───┼───────┼──────────────────────────┼──────────┤
    │ 0 │ which │ Nushell built-in command │ true     │
    ╰───┴───────┴──────────────────────────┴──────────╯

Since `git` is your usual `git` command, the nushell help system won't work:

    〉help git
    Error: nu::shell::command_not_found (link)

    × Command not found
    ╭─[entry #20:1:1]
    1 │ help git
    ·      ─┬─
    ·       ╰── command not found
    ╰────

Of course you can still do

    〉git --help
    usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
            [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
            [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
            [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
            <command> [<args>]

    These are common Git commands used in various situations:

    start a working area (see also: git help tutorial)
    clone             Clone a repository into a new directory
    init              Create an empty Git repository or reinitialize an existing one

    work on the current change (see also: git help everyday)
    add               Add file contents to the index
    mv                Move or rename a file, a directory, or a symlink
    restore           Restore working tree files
    rm                Remove files from the working tree and from the index
    sparse-checkout   Initialize and modify the sparse-checkout

    examine the history and state (see also: git help revisions)
    bisect            Use binary search to find the commit that introduced a bug
    diff              Show changes between commits, commit and working tree, etc
    grep              Print lines matching a pattern
    log               Show commit logs
    show              Show various types of objects
    status            Show the working tree status

    grow, mark and tweak your common history
    branch            List, create, or delete branches
    commit            Record changes to the repository
    merge             Join two or more development histories together
    rebase            Reapply commits on top of another base tip
    reset             Reset current HEAD to the specified state
    switch            Switch branches
    tag               Create, list, delete or verify a tag object signed with GPG

    collaborate (see also: git help workflows)
    fetch             Download objects and refs from another repository
    pull              Fetch from and integrate with another repository or a local branch
    push              Update remote refs along with associated objects

    'git help -a' and 'git help -g' list available subcommands and some
    concept guides. See 'git help <command>' or 'git help <concept>'
    to read about a specific subcommand or concept.
    See 'git help git' for an overview of the system.

since `git` supports the `--help` option. To get some help about the
nushell commands, do

    〉help
    Welcome to Nushell.

    Here are some tips to help you get started.
    * help commands - list all available commands
    * help <command name> - display help about a particular command
    * help --find <text to search> - search through all of help

    Nushell works on the idea of a "pipeline". Pipelines are commands connected with the '|' character.
    Each stage in the pipeline works together to load, parse, and display information to you.

    [Examples]

    List the files in the current directory, sorted by size:
        ls | sort-by size

    Get information about the current system:
        sys | get host

    Get the processes on your system actively using CPU:
        ps | where cpu > 0

    You can also learn more at https://www.nushell.sh/book/

The list of all nushell commands:

    〉help commands    ╭─────┬──────────────────────────┬──────────────┬───────────┬───────────┬──────────────────────────────────────┬──────────────────────────────────────╮
    │  #  │           name           │   category   │ is_plugin │ is_custom │                usage                 │             extra_usage              │
    ├─────┼──────────────────────────┼──────────────┼───────────┼───────────┼──────────────────────────────────────┼──────────────────────────────────────┤
    │   0 │ alias                    │ core         │ false     │ false     │ Alias a command (with optional       │                                      │
    │     │                          │              │           │           │ flags) to a new name                 │                                      │
    │   1 │ all?                     │ filters      │ false     │ false     │ Test if every element of the input   │                                      │
    │     │                          │              │           │           │ matches a predicate.                 │                                      │
    │   2 │ ansi                     │ platform     │ false     │ false     │ Output ANSI codes to change color.   │ For escape sequences:                │
    │     │                          │              │           │           │                                      │ Escape: '\x1b[' is not required for  │
    │     │                          │              │           │           │                                      │ --escape parameter                   │
    │     │                          │              │           │           │                                      │ Format: #(;#)m                       │
    │     │                          │              │           │           │                                      │ Example: 1;31m for bold red or       │
    │     │                          │              │           │           │                                      │ 2;37;41m for dimmed white fg with    │
    │     │                          │              │           │           │                                      │ red bg                               │
    │     │                          │              │           │           │                                      │ There can be multiple text           │
    │     │                          │              │           │           │                                      │ formatting sequence numbers          │
    │     │                          │              │           │           │                                      │ separated by a ; and ending with an  │
    │     │                          │              │           │           │                                      │ m where the # is of the              │
    │     │                          │              │           │           │                                      │ following values:                    │
    │     │                          │              │           │           │                                      │     attribute_number, abbreviation,  │
    │     │                          │              │           │           │                                      │ description                          │
    │     │                          │              │           │           │                                      │     0     reset / normal display     │
    │     │                          │              │           │           │                                      │     1  b  bold or increased          │
    │     │                          │              │           │           │                                      │ intensity                            │
    │     │                          │              │           │           │                                      │     2  d  faint or decreased         │
    │     │                          │              │           │           │                                      │ intensity                            │
    │     │                          │              │           │           │                                      │     3  i  italic on (non-mono font)  │
    │     │                          │              │           │           │                                      │     4  u  underline on               │
    │     │                          │              │           │           │                                      │     5  l  slow blink on              │
    │     │                          │              │           │           │                                      │     6     fast blink on              │
    │     │                          │              │           │           │                                      │     7  r  reverse video on           │
    │     │                          │              │           │           │                                      │     8  h  nondisplayed (invisible)   │
    │     │                          │              │           │           │                                      │ on                                   │
    │     │                          │              │           │           │                                      │     9  s  strike-through on          │
    │     │                          │              │           │           │                                      │     foreground/bright colors         │
    │     │                          │              │           │           │                                      │ background/bright colors             │
    │     │                          │              │           │           │                                      │     30/90    black                   │
    │     │                          │              │           │           │                                      │ 40/100    black                      │
    │     │                          │              │           │           │                                      │     31/91    red                     │
    │     │                          │              │           │           │                                      │ 41/101    red                        │
    │     │                          │              │           │           │                                      │     32/92    green                   │
    │     │                          │              │           │           │                                      │ 42/102    green                      │
    │     │                          │              │           │           │                                      │     33/93    yellow                  │
    │     │                          │              │           │           │                                      │ 43/103    yellow                     │
    │     │                          │              │           │           │                                      │     34/94    blue                    │
    │     │                          │              │           │           │                                      │ 44/104    blue                       │
    │     │                          │              │           │           │                                      │     35/95    magenta                 │
    │     │                          │              │           │           │                                      │ 45/105    magenta                    │
    │     │                          │              │           │           │                                      │     36/96    cyan                    │
    │     │                          │              │           │           │                                      │ 46/106    cyan                       │
    │     │                          │              │           │           │                                      │     37/97    white                   │
    │     │                          │              │           │           │                                      │ 47/107    white                      │
    │     │                          │              │           │           │                                      │                                      │
    │     │                          │              │           │           │                                      │ https://en.wikipedia.org/wiki/ANSI_  │
    │     │                          │              │           │           │                                      │ escape_code                          │
    │     │                          │              │           │           │                                      │ OSC: '\x1b]' is not required for     │
    │     │                          │              │           │           │                                      │ --osc parameter                      │
    │     │                          │              │           │           │                                      │ Example: echo [(ansi -o '0') 'some   │
    │     │                          │              │           │           │                                      │ title' (char bel)] | str collect     │
    │     │                          │              │           │           │                                      │ Format: #                            │
    │     │                          │              │           │           │                                      │     0 Set window title and icon      │
    │     │                          │              │           │           │                                      │ name                                 │
    │     │                          │              │           │           │                                      │     1 Set icon name                  │
    │     │                          │              │           │           │                                      │     2 Set window title               │
    │     │                          │              │           │           │                                      │     4 Set/read color palette         │
    │     │                          │              │           │           │                                      │     9 iTerm2 Grown notifications     │
    │     │                          │              │           │           │                                      │     10 Set foreground color (x11     │
    │     │                          │              │           │           │                                      │ color spec)                          │
    │     │                          │              │           │           │                                      │     11 Set background color (x11     │
    │     │                          │              │           │           │                                      │ color spec)                          │
    │     │                          │              │           │           │                                      │     ... others                       │
    │   3 │ ansi gradient            │ platform     │ false     │ false     │ draw text with a provided start and  │                                      │
    │     │                          │              │           │           │ end code making a gradient           │                                      │
    │   4 │ ansi strip               │ platform     │ false     │ false     │ strip ansi escape sequences from     │                                      │
    │     │                          │              │           │           │ string                               │                                      │
    │   5 │ any?                     │ filters      │ false     │ false     │ Tests if any element of the input    │                                      │
    │     │                          │              │           │           │ matches a predicate.                 │                                      │
    │   6 │ append                   │ filters      │ false     │ false     │ Append a row to the table.           │                                      │
    │   7 │ benchmark                │ system       │ false     │ false     │ Time the running time of a block     │                                      │
    │   8 │ build-string             │ strings      │ false     │ false     │ Create a string from the arguments.  │                                      │
    │   9 │ cal                      │ generators   │ false     │ false     │ Display a calendar.                  │                                      │
    │  10 │ cd                       │ filesystem   │ false     │ false     │ Change directory.                    │                                      │
    │  11 │ char                     │ strings      │ false     │ false     │ Output special characters (e.g.,     │                                      │
    │     │                          │              │           │           │ 'newline').                          │                                      │
    │  12 │ clear                    │ platform     │ false     │ false     │ Clear the terminal.                  │                                      │
    │  13 │ collect                  │ filters      │ false     │ false     │ Collect the stream and pass it to a  │                                      │
    │     │                          │              │           │           │ block.                               │                                      │
    │  14 │ columns                  │ filters      │ false     │ false     │ Show the columns in the input.       │                                      │
    │  15 │ compact                  │ filters      │ false     │ false     │ Creates a table with non-empty       │                                      │
    │     │                          │              │           │           │ rows.                                │                                      │
    │  16 │ complete                 │ system       │ false     │ false     │ Complete the external piped in,      │                                      │
    │     │                          │              │           │           │ collecting outputs and exit code     │                                      │
    │  17 │ cp                       │ filesystem   │ false     │ false     │ Copy files.                          │                                      │
    │  18 │ create_left_prompt       │ default      │ false     │ true      │                                      │                                      │
    │  19 │ create_right_prompt      │ default      │ false     │ true      │                                      │                                      │
    │  20 │ dataframe                │ deprecated   │ false     │ false     │ Deprecated command                   │                                      │
    │  21 │ date                     │ date         │ false     │ false     │ date                                 │                                      │
    │  22 │ date format              │ date         │ false     │ false     │ Format a given date using a format   │                                      │
    │     │                          │              │           │           │ string.                              │                                      │
    │  23 │ date humanize            │ date         │ false     │ false     │ Print a 'humanized' format for the   │                                      │
    │     │                          │              │           │           │ date, relative to now.               │                                      │
    │  24 │ date list-timezone       │ date         │ false     │ false     │ List supported time zones.           │                                      │
    │  25 │ date now                 │ date         │ false     │ false     │ Get the current date.                │                                      │
    │  26 │ date to-table            │ date         │ false     │ false     │ Print the date in a structured       │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │  27 │ date to-timezone         │ date         │ false     │ false     │ Convert a date to a given time       │ Use 'date list-timezone' to list     │
    │     │                          │              │           │           │ zone.                                │ all supported time zones.            │
    │  28 │ debug                    │ core         │ false     │ false     │ Debug print the value(s) piped in.   │                                      │
    │  29 │ decode                   │ strings      │ false     │ false     │ Decode bytes as a string.            │ Multiple encodings are supported,    │
    │     │                          │              │           │           │                                      │ here is an example of a few:         │
    │     │                          │              │           │           │                                      │ big5, euc-jp, euc-kr, gbk,           │
    │     │                          │              │           │           │                                      │ iso-8859-1, utf-16, cp1252, latin5   │
    │     │                          │              │           │           │                                      │ For a more complete list of          │
    │     │                          │              │           │           │                                      │ encodings please refer to the        │
    │     │                          │              │           │           │                                      │ encoding_rs                          │
    │     │                          │              │           │           │                                      │ documentation link at                │
    │     │                          │              │           │           │                                      │ https://docs.rs/encoding_rs/0.8.28/  │
    │     │                          │              │           │           │                                      │ encoding_rs/#statics                 │
    │  30 │ def                      │ core         │ false     │ false     │ Define a custom command              │                                      │
    │  31 │ def-env                  │ core         │ false     │ false     │ Define a custom command, which       │                                      │
    │     │                          │              │           │           │ participates in the caller           │                                      │
    │     │                          │              │           │           │ environment                          │                                      │
    │  32 │ default                  │ filters      │ false     │ false     │ Sets a default row's column if       │                                      │
    │     │                          │              │           │           │ missing.                             │                                      │
    │  33 │ describe                 │ core         │ false     │ false     │ Describe the value(s) piped in.      │                                      │
    │  34 │ detect columns           │ strings      │ false     │ false     │ splits contents across multiple      │                                      │
    │     │                          │              │           │           │ columns via the separator.           │                                      │
    │  35 │ dfr                      │ dataframe    │ false     │ false     │ Dataframe commands                   │                                      │
    │  36 │ dfr aggregate            │ dataframe    │ false     │ false     │ Performs an aggregation operation    │                                      │
    │     │                          │              │           │           │ on a dataframe and groupby object    │                                      │
    │  37 │ dfr all-false            │ dataframe    │ false     │ false     │ Returns true if all values are       │                                      │
    │     │                          │              │           │           │ false                                │                                      │
    │  38 │ dfr all-true             │ dataframe    │ false     │ false     │ Returns true if all values are true  │                                      │
    │  39 │ dfr append               │ dataframe    │ false     │ false     │ Appends a new dataframe              │                                      │
    │  40 │ dfr arg-max              │ dataframe    │ false     │ false     │ Return index for max value in        │                                      │
    │     │                          │              │           │           │ series                               │                                      │
    │  41 │ dfr arg-min              │ dataframe    │ false     │ false     │ Return index for min value in        │                                      │
    │     │                          │              │           │           │ series                               │                                      │
    │  42 │ dfr arg-sort             │ dataframe    │ false     │ false     │ Returns indexes for a sorted series  │                                      │
    │  43 │ dfr arg-true             │ dataframe    │ false     │ false     │ Returns indexes where values are     │                                      │
    │     │                          │              │           │           │ true                                 │                                      │
    │  44 │ dfr arg-unique           │ dataframe    │ false     │ false     │ Returns indexes for unique values    │                                      │
    │  45 │ dfr as-date              │ dataframe    │ false     │ false     │ Converts string to date. Format      │                                      │
    │     │                          │              │           │           │ example:                             │                                      │
    │     │                          │              │           │           │         "%Y-%m-%d"    => 2021-12-31  │                                      │
    │     │                          │              │           │           │         "%d-%m-%Y"    => 31-12-2021  │                                      │
    │     │                          │              │           │           │         "%Y%m%d"      => 2021319     │                                      │
    │     │                          │              │           │           │ (2021-03-19)                         │                                      │
    │  46 │ dfr as-datetime          │ dataframe    │ false     │ false     │ Converts string to datetime. Format  │                                      │
    │     │                          │              │           │           │ example:                             │                                      │
    │     │                          │              │           │           │         "%y/%m/%d %H:%M:%S"  =>      │                                      │
    │     │                          │              │           │           │ 21/12/31 12:54:98                    │                                      │
    │     │                          │              │           │           │         "%y-%m-%d %H:%M:%S"  =>      │                                      │
    │     │                          │              │           │           │ 2021-12-31 24:58:01                  │                                      │
    │     │                          │              │           │           │         "%y/%m/%d %H:%M:%S"  =>      │                                      │
    │     │                          │              │           │           │ 21/12/31 24:58:01                    │                                      │
    │     │                          │              │           │           │         "%y%m%d %H:%M:%S"    =>      │                                      │
    │     │                          │              │           │           │ 210319 23:58:50                      │                                      │
    │     │                          │              │           │           │         "%Y/%m/%d %H:%M:%S"  =>      │                                      │
    │     │                          │              │           │           │ 2021/12/31 12:54:98                  │                                      │
    │     │                          │              │           │           │         "%Y-%m-%d %H:%M:%S"  =>      │                                      │
    │     │                          │              │           │           │ 2021-12-31 24:58:01                  │                                      │
    │     │                          │              │           │           │         "%Y/%m/%d %H:%M:%S"  =>      │                                      │
    │     │                          │              │           │           │ 2021/12/31 24:58:01                  │                                      │
    │     │                          │              │           │           │         "%Y%m%d %H:%M:%S"    =>      │                                      │
    │     │                          │              │           │           │ 20210319 23:58:50                    │                                      │
    │     │                          │              │           │           │         "%FT%H:%M:%S"        =>      │                                      │
    │     │                          │              │           │           │ 2019-04-18T02:45:55                  │                                      │
    │     │                          │              │           │           │         "%FT%H:%M:%S.%6f"    =>      │                                      │
    │     │                          │              │           │           │ microseconds                         │                                      │
    │     │                          │              │           │           │         "%FT%H:%M:%S.%9f"    =>      │                                      │
    │     │                          │              │           │           │ nanoseconds                          │                                      │
    │  47 │ dfr column               │ dataframe    │ false     │ false     │ Returns the selected column          │                                      │
    │  48 │ dfr concatenate          │ dataframe    │ false     │ false     │ Concatenates strings with other      │                                      │
    │     │                          │              │           │           │ array                                │                                      │
    │  49 │ dfr contains             │ dataframe    │ false     │ false     │ Checks if a pattern is contained in  │                                      │
    │     │                          │              │           │           │ a string                             │                                      │
    │  50 │ dfr count-null           │ dataframe    │ false     │ false     │ Counts null values                   │                                      │
    │  51 │ dfr count-unique         │ dataframe    │ false     │ false     │ Counts unique values                 │                                      │
    │  52 │ dfr cumulative           │ dataframe    │ false     │ false     │ Cumulative calculation for a series  │                                      │
    │  53 │ dfr describe             │ dataframe    │ false     │ false     │ Describes dataframes numeric         │                                      │
    │     │                          │              │           │           │ columns                              │                                      │
    │  54 │ dfr drop                 │ dataframe    │ false     │ false     │ Creates a new dataframe by dropping  │                                      │
    │     │                          │              │           │           │ the selected columns                 │                                      │
    │  55 │ dfr drop-duplicates      │ dataframe    │ false     │ false     │ Drops duplicate values in dataframe  │                                      │
    │  56 │ dfr drop-nulls           │ dataframe    │ false     │ false     │ Drops null values in dataframe       │                                      │
    │  57 │ dfr dtypes               │ dataframe    │ false     │ false     │ Show dataframe data types            │                                      │
    │  58 │ dfr filter-with          │ dataframe    │ false     │ false     │ Filters dataframe using a mask as    │                                      │
    │     │                          │              │           │           │ reference                            │                                      │
    │  59 │ dfr first                │ dataframe    │ false     │ false     │ Creates new dataframe with first     │                                      │
    │     │                          │              │           │           │ rows                                 │                                      │
    │  60 │ dfr get                  │ dataframe    │ false     │ false     │ Creates dataframe with the selected  │                                      │
    │     │                          │              │           │           │ columns                              │                                      │
    │  61 │ dfr get-day              │ dataframe    │ false     │ false     │ Gets day from date                   │                                      │
    │  62 │ dfr get-hour             │ dataframe    │ false     │ false     │ Gets hour from date                  │                                      │
    │  63 │ dfr get-minute           │ dataframe    │ false     │ false     │ Gets minute from date                │                                      │
    │  64 │ dfr get-month            │ dataframe    │ false     │ false     │ Gets month from date                 │                                      │
    │  65 │ dfr get-nanosecond       │ dataframe    │ false     │ false     │ Gets nanosecond from date            │                                      │
    │  66 │ dfr get-ordinal          │ dataframe    │ false     │ false     │ Gets ordinal from date               │                                      │
    │  67 │ dfr get-second           │ dataframe    │ false     │ false     │ Gets second from date                │                                      │
    │  68 │ dfr get-week             │ dataframe    │ false     │ false     │ Gets week from date                  │                                      │
    │  69 │ dfr get-weekday          │ dataframe    │ false     │ false     │ Gets weekday from date               │                                      │
    │  70 │ dfr get-year             │ dataframe    │ false     │ false     │ Gets year from date                  │                                      │
    │  71 │ dfr group-by             │ dataframe    │ false     │ false     │ Creates a groupby object that can    │                                      │
    │     │                          │              │           │           │ be used for other aggregations       │                                      │
    │  72 │ dfr is-duplicated        │ dataframe    │ false     │ false     │ Creates mask indicating duplicated   │                                      │
    │     │                          │              │           │           │ values                               │                                      │
    │  73 │ dfr is-in                │ dataframe    │ false     │ false     │ Checks if elements from a series     │                                      │
    │     │                          │              │           │           │ are contained in right series        │                                      │
    │  74 │ dfr is-not-null          │ dataframe    │ false     │ false     │ Creates mask where value is not      │                                      │
    │     │                          │              │           │           │ null                                 │                                      │
    │  75 │ dfr is-null              │ dataframe    │ false     │ false     │ Creates mask where value is null     │                                      │
    │  76 │ dfr is-unique            │ dataframe    │ false     │ false     │ Creates mask indicating unique       │                                      │
    │     │                          │              │           │           │ values                               │                                      │
    │  77 │ dfr join                 │ dataframe    │ false     │ false     │ Joins a dataframe using columns as   │                                      │
    │     │                          │              │           │           │ reference                            │                                      │
    │  78 │ dfr last                 │ dataframe    │ false     │ false     │ Creates new dataframe with tail      │                                      │
    │     │                          │              │           │           │ rows                                 │                                      │
    │  79 │ dfr list                 │ dataframe    │ false     │ false     │ Lists stored dataframes              │                                      │
    │  80 │ dfr melt                 │ dataframe    │ false     │ false     │ Unpivot a DataFrame from wide to     │                                      │
    │     │                          │              │           │           │ long format                          │                                      │
    │  81 │ dfr not                  │ dataframe    │ false     │ false     │ Inverts boolean mask                 │                                      │
    │  82 │ dfr open                 │ dataframe    │ false     │ false     │ Opens csv, json or parquet file to   │                                      │
    │     │                          │              │           │           │ create dataframe                     │                                      │
    │  83 │ dfr pivot                │ dataframe    │ false     │ false     │ Performs a pivot operation on a      │                                      │
    │     │                          │              │           │           │ groupby object                       │                                      │
    │  84 │ dfr rename               │ dataframe    │ false     │ false     │ Renames a series                     │                                      │
    │  85 │ dfr rename-col           │ dataframe    │ false     │ false     │ rename a dataframe column            │                                      │
    │  86 │ dfr replace              │ dataframe    │ false     │ false     │ Replace the leftmost (sub)string by  │                                      │
    │     │                          │              │           │           │ a regex pattern                      │                                      │
    │  87 │ dfr replace-all          │ dataframe    │ false     │ false     │ Replace all (sub)strings by a regex  │                                      │
    │     │                          │              │           │           │ pattern                              │                                      │
    │  88 │ dfr rolling              │ dataframe    │ false     │ false     │ Rolling calculation for a series     │                                      │
    │  89 │ dfr sample               │ dataframe    │ false     │ false     │ Create sample dataframe              │                                      │
    │  90 │ dfr set                  │ dataframe    │ false     │ false     │ Sets value where given mask is true  │                                      │
    │  91 │ dfr set-with-idx         │ dataframe    │ false     │ false     │ Sets value in the given index        │                                      │
    │  92 │ dfr shape                │ dataframe    │ false     │ false     │ Shows column and row size for a      │                                      │
    │     │                          │              │           │           │ dataframe                            │                                      │
    │  93 │ dfr shift                │ dataframe    │ false     │ false     │ Shifts the values by a given period  │                                      │
    │  94 │ dfr slice                │ dataframe    │ false     │ false     │ Creates new dataframe from a slice   │                                      │
    │     │                          │              │           │           │ of rows                              │                                      │
    │  95 │ dfr sort                 │ dataframe    │ false     │ false     │ Creates new sorted dataframe or      │                                      │
    │     │                          │              │           │           │ series                               │                                      │
    │  96 │ dfr str-lengths          │ dataframe    │ false     │ false     │ Get lengths of all strings           │                                      │
    │  97 │ dfr str-slice            │ dataframe    │ false     │ false     │ Slices the string from the start     │                                      │
    │     │                          │              │           │           │ position until the selected length   │                                      │
    │  98 │ dfr strftime             │ dataframe    │ false     │ false     │ Formats date based on string rule    │                                      │
    │  99 │ dfr take                 │ dataframe    │ false     │ false     │ Creates new dataframe using the      │                                      │
    │     │                          │              │           │           │ given indices                        │                                      │
    │ 100 │ dfr to-csv               │ dataframe    │ false     │ false     │ Saves dataframe to csv file          │                                      │
    │ 101 │ dfr to-df                │ dataframe    │ false     │ false     │ Converts a List, Table or            │                                      │
    │     │                          │              │           │           │ Dictionary into a dataframe          │                                      │
    │ 102 │ dfr to-dummies           │ dataframe    │ false     │ false     │ Creates a new dataframe with dummy   │                                      │
    │     │                          │              │           │           │ variables                            │                                      │
    │ 103 │ dfr to-lowercase         │ dataframe    │ false     │ false     │ Lowercase the strings in the column  │                                      │
    │ 104 │ dfr to-nu                │ dataframe    │ false     │ false     │ Converts a section of the dataframe  │                                      │
    │     │                          │              │           │           │ to Nushell Table                     │                                      │
    │ 105 │ dfr to-parquet           │ dataframe    │ false     │ false     │ Saves dataframe to parquet file      │                                      │
    │ 106 │ dfr to-uppercase         │ dataframe    │ false     │ false     │ Uppercase the strings in the column  │                                      │
    │ 107 │ dfr unique               │ dataframe    │ false     │ false     │ Returns unique values from a series  │                                      │
    │ 108 │ dfr value-counts         │ dataframe    │ false     │ false     │ Returns a dataframe with the counts  │                                      │
    │     │                          │              │           │           │ for unique values in series          │                                      │
    │ 109 │ dfr with-column          │ dataframe    │ false     │ false     │ Adds a series to the dataframe       │                                      │
    │ 110 │ do                       │ core         │ false     │ false     │ Run a block                          │                                      │
    │ 111 │ drop                     │ filters      │ false     │ false     │ Remove the last number of rows or    │                                      │
    │     │                          │              │           │           │ columns.                             │                                      │
    │ 112 │ drop column              │ filters      │ false     │ false     │ Remove the last number of columns.   │                                      │
    │     │                          │              │           │           │ If you want to remove columns by     │                                      │
    │     │                          │              │           │           │ name, try 'reject'.                  │                                      │
    │ 113 │ drop nth                 │ filters      │ false     │ false     │ Drop the selected rows.              │                                      │
    │ 114 │ du                       │ core         │ false     │ false     │ Find disk usage sizes of specified   │                                      │
    │     │                          │              │           │           │ items.                               │                                      │
    │ 115 │ each                     │ filters      │ false     │ false     │ Run a block on each element of       │                                      │
    │     │                          │              │           │           │ input                                │                                      │
    │ 116 │ echo                     │ core         │ false     │ false     │ Echo the arguments back to the       │                                      │
    │     │                          │              │           │           │ user.                                │                                      │
    │ 117 │ empty?                   │ filters      │ false     │ false     │ Check for empty values.              │                                      │
    │ 118 │ enter                    │ shells       │ false     │ false     │ Enters a new shell at the given      │                                      │
    │     │                          │              │           │           │ path.                                │                                      │
    │ 119 │ env                      │ env          │ false     │ false     │ Display current environment          │                                      │
    │     │                          │              │           │           │ variables                            │                                      │
    │ 120 │ error make               │ core         │ false     │ false     │ Create an error.                     │                                      │
    │ 121 │ every                    │ filters      │ false     │ false     │ Show (or skip) every n-th row,       │                                      │
    │     │                          │              │           │           │ starting from the first one.         │                                      │
    │ 122 │ exec                     │ system       │ false     │ false     │ Execute a command, replacing the     │ Currently supported only on          │
    │     │                          │              │           │           │ current process.                     │ Unix-based systems.                  │
    │ 123 │ exit                     │ shells       │ false     │ false     │ Runs a script file in the current    │                                      │
    │     │                          │              │           │           │ context.                             │                                      │
    │ 124 │ export                   │ core         │ false     │ false     │ Export custom commands or            │                                      │
    │     │                          │              │           │           │ environment variables from a module. │                                      │
    │ 125 │ export def               │ core         │ false     │ false     │ Define an alias and export it from   │                                      │
    │     │                          │              │           │           │ a module                             │                                      │
    │ 126 │ export def               │ core         │ false     │ false     │ Define a custom command and export   │                                      │
    │     │                          │              │           │           │ it from a module                     │                                      │
    │ 127 │ export def-env           │ core         │ false     │ false     │ Define a custom command that         │                                      │
    │     │                          │              │           │           │ participates in the environment and  │                                      │
    │     │                          │              │           │           │ export it from a module              │                                      │
    │ 128 │ export env               │ core         │ false     │ false     │ Export a block from a module that    │                                      │
    │     │                          │              │           │           │ will be evaluated as an environment  │                                      │
    │     │                          │              │           │           │ variable when imported.              │                                      │
    │ 129 │ export extern            │ core         │ false     │ false     │ Define an extern and export it from  │                                      │
    │     │                          │              │           │           │ a module                             │                                      │
    │ 130 │ extern                   │ core         │ false     │ false     │ Define a signature for an external   │                                      │
    │     │                          │              │           │           │ command                              │                                      │
    │ 131 │ fetch                    │ network      │ false     │ false     │ Fetch the contents from a URL (HTTP  │                                      │
    │     │                          │              │           │           │ GET operation).                      │                                      │
    │ 132 │ find                     │ filters      │ false     │ false     │ Searches terms in the input or for   │                                      │
    │     │                          │              │           │           │ elements of the input that satisfies │                                      │
    │     │                          │              │           │           │ the predicate.                       │                                      │
    │ 133 │ first                    │ filters      │ false     │ false     │ Show only the first number of rows.  │                                      │
    │ 134 │ flatten                  │ filters      │ false     │ false     │ Flatten the table.                   │                                      │
    │ 135 │ fmt                      │ conversions  │ false     │ false     │ format numbers                       │                                      │
    │ 136 │ for                      │ core         │ false     │ false     │ Loop over a range                    │                                      │
    │ 137 │ format                   │ strings      │ false     │ false     │ Format columns into a string using   │                                      │
    │     │                          │              │           │           │ a simple pattern.                    │                                      │
    │ 138 │ from                     │ formats      │ false     │ false     │ Parse a string or binary data into   │                                      │
    │     │                          │              │           │           │ structured data                      │                                      │
    │ 139 │ from csv                 │ formats      │ false     │ false     │ Parse text as .csv and create        │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 140 │ from eml                 │ formats      │ false     │ false     │ Parse text as .eml and create        │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 141 │ from ics                 │ formats      │ false     │ false     │ Parse text as .ics and create        │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 142 │ from ini                 │ formats      │ false     │ false     │ Parse text as .ini and create table  │                                      │
    │ 143 │ from json                │ formats      │ false     │ false     │ Convert from json to structured      │                                      │
    │     │                          │              │           │           │ data                                 │                                      │
    │ 144 │ from nuon                │ experimental │ false     │ false     │ Convert from nuon to structured      │                                      │
    │     │                          │              │           │           │ data                                 │                                      │
    │ 145 │ from ods                 │ formats      │ false     │ false     │ Parse OpenDocument                   │                                      │
    │     │                          │              │           │           │ Spreadsheet(.ods) data and create    │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 146 │ from ssv                 │ formats      │ false     │ false     │ Parse text as space-separated        │                                      │
    │     │                          │              │           │           │ values and create a table. The       │                                      │
    │     │                          │              │           │           │ default minimum number of spaces     │                                      │
    │     │                          │              │           │           │ counted as a separator is 2.         │                                      │
    │ 147 │ from toml                │ formats      │ false     │ false     │ Parse text as .toml and create       │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 148 │ from tsv                 │ formats      │ false     │ false     │ Parse text as .tsv and create        │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 149 │ from url                 │ formats      │ false     │ false     │ Parse url-encoded string as a        │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 150 │ from vcf                 │ formats      │ false     │ false     │ Parse text as .vcf and create        │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 151 │ from xlsx                │ formats      │ false     │ false     │ Parse binary Excel(.xlsx) data and   │                                      │
    │     │                          │              │           │           │ create table.                        │                                      │
    │ 152 │ from xml                 │ formats      │ false     │ false     │ Parse text as .xml and create        │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 153 │ from yaml                │ formats      │ false     │ false     │ Parse text as .yaml/.yml and create  │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 154 │ from yml                 │ formats      │ false     │ false     │ Parse text as .yaml/.yml and create  │                                      │
    │     │                          │              │           │           │ table.                               │                                      │
    │ 155 │ g                        │ shells       │ false     │ false     │ Switch to a given shell.             │                                      │
    │ 156 │ get                      │ filters      │ false     │ false     │ Extract data using a cell path.      │                                      │
    │ 157 │ git checkout             │ default      │ false     │ false     │                                      │                                      │
    │ 158 │ git push                 │ default      │ false     │ false     │                                      │                                      │
    │ 159 │ grid                     │ viewers      │ false     │ false     │ Renders the output to a textual      │ grid was built to give a concise     │
    │     │                          │              │           │           │ terminal grid.                       │ gridded layout for ls. however,      │
    │     │                          │              │           │           │                                      │ it determines what to put in the     │
    │     │                          │              │           │           │                                      │ grid by looking for a column named   │
    │     │                          │              │           │           │                                      │ 'name'. this works great for tables  │
    │     │                          │              │           │           │                                      │ and records but for lists we         │
    │     │                          │              │           │           │                                      │ need to do something different.      │
    │     │                          │              │           │           │                                      │ such as with '[one two three] |      │
    │     │                          │              │           │           │                                      │ grid'                                │
    │     │                          │              │           │           │                                      │ it creates a fake column called      │
    │     │                          │              │           │           │                                      │ 'name' for these values so that it   │
    │     │                          │              │           │           │                                      │ prints out the list properly.        │
    │ 160 │ group                    │ filters      │ false     │ false     │ Groups input into groups of          │                                      │
    │     │                          │              │           │           │ `group_size`.                        │                                      │
    │ 161 │ group-by                 │ default      │ false     │ false     │ Create a new table grouped.          │                                      │
    │ 162 │ hash                     │ hash         │ false     │ false     │ Apply hash function.                 │                                      │
    │ 163 │ hash base64              │ hash         │ false     │ false     │ base64 encode or decode a value      │                                      │
    │ 164 │ hash md5                 │ default      │ false     │ false     │ hash a value using the md5 hash      │                                      │
    │     │                          │              │           │           │ algorithm                            │                                      │
    │ 165 │ hash sha256              │ default      │ false     │ false     │ hash a value using the sha256 hash   │                                      │
    │     │                          │              │           │           │ algorithm                            │                                      │
    │ 166 │ headers                  │ filters      │ false     │ false     │ Use the first row of the table as    │                                      │
    │     │                          │              │           │           │ column names.                        │                                      │
    │ 167 │ help                     │ core         │ false     │ false     │ Display help information about       │                                      │
    │     │                          │              │           │           │ commands.                            │                                      │
    │ 168 │ hide                     │ core         │ false     │ false     │ Hide symbols in the current scope    │ Symbols are hidden by priority:      │
    │     │                          │              │           │           │                                      │ First aliases, then custom commands, │
    │     │                          │              │           │           │                                      │ then environment variables.          │
    │ 169 │ history                  │ core         │ false     │ false     │ Get the command history              │                                      │
    │ 170 │ if                       │ core         │ false     │ false     │ Conditionally run a block.           │                                      │
    │ 171 │ ignore                   │ core         │ false     │ false     │ Ignore the output of the previous    │                                      │
    │     │                          │              │           │           │ command in the pipeline              │                                      │
    │ 172 │ input                    │ platform     │ false     │ false     │ Get input from the user.             │                                      │
    │ 173 │ insert                   │ filters      │ false     │ false     │ Insert a new column.                 │                                      │
    │ 174 │ into                     │ conversions  │ false     │ false     │ Apply into function.                 │                                      │
    │ 175 │ into binary              │ conversions  │ false     │ false     │ Convert value to a binary primitive  │                                      │
    │ 176 │ into bool                │ conversions  │ false     │ false     │ Convert value to boolean             │                                      │
    │ 177 │ into datetime            │ conversions  │ false     │ false     │ converts text into datetime          │                                      │
    │ 178 │ into decimal             │ default      │ false     │ false     │ converts text into decimal           │                                      │
    │ 179 │ into duration            │ conversions  │ false     │ false     │ Convert value to duration            │                                      │
    │ 180 │ into filesize            │ conversions  │ false     │ false     │ Convert value to filesize            │                                      │
    │ 181 │ into int                 │ conversions  │ false     │ false     │ Convert value to integer             │                                      │
    │ 182 │ into string              │ conversions  │ false     │ false     │ Convert value to string              │                                      │
    │ 183 │ keep                     │ filters      │ false     │ false     │ Keep the first n elements of the     │                                      │
    │     │                          │              │           │           │ input.                               │                                      │
    │ 184 │ keep until               │ filters      │ false     │ false     │ Keep elements of the input until a   │                                      │
    │     │                          │              │           │           │ predicate is true.                   │                                      │
    │ 185 │ keep while               │ filters      │ false     │ false     │ Keep elements of the input while a   │                                      │
    │     │                          │              │           │           │ predicate is true.                   │                                      │
    │ 186 │ keybindings              │ platform     │ false     │ false     │ Keybindings related commands         │                                      │
    │ 187 │ keybindings default      │ platform     │ false     │ false     │ List default keybindings             │                                      │
    │ 188 │ keybindings list         │ platform     │ false     │ false     │ List available options that can be   │                                      │
    │     │                          │              │           │           │ used to create keybindings           │                                      │
    │ 189 │ keybindings listen       │ platform     │ false     │ false     │ Get input from the user.             │                                      │
    │ 190 │ kill                     │ platform     │ false     │ false     │ Kill a process using the process     │                                      │
    │     │                          │              │           │           │ id.                                  │                                      │
    │ 191 │ last                     │ filters      │ false     │ false     │ Show only the last number of rows.   │                                      │
    │ 192 │ length                   │ filters      │ false     │ false     │ Count the number of elements in the  │                                      │
    │     │                          │              │           │           │ input.                               │                                      │
    │ 193 │ let                      │ core         │ false     │ false     │ Create a variable and give it a      │                                      │
    │     │                          │              │           │           │ value.                               │                                      │
    │ 194 │ let-env                  │ env          │ false     │ false     │ Create an environment variable and   │                                      │
    │     │                          │              │           │           │ give it a value.                     │                                      │
    │ 195 │ lines                    │ filters      │ false     │ false     │ Converts input to lines              │                                      │
    │ 196 │ load-env                 │ filesystem   │ false     │ false     │ Loads an environment update from a   │                                      │
    │     │                          │              │           │           │ record.                              │                                      │
    │ 197 │ ls                       │ filesystem   │ false     │ false     │ List the files in a directory.       │                                      │
    │ 198 │ match                    │ deprecated   │ false     │ false     │ Deprecated command                   │                                      │
    │ 199 │ math                     │ math         │ false     │ false     │ Use mathematical functions as        │                                      │
    │     │                          │              │           │           │ aggregate functions on a list of     │                                      │
    │     │                          │              │           │           │ numbers or tables.                   │                                      │
    │ 200 │ math abs                 │ math         │ false     │ false     │ Returns absolute values of a list    │                                      │
    │     │                          │              │           │           │ of numbers                           │                                      │
    │ 201 │ math avg                 │ math         │ false     │ false     │ Finds the average of a list of       │                                      │
    │     │                          │              │           │           │ numbers or tables                    │                                      │
    │ 202 │ math ceil                │ math         │ false     │ false     │ Applies the ceil function to a list  │                                      │
    │     │                          │              │           │           │ of numbers                           │                                      │
    │ 203 │ math eval                │ math         │ false     │ false     │ Evaluate a math expression into a    │                                      │
    │     │                          │              │           │           │ number                               │                                      │
    │ 204 │ math floor               │ math         │ false     │ false     │ Applies the floor function to a      │                                      │
    │     │                          │              │           │           │ list of numbers                      │                                      │
    │ 205 │ math max                 │ math         │ false     │ false     │ Finds the maximum within a list of   │                                      │
    │     │                          │              │           │           │ numbers or tables                    │                                      │
    │ 206 │ math median              │ math         │ false     │ false     │ Gets the median of a list of         │                                      │
    │     │                          │              │           │           │ numbers                              │                                      │
    │ 207 │ math min                 │ math         │ false     │ false     │ Finds the minimum within a list of   │                                      │
    │     │                          │              │           │           │ numbers or tables                    │                                      │
    │ 208 │ math mode                │ math         │ false     │ false     │ Gets the most frequent element(s)    │                                      │
    │     │                          │              │           │           │ from a list of numbers or tables     │                                      │
    │ 209 │ math product             │ math         │ false     │ false     │ Finds the product of a list of       │                                      │
    │     │                          │              │           │           │ numbers or tables                    │                                      │
    │ 210 │ math round               │ math         │ false     │ false     │ Applies the round function to a      │                                      │
    │     │                          │              │           │           │ list of numbers                      │                                      │
    │ 211 │ math sqrt                │ math         │ false     │ false     │ Applies the square root function to  │                                      │
    │     │                          │              │           │           │ a list of numbers                    │                                      │
    │ 212 │ math stddev              │ math         │ false     │ false     │ Finds the stddev of a list of        │                                      │
    │     │                          │              │           │           │ numbers or tables                    │                                      │
    │ 213 │ math sum                 │ math         │ false     │ false     │ Finds the sum of a list of numbers   │                                      │
    │     │                          │              │           │           │ or tables                            │                                      │
    │ 214 │ math variance            │ math         │ false     │ false     │ Finds the variance of a list of      │                                      │
    │     │                          │              │           │           │ numbers or tables                    │                                      │
    │ 215 │ merge                    │ filters      │ false     │ false     │ Merge a table into an input table    │                                      │
    │ 216 │ metadata                 │ core         │ false     │ false     │ Get the metadata for items in the    │                                      │
    │     │                          │              │           │           │ stream                               │                                      │
    │ 217 │ mkdir                    │ filesystem   │ false     │ false     │ Make directories, creates            │                                      │
    │     │                          │              │           │           │ intermediary directories as          │                                      │
    │     │                          │              │           │           │ required.                            │                                      │
    │ 218 │ module                   │ core         │ false     │ false     │ Define a custom module               │                                      │
    │ 219 │ move                     │ filters      │ false     │ false     │ Move columns before or after other   │                                      │
    │     │                          │              │           │           │ columns                              │                                      │
    │ 220 │ mv                       │ filesystem   │ false     │ false     │ Move files or directories.           │                                      │
    │ 221 │ n                        │ shells       │ false     │ false     │ Switch to the next shell.            │                                      │
    │ 222 │ nth                      │ deprecated   │ false     │ false     │ Deprecated command                   │                                      │
    │ 223 │ nu-highlight             │ strings      │ false     │ false     │ Syntax highlight the input string.   │                                      │
    │ 224 │ open                     │ filesystem   │ false     │ false     │ Load a file into a cell, converting  │                                      │
    │     │                          │              │           │           │ to table if possible (avoid by       │                                      │
    │     │                          │              │           │           │ appending '--raw').                  │                                      │
    │ 225 │ p                        │ shells       │ false     │ false     │ Switch to the previous shell.        │                                      │
    │ 226 │ par-each                 │ filters      │ false     │ false     │ Run a block on each element of       │                                      │
    │     │                          │              │           │           │ input in parallel                    │                                      │
    │ 227 │ parse                    │ strings      │ false     │ false     │ Parse columns from string data       │                                      │
    │     │                          │              │           │           │ using a simple pattern.              │                                      │
    │ 228 │ path                     │ default      │ false     │ false     │ Explore and manipulate paths.        │ There are three ways to represent a  │
    │     │                          │              │           │           │                                      │ path:                                │
    │     │                          │              │           │           │                                      │ * As a path literal, e.g.,           │
    │     │                          │              │           │           │                                      │ '/home/viking/spam.txt'              │
    │     │                          │              │           │           │                                      │ * As a structured path: a table      │
    │     │                          │              │           │           │                                      │ with 'parent', 'stem', and           │
    │     │                          │              │           │           │                                      │ 'extension' (and                     │
    │     │                          │              │           │           │                                      │ * 'prefix' on Windows) columns.      │
    │     │                          │              │           │           │                                      │ This format is produced by the 'path │
    │     │                          │              │           │           │                                      │ parse'                               │
    │     │                          │              │           │           │                                      │   subcommand.                        │
    │     │                          │              │           │           │                                      │ * As an inner list of path parts,    │
    │     │                          │              │           │           │                                      │ e.g., '[[ / home viking spam.txt     │
    │     │                          │              │           │           │                                      │ ]]'.                                 │
    │     │                          │              │           │           │                                      │   Splitting into parts is done by    │
    │     │                          │              │           │           │                                      │ the `path split` command.            │
    │     │                          │              │           │           │                                      │ All subcommands accept all three     │
    │     │                          │              │           │           │                                      │ variants as an input. Furthermore,   │
    │     │                          │              │           │           │                                      │ the 'path                            │
    │     │                          │              │           │           │                                      │ join' subcommand can be used to      │
    │     │                          │              │           │           │                                      │ join the structured path or path     │
    │     │                          │              │           │           │                                      │ parts back into                      │
    │     │                          │              │           │           │                                      │ the path literal.                    │
    │ 229 │ path basename            │ default      │ false     │ false     │ Get the final component of a path    │                                      │
    │ 230 │ path dirname             │ default      │ false     │ false     │ Get the parent directory of a path   │                                      │
    │ 231 │ path exists              │ default      │ false     │ false     │ Check whether a path exists          │                                      │
    │ 232 │ path expand              │ default      │ false     │ false     │ Try to expand a path to its          │                                      │
    │     │                          │              │           │           │ absolute form                        │                                      │
    │ 233 │ path join                │ default      │ false     │ false     │ Join a structured path or a list of  │ Optionally, append an additional     │
    │     │                          │              │           │           │ path parts.                          │ path to the result. It is designed   │
    │     │                          │              │           │           │                                      │ to accept                            │
    │     │                          │              │           │           │                                      │ the output of 'path parse' and       │
    │     │                          │              │           │           │                                      │ 'path split' subcommands.            │
    │ 234 │ path parse               │ default      │ false     │ false     │ Convert a path into structured       │ Each path is split into a table      │
    │     │                          │              │           │           │ data.                                │ with 'parent', 'stem' and            │
    │     │                          │              │           │           │                                      │ 'extension' fields.                  │
    │     │                          │              │           │           │                                      │ On Windows, an extra 'prefix'        │
    │     │                          │              │           │           │                                      │ column is added.                     │
    │ 235 │ path relative-to         │ default      │ false     │ false     │ Get a path as relative to another    │ Can be used only when the input and  │
    │     │                          │              │           │           │ path.                                │ the argument paths are either both   │
    │     │                          │              │           │           │                                      │ absolute or both relative. The       │
    │     │                          │              │           │           │                                      │ argument path needs to be a parent   │
    │     │                          │              │           │           │                                      │ of the input                         │
    │     │                          │              │           │           │                                      │ path.                                │
    │ 236 │ path split               │ default      │ false     │ false     │ Split a path into parts by a         │                                      │
    │     │                          │              │           │           │ separator.                           │                                      │
    │ 237 │ path type                │ default      │ false     │ false     │ Get the type of the object a path    │                                      │
    │     │                          │              │           │           │ refers to (e.g., file, dir, symlink) │                                      │
    │ 238 │ pivot                    │ deprecated   │ false     │ false     │ Deprecated command                   │                                      │
    │ 239 │ post                     │ network      │ false     │ false     │ Post a body to a URL (HTTP POST      │                                      │
    │     │                          │              │           │           │ operation).                          │                                      │
    │ 240 │ prepend                  │ filters      │ false     │ false     │ Prepend a row to the table.          │                                      │
    │ 241 │ print                    │ strings      │ false     │ false     │ Prints the values given              │                                      │
    │ 242 │ ps                       │ system       │ false     │ false     │ View information about system        │                                      │
    │     │                          │              │           │           │ processes.                           │                                      │
    │ 243 │ random                   │ random       │ false     │ false     │ Generate a random values.            │                                      │
    │ 244 │ random bool              │ random       │ false     │ false     │ Generate a random boolean value      │                                      │
    │ 245 │ random chars             │ random       │ false     │ false     │ Generate random chars                │                                      │
    │ 246 │ random decimal           │ random       │ false     │ false     │ Generate a random decimal within a   │                                      │
    │     │                          │              │           │           │ range [min..max]                     │                                      │
    │ 247 │ random dice              │ random       │ false     │ false     │ Generate a random dice roll          │                                      │
    │ 248 │ random integer           │ random       │ false     │ false     │ Generate a random integer            │                                      │
    │     │                          │              │           │           │ [min..max]                           │                                      │
    │ 249 │ random uuid              │ random       │ false     │ false     │ Generate a random uuid4 string       │                                      │
    │ 250 │ range                    │ filters      │ false     │ false     │ Return only the selected rows.       │                                      │
    │ 251 │ reduce                   │ default      │ false     │ false     │ Aggregate a list table to a single   │                                      │
    │     │                          │              │           │           │ value using an accumulator block.    │                                      │
    │ 252 │ register                 │ core         │ false     │ false     │ Register a plugin                    │                                      │
    │ 253 │ reject                   │ filters      │ false     │ false     │ Remove the given columns from the    │                                      │
    │     │                          │              │           │           │ table. If you want to remove rows,   │                                      │
    │     │                          │              │           │           │ try 'drop'.                          │                                      │
    │ 254 │ rename                   │ filters      │ false     │ false     │ Creates a new table with columns     │                                      │
    │     │                          │              │           │           │ renamed.                             │                                      │
    │ 255 │ reverse                  │ filters      │ false     │ false     │ Reverses the table.                  │                                      │
    │ 256 │ rm                       │ filesystem   │ false     │ false     │ Remove file(s).                      │                                      │
    │ 257 │ roll                     │ filters      │ false     │ false     │ Rolling commands for tables          │                                      │
    │ 258 │ roll down                │ filters      │ false     │ false     │ Roll table rows down                 │                                      │
    │ 259 │ roll left                │ filters      │ false     │ false     │ Roll table columns left              │                                      │
    │ 260 │ roll right               │ filters      │ false     │ false     │ Roll table columns right             │                                      │
    │ 261 │ roll up                  │ filters      │ false     │ false     │ Roll table rows up                   │                                      │
    │ 262 │ rotate                   │ filters      │ false     │ false     │ Rotates a table clockwise (default)  │                                      │
    │     │                          │              │           │           │ or counter-clockwise (use --ccw      │                                      │
    │     │                          │              │           │           │ flag).                               │                                      │
    │ 263 │ run-external             │ system       │ false     │ false     │ Runs external command                │                                      │
    │ 264 │ save                     │ filesystem   │ false     │ false     │ Save a file.                         │                                      │
    │ 265 │ select                   │ filters      │ false     │ false     │ Down-select table to only these      │                                      │
    │     │                          │              │           │           │ columns.                             │                                      │
    │ 266 │ seq                      │ generators   │ false     │ false     │ Print sequences of numbers.          │                                      │
    │ 267 │ seq date                 │ generators   │ false     │ false     │ print sequences of dates             │                                      │
    │ 268 │ shells                   │ shells       │ false     │ false     │ Lists all open shells.               │                                      │
    │ 269 │ shuffle                  │ filters      │ false     │ false     │ Shuffle rows randomly.               │                                      │
    │ 270 │ size                     │ strings      │ false     │ false     │ Gather word count statistics on the  │                                      │
    │     │                          │              │           │           │ text.                                │                                      │
    │ 271 │ skip                     │ filters      │ false     │ false     │ Skip the first n elements of the     │                                      │
    │     │                          │              │           │           │ input.                               │                                      │
    │ 272 │ skip until               │ filters      │ false     │ false     │ Skip elements of the input until a   │                                      │
    │     │                          │              │           │           │ predicate is true.                   │                                      │
    │ 273 │ skip while               │ filters      │ false     │ false     │ Skip elements of the input while a   │                                      │
    │     │                          │              │           │           │ predicate is true.                   │                                      │
    │ 274 │ sleep                    │ platform     │ false     │ false     │ Delay for a specified amount of      │                                      │
    │     │                          │              │           │           │ time.                                │                                      │
    │ 275 │ sort-by                  │ filters      │ false     │ false     │ Sort by the given columns, in        │                                      │
    │     │                          │              │           │           │ increasing order.                    │                                      │
    │ 276 │ source                   │ core         │ false     │ false     │ Runs a script file in the current    │                                      │
    │     │                          │              │           │           │ context.                             │                                      │
    │ 277 │ split                    │ strings      │ false     │ false     │ Split contents across desired        │                                      │
    │     │                          │              │           │           │ subcommand (like row, column) via    │                                      │
    │     │                          │              │           │           │ the separator.                       │                                      │
    │ 278 │ split chars              │ strings      │ false     │ false     │ splits a string's characters into    │                                      │
    │     │                          │              │           │           │ separate rows                        │                                      │
    │ 279 │ split column             │ strings      │ false     │ false     │ splits contents across multiple      │                                      │
    │     │                          │              │           │           │ columns via the separator.           │                                      │
    │ 280 │ split row                │ strings      │ false     │ false     │ splits contents over multiple rows   │                                      │
    │     │                          │              │           │           │ via the separator.                   │                                      │
    │ 281 │ split-by                 │ default      │ false     │ false     │ Create a new table splitted.         │                                      │
    │ 282 │ str                      │ strings      │ false     │ false     │ Various commands for working with    │                                      │
    │     │                          │              │           │           │ string data.                         │                                      │
    │ 283 │ str camel-case           │ strings      │ false     │ false     │ converts a string to camelCase       │                                      │
    │ 284 │ str capitalize           │ strings      │ false     │ false     │ capitalizes text                     │                                      │
    │ 285 │ str collect              │ strings      │ false     │ false     │ creates a string from the input,     │                                      │
    │     │                          │              │           │           │ optionally using a separator         │                                      │
    │ 286 │ str contains             │ strings      │ false     │ false     │ Checks if string contains pattern    │                                      │
    │ 287 │ str downcase             │ strings      │ false     │ false     │ downcases text                       │                                      │
    │ 288 │ str ends-with            │ strings      │ false     │ false     │ checks if string ends with pattern   │                                      │
    │ 289 │ str find-replace         │ strings      │ false     │ false     │ finds and replaces text              │                                      │
    │ 290 │ str index-of             │ strings      │ false     │ false     │ Returns starting index of given      │                                      │
    │     │                          │              │           │           │ pattern in string counting from 0.   │                                      │
    │     │                          │              │           │           │ Returns -1 when there are no         │                                      │
    │     │                          │              │           │           │ results.                             │                                      │
    │ 291 │ str kebab-case           │ strings      │ false     │ false     │ converts a string to kebab-case      │                                      │
    │ 292 │ str length               │ strings      │ false     │ false     │ outputs the lengths of the strings   │                                      │
    │     │                          │              │           │           │ in the pipeline                      │                                      │
    │ 293 │ str lpad                 │ strings      │ false     │ false     │ pad a string with a character a      │                                      │
    │     │                          │              │           │           │ certain length                       │                                      │
    │ 294 │ str pascal-case          │ strings      │ false     │ false     │ converts a string to PascalCase      │                                      │
    │ 295 │ str reverse              │ strings      │ false     │ false     │ outputs the reversals of the         │                                      │
    │     │                          │              │           │           │ strings in the pipeline              │                                      │
    │ 296 │ str rpad                 │ strings      │ false     │ false     │ pad a string with a character a      │                                      │
    │     │                          │              │           │           │ certain length                       │                                      │
    │ 297 │ str screaming-snake-case │ strings      │ false     │ false     │ converts a string to                 │                                      │
    │     │                          │              │           │           │ SCREAMING_SNAKE_CASE                 │                                      │
    │ 298 │ str snake-case           │ strings      │ false     │ false     │ converts a string to snake_case      │                                      │
    │ 299 │ str starts-with          │ strings      │ false     │ false     │ checks if string starts with         │                                      │
    │     │                          │              │           │           │ pattern                              │                                      │
    │ 300 │ str substring            │ default      │ false     │ false     │ substrings text                      │                                      │
    │ 301 │ str to-datetime          │ deprecated   │ false     │ false     │ Deprecated command                   │                                      │
    │ 302 │ str to-decimal           │ deprecated   │ false     │ false     │ Deprecated command                   │                                      │
    │ 303 │ str to-int               │ deprecated   │ false     │ false     │ Deprecated command                   │                                      │
    │ 304 │ str trim                 │ default      │ false     │ false     │ trims text                           │                                      │
    │ 305 │ str upcase               │ default      │ false     │ false     │ upcases text                         │                                      │
    │ 306 │ sys                      │ system       │ false     │ false     │ View information about the system.   │                                      │
    │ 307 │ table                    │ viewers      │ false     │ false     │ Render the table.                    │                                      │
    │ 308 │ term size                │ platform     │ false     │ false     │ Returns the terminal size            │                                      │
    │ 309 │ to                       │ formats      │ false     │ false     │ Translate structured data to a       │                                      │
    │     │                          │              │           │           │ format                               │                                      │
    │ 310 │ to csv                   │ formats      │ false     │ false     │ Convert table into .csv text         │                                      │
    │ 311 │ to html                  │ formats      │ false     │ false     │ Convert table into simple HTML       │                                      │
    │ 312 │ to json                  │ formats      │ false     │ false     │ Converts table data into JSON text.  │                                      │
    │ 313 │ to md                    │ formats      │ false     │ false     │ Convert table into simple Markdown   │                                      │
    │ 314 │ to nuon                  │ experimental │ false     │ false     │ Converts table data into Nuon        │                                      │
    │     │                          │              │           │           │ (Nushell Object Notation) text.      │                                      │
    │ 315 │ to toml                  │ formats      │ false     │ false     │ Convert table into .toml text        │                                      │
    │ 316 │ to tsv                   │ formats      │ false     │ false     │ Convert table into .tsv text         │                                      │
    │ 317 │ to url                   │ formats      │ false     │ false     │ Convert table into url-encoded text  │                                      │
    │ 318 │ to xml                   │ formats      │ false     │ false     │ Convert table into .xml text         │                                      │
    │ 319 │ to yaml                  │ formats      │ false     │ false     │ Convert table into .yaml/.yml text   │                                      │
    │ 320 │ touch                    │ filesystem   │ false     │ false     │ Creates one or more files.           │                                      │
    │ 321 │ transpose                │ default      │ false     │ false     │ Transposes the table contents so     │                                      │
    │     │                          │              │           │           │ rows become columns and columns      │                                      │
    │     │                          │              │           │           │ become rows.                         │                                      │
    │ 322 │ tutor                    │ core         │ false     │ false     │ Run the tutorial. To begin, run:     │                                      │
    │     │                          │              │           │           │ tutor                                │                                      │
    │ 323 │ unalias                  │ deprecated   │ false     │ false     │ Deprecated command                   │                                      │
    │ 324 │ uniq                     │ filters      │ false     │ false     │ Return the unique rows.              │                                      │
    │ 325 │ update                   │ filters      │ false     │ false     │ Update an existing column to have a  │                                      │
    │     │                          │              │           │           │ new value.                           │                                      │
    │ 326 │ update cells             │ filters      │ false     │ false     │ Update the table cells.              │                                      │
    │ 327 │ upsert                   │ filters      │ false     │ false     │ Update an existing column to have a  │                                      │
    │     │                          │              │           │           │ new value, or insert a new column.   │                                      │
    │ 328 │ url                      │ network      │ false     │ false     │ Apply url function.                  │                                      │
    │ 329 │ url host                 │ network      │ false     │ false     │ gets the host of a url               │                                      │
    │ 330 │ url path                 │ network      │ false     │ false     │ gets the path of a url               │                                      │
    │ 331 │ url query                │ network      │ false     │ false     │ gets the query of a url              │                                      │
    │ 332 │ url scheme               │ network      │ false     │ false     │ gets the scheme (eg http, file) of   │                                      │
    │     │                          │              │           │           │ a url                                │                                      │
    │ 333 │ use                      │ core         │ false     │ false     │ Use definitions from a module        │                                      │
    │ 334 │ version                  │ default      │ false     │ false     │ Display Nu version.                  │                                      │
    │ 335 │ view-source              │ core         │ false     │ false     │ View a block, module, or a           │                                      │
    │     │                          │              │           │           │ definition                           │                                      │
    │ 336 │ where                    │ filters      │ false     │ false     │ Filter values based on a condition.  │                                      │
    │ 337 │ which                    │ system       │ false     │ false     │ Finds a program file, alias or       │                                      │
    │     │                          │              │           │           │ custom command.                      │                                      │
    │ 338 │ window                   │ filters      │ false     │ false     │ Creates a sliding window of          │                                      │
    │     │                          │              │           │           │ `window_size` that slide by n        │                                      │
    │     │                          │              │           │           │ rows/elements across input.          │                                      │
    │ 339 │ with-env                 │ env          │ false     │ false     │ Runs a block with an environment     │                                      │
    │     │                          │              │           │           │ variable set.                        │                                      │
    │ 340 │ wrap                     │ filters      │ false     │ false     │ Wrap the value into a column.        │                                      │
    │ 341 │ zip                      │ filters      │ false     │ false     │ Combine a stream with the input      │                                      │
    ├─────┼──────────────────────────┼──────────────┼───────────┼───────────┼──────────────────────────────────────┼──────────────────────────────────────┤
    │  #  │           name           │   category   │ is_plugin │ is_custom │                usage                 │             extra_usage              │
    ╰─────┴──────────────────────────┴──────────────┴───────────┴───────────┴──────────────────────────────────────┴──────────────────────────────────────╯


