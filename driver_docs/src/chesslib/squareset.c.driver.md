# Purpose
This C source code file implements a simple set of functions for manipulating a "square set," which is likely a data structure used in a chess-related application. The file includes two primary functions: [`sqSetSet`](#sqSetSet) and [`sqSetGet`](#sqSetGet). The [`sqSetSet`](#sqSetSet) function modifies a bit within a `sqSet` data structure, setting or clearing it based on the provided `value`, while ensuring the square is valid. The [`sqSetGet`](#sqSetGet) function retrieves the value of a specific bit from the `sqSet`, again checking for validity. This code is part of a larger library, as indicated by the inclusion of "chesslib/squareset.h", and it uses bitwise operations to efficiently manage the state of chessboard squares.
# Imports and Dependencies

---
- `stdlib.h`
- `chesslib/squareset.h`


# Functions

---
### sqSetSet<!-- {{#callable:sqSetSet}} -->
The `sqSetSet` function modifies a bit in a square set based on the given square and value.
- **Inputs**:
    - `ss`: A pointer to a `sqSet`, which is a data structure representing a set of squares.
    - `s`: A `sq` type representing a specific square to be modified in the set.
    - `value`: A `uint8_t` value indicating whether to set (1) or clear (0) the bit corresponding to the square `s`.
- **Control Flow**:
    - Check if the square `s` is invalid using `sqEq(s, SQ_INVALID)`, and return immediately if it is.
    - Calculate the bit position for the square `s` using `sqGetIndex(s)` and shift a 1 to that position to create a bitmask.
    - If `value` is non-zero, set the bit in `ss` using the bitwise OR operation with the bitmask.
    - If `value` is zero, clear the bit in `ss` using the bitwise AND operation with the negated bitmask.
- **Output**:
    - The function does not return a value; it modifies the `sqSet` in place.
- **Functions called**:
    - [`sqEq`](square.c.driver.md#sqEq)
    - [`sqGetIndex`](square.c.driver.md#sqGetIndex)


---
### sqSetGet<!-- {{#callable:sqSetGet}} -->
The function `sqSetGet` retrieves the bit value at a specific index in a square set, representing a chessboard state, based on the given square.
- **Inputs**:
    - `ss`: A pointer to a `sqSet`, which is a data structure representing a set of squares on a chessboard.
    - `s`: A `sq` type representing a specific square on the chessboard.
- **Control Flow**:
    - Check if the square `s` is invalid using `sqEq(s, SQ_INVALID)`; if it is invalid, return 0.
    - Calculate the index of the square `s` using `sqGetIndex(s)`.
    - Shift the bits of `*ss` right by the calculated index and perform a bitwise AND with 1 to isolate the bit at that index.
    - Return the isolated bit value, which is either 0 or 1.
- **Output**:
    - The function returns a `uint8_t` value, which is 0 if the square is invalid or if the bit at the specified index is 0, and 1 if the bit at the specified index is 1.
- **Functions called**:
    - [`sqEq`](square.c.driver.md#sqEq)
    - [`sqGetIndex`](square.c.driver.md#sqGetIndex)


