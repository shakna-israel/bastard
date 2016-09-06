# Beautifully Absurd Syntax and ARgumentative Dialogue

An esoteric language, inspired by Brainfuck and Fortran.

---

## Notes

BASTARD has been designed, re-designed and re-structured again and again.

However, the specification found at [Specification.md](Specification.md), is currently accepted, and will not under go any large changes from now on.

BASTARD was developed to be used for "Real Work", though it is highly impractical. (Those funding it have finally allowed me to release the Spec into the wild.)

A few features of note:

* Can only read files with a name length of 1. (This is under review and may change.)
* Has no branching evaluation, such as if or case switching.
* Does have a conditional looping construct. (Which kinda allows you to do a clumsy if.)
* Can read from stdin.
* Can output to stderr, stdout in both ASCII and UTF-8.

---

## Hello, World!

"Hello, World!" is usually the first program anybody writes, but can be a pain in the butt to write in many estoric languages.

However, here lies a simple version in BASTARD, fully commented:

```
Sets the current cell to the ASCII for the letter "H".
A 72

Moves to the next cell, and sets it to the ASCII for the letter "e"
! 01
A 99
A 02

Moves to the next cell, and sets it to the ASCII for the letter "l"
! 01
A 99
A 09

Moves to the next cell, and sets it to the ASCII for the letter "l"
! 01
A 99
A 09

Moves to the next cell, and sets it to the ASCII for the letter "o"
! 01
A 99
A 12

Moves to the next cell, and sets it to the ASCII for the symbol ","
! 01
A 44

Moves to the next cell, and sets it to the ASCII for the symbol " "
! 01
A 32

Moves to the next cell, and sets it to the ASCII for the letter "W"
! 01
A 87

Moves to the next cell, and sets it to the ASCII for the letter "o"
! 01
A 99
A 12

Moves to the next cell, and sets it to the ASCII for the letter "r"
! 01
A 99
A 15

Moves to the next cell, and sets it to the ASCII for the letter "l"
! 01
A 99
A 09

Moves to the next cell, and sets it to the ASCII for the letter "d"
! 01
A 99
A 01

Moves to the next cell, and sets it to the ASCII for the letter "!"
! 01
A 33

Sets the output port to stdout, using ASCII.
R 01

Loops through till the loop cell is 13.
! 01
D 13

Selects a Cell the loop number backwards from the loop cell.
? 00

Prints the cell to stdout, with no line ending
T 00

Selects the loop cell and increments it by one.
; 00
A 1
```

Or without the comments:

```
A 72 ! 01 A 99 A 02 ! 01 A 99 A 09 ! 01 A 99 A 09 ! 01 A 99 A 12 ! 01 A 44 ! 01 A 32 ! 01 A 87 ! 01 A 99 A 12 ! 01 A 99 A 15 ! 01 A 99 A 09 ! 01 A 99 A 01 ! 01 A 33 R 01 ! 01 D 13 ? 00 T 00 ; 00 A 1
```

198 characters for a "Hello, World!" is incredibly verbose, but not as much as some estoric languages.

As you can see, BASTARD is designed for obfuscation, not for "code golf".

---

## Implementation

There is a reference implementation to be found in the [implementation](implementation) folder.

---

## License

All rights reserved, (c) 2016, James Milne.

The Specification is released under the Creative Commons Attribution 4.0 International license. (See [LICENSE.md](LICENSE.md)).

The reference implementation includes its own license file, see [specification/LICENSE.md](specification/LICENSE.md).
