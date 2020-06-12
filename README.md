# day-utils

day-utils are two command line tools: day-range outputs a sequence of consecutive dates, day-format rewrites dates in various formats.

## Prerequisites

[lua 5.1+](https://www.lua.org/) or [luajit 2.0.5](http://luajit.org/), the [LPeg](http://www.inf.puc-rio.br/~roberto/lpeg/) library.

## Installation

Copy `day-range` and `day-format` somewhere in your path, edit their first lines if necessary, make them executable.

## Usage: day-range

```bash
day-range sunday .. + 3 days
```

will print four dates on stdout, in `YYYY-MM-DD` format, of the coming Sunday through the Wednesday after it.

```bash
day-range apr 23
```

will print `YYYY-04-23`, where `YYYY` is the current year.

day-range is insensitive to the case of arguments. For the kinds of date specifications understood by day-range, run `./t/run` and read `./t/results-obtained`.

## Usage: day-format

```bash
day-range sunday .. +3d | day-format Friday, October 15th
```

day-format reads `YYYY-MM-DD` dates on stdin and writes them to stdout formatted according to its arguments.

Arguments are concatenated, with spaces as cement, into a formatting specification. Certain substrings in the specification are substituted with components of the date being processed, and the result is written to stdout on a line by itself.

The formatting specification could be seen as a readable version of a `strftime` string. In the grand tradition of programming languages, it is entirely English-centric.

Certain substrings of decimal digits are replaced with the following values:

* `1`, `2`, ... `9`: the numeric day
* `10`, `11`, `12`: the numeric month, two digits, with leading `0` if needed
* `13`, `14`, ... `31`: the numeric day, two digits, with leading `0` if needed
* `2000` ... `9999`: the year, four digits; this formatter is not Y10K-safe
* `10000` and above: the unix epoch

Longer substrings get preference.

Other substrings with special meaning, and what they are replaced with:

* `1st`, `2nd` ... `9th`: the numeric day with ordinal English suffix
* `13th` ... `31st`: the numeric day with ordinal English suffix, four characters, with leading `0` if needed
* `January` ... `December`: English month name
* `Jan` ... `Dec`: three-character abbreviation of English month name
* `Sunday` ... `Saturday`: English day of week
* `Sun` ... `Sat`: three-character abbreviation of English day of week

Note:

* The format string is not tokenized
* Any ordinal suffix works with any qualifying numeral: `1th`, `9rd`, `22st` are valid
* All-lowercase versions of month and day names also work and have the same meaning

