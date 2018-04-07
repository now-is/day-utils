# day-utils

day-utils are two command line tools:

day-range outputs a sequence of consecutive dates.
day-format rewrites dates in various formats.

## Prerequisites

[lua 5.1+](https://www.lua.org/) or [luajit 2.0.5](http://luajit.org/), the [LPeg](http://www.inf.puc-rio.br/~roberto/lpeg/) library.

## Installation

Copy day-range and day-format somewhere in your path, edit their first lines if necessary, make them executable.

## Usage: day-range

```bash
day-range sunday .. + 3 days
```

Will print 4 dates on stdout, in YYYY-MM-DD format, of the coming Sunday through the Wednesday after it.

```bash
day-range apr 23
```

will print YYYY-04-23, where YYYY is the current year.

day-range is insensitive to the case of arguments. For the kinds of date specifications understood by day-range, run ./t/run and read t/results-obtained.

## Usage: day-format

```bash
day-range sunday .. +3d | day-format weekdaynamelong, monthnamelong dayshort
```

day-format eads YYYY-MM-DD dates on stdin and writes them to stdout formatted according to its arguments.

Arguments are concatenated (with space characters as cement) into a formatting specification. Certain designated substrings in the specification, or "template", are substituted with components of the date being processed, and the result is written to stdout on a line by itself.

The formatting specification could be seen as a readable version of a strftime string.

To see all strings with special meaning to day-format, run:

```bash
day-format menu
```

This can be used to set up command-line completion for a shell.
