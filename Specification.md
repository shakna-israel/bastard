# Specification

Herein lies the specification for the language formally known as "Beautifully Absurd SynTax and ARgumentative Dialogue", herein referred to as "BASTARD".

## Internals

There are exactly 4 internal types that BASTARD is required to represent.

### Integer

An "Integer" is an object that stores a number, a user can represent by exactly two digits, ranging from 00 to 99.

However, despite the represention, any length number can be formed, using the "Functions" within the Standard Library.

### Cell

A "Cell" is an object that can store values of the "Integer" type.

BASTARD, at the beginning of interpretation, generates 30,000 of these "Cells".

Each "Cell" must be accessible through a function, as seen in the Standard Library.

Each "Cell" must be seemingly mutable, as the "Integer" it stores can change. (Though implementations may use immutable data in a way not immediate obviousto end users).

### Port

A BASTARD "Port" is a type that abstracts connection to the Operating System, in a particular way.

These connections are:

* stdout
* stderr
* stdin
* Files resting in the Operating System's file system

### Function

A "Function" is represented by a single ASCII character, and takes a single, mandatory "Integer".

The definitions of behaviour for the "Functions" can be found in the Standard Library.

## Standard Library

BASTARD has a series of functions immediately exposed to the implementation, called the Standard Library.

### B

This "Function" is represented by the ASCII character, B

It takes a single "Integer".

When called, the "Function" changes the currently selected "Cell", based on the "Integer" provided.

If the "Integer" is larger than the number of "Cells" provided, the selector wraps, back to the beginning.

#### Examples

```
B 12
```

This selects the 12th "Cell".

```
B 30005
```

This selects the 5th "Cell".

### A

This "Function" is represented by the ASCII character, A

It takes a single "Integer".

When called, this "Function" increments the value stored in the current "Cell" by the provided "Integer".

#### Examples

Assuming a newly initiated "Cell":

```
A 26
```

The selected "Cell", changes from 00, where it began, to 26.

If we, using the same "Cell" again:

```
A 99
```

Then the selected "Cell", becomes 125.

### S

This "Function" is represented by the ASCII character, S

It takes a single "Integer".

When called, this "Function" decrements the value stored in the current "Cell" by the provided "Integer".

#### Examples

Assuming a "Cell" with a value of 125:

```
S 26
```

The selected "Cell", changes from 125 to 99.

If we, using the same "Cell" again:

```
S 99
```

Then the selected "Cell", becomes 00.

### T

This "Function" is represented by the ASCII character, T

It takes a single "Integer".

When called, this "Function" sends the current value of the selected "Cell" to the selected "Port".

The provided "Integer" has no effect, and exists for consistency's sake.

See "R" or "Ports" for more information.

#### Examples

Assuming the currently selected "Port" represents stdout:

Also assuming lines beginning with "$" to be input, and lines beginning with ">" to represent printed output to stdout, without a line ending character.

Also assuming the current selected "Cell" contains 65.

```
$ T 99
> A
```

If instead, we assumed the selected "Cell" contained 01:

```
$ T 67
> 1
```

### R

This "Function" is represented by the ASCII character, R

It takes a single "Integer".

When called, this "Function" behaves slightly differently, based on the provided "Integer".

#### "Integer" == 00

When the "Integer" provided is equal to 00, it changes the selected "Port" to stderr, and coerces all future output to stderr by BASTARD to output as ASCII.

#### "Integer" == 01

When the "Integer" provided is equal to 01, it changes the selected "Port" to stdout, and coerces all future output to stdout by BASTARD to output as ASCII.

#### "Integer" == 02

When the "Integer" provided is equal to 02, it reads exactly two characters from stdin, converting them from their ASCII representation to an "Integer" and adds them to the currently selected "Cell".

#### "Integer" == 03

When the "Integer" provided is equal to 03, it reads from a file in the Operating System's filesystem. 

The file to be read is relative to the Current Working Directory, where BASTARD was launched. 

The file to be read is found by converting the contents of the currently selected "Cell" to ASCII, and using it as a path.

The entire contents of the file is then read, converting each character therin from their ASCII representation to an "Integer" and adds them to a "Cell" adjacent positively to the currently selected "Cell".

#### "Integer" == 04

When the "Integer" provided is equal to 04, it changes the selected "Port" to stderr, and coerces all future output to stderr by BASTARD to output as UTF-8.

#### "Integer" == 05

When the "Integer" provided is equal to 05, it changes the selected "Port" to stdout, and coerces all future output to stdout by BASTARD to output as UTF-8.

#### "Integer" == 06

When the "Integer" provided is equal to 06, it reads exactly two characters from stdin, converting them from their UTF-8 representation to an "Integer" and adds them to the currently selected "Cell".

#### "Integer" == 07

When the "Integer" provided is equal to 07, it reads from a file in the Operating System's filesystem. 

The file to be read is relative to the Current Working Directory, where BASTARD was launched. 

The file to be read is found by converting the contents of the currently selected "Cell" to UTF-8, and using it as a path.

The entire contents of the file is then read, converting each character therin from their UTF-8 representation to an "Integer" and adds them to a "Cell" adjacent positively to the currently selected "Cell".

#### Limitations

Firstly, many implementations may not wish to deal with UTF-8, and thus Ports 04, 05, 06 and 07 may not exist!

Secondly, a cursory glance at the File Ports reveals that they can only provided a single character, and so BASTARD can only read files in the relative folder, whose names are only one character long.

This is highly unfortunate, but the cost of so consistent a language.

The specification may be changed to accomodate greater usefulness in the future.

### D

This "Function" is represented by the ASCII character, D

It takes a single "Integer".

When called, this "Function" generates a loop construct, that only exits, once the value of the "Cell" that had been selected at call-time of the loop generator reaches the same value as the "Integer" provided.

### ?

This "Function" is represented by the ASCII character, ?

It takes a single "Integer".

Unless within a loop construct, this "Function" does nothing.

Within a loop construct, it selects a "Cell" that is negative to the first "Cell" the loop was called on, by the number the "Integer" the loop was given, negative the number of times the loop has happened.

When the resulting number is negative, the selection happens in the opposite direction.

### ;

This "Function" is represented by the ASCII character, ;

It takes a single "Integer".

Unless within a loop construct, this "Function" does nothing.

Within a loop construct, it selects the "Cell" that the loop was first called on.

### !

This "Function" is represented by the ASCII character, !

It takes a single "Integer".

When called, this "Function" selects a "Cell" relative to the current "Cell" by the provided "Integer".

As always, "Cell" selection wraps if the "Cell" trying to be accessed is beyond the number that exist.

#### Examples

If we assume the currently selected "Cell" is the 12th "Cell":

```
! 10
```

We would then have the 22nd "Cell" selected.

### .

This "Function" is represented by the ASCII character, !

It takes a single "Integer".

When called, this "Function" selects a "Cell" relative to the current "Cell" by the provided "Integer", in a negative fashion.

As always, "Cell" selection wraps if the "Cell" trying to be accessed is beyond the number that exist.

#### Examples

If we assume the currently selected "Cell" is the 12th "Cell":

```
. 10
```

We would then have the 2nd "Cell" selected.
