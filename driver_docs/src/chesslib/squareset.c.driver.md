# Purpose
This C source code file implements a simple set of functions to manipulate a "square set," likely used in a chess-related application. The file includes two primary functions: [`sqSetSet`](#sqSetSet) and [`sqSetGet`](#sqSetGet). The [`sqSetSet`](#sqSetSet) function modifies a bit within a `sqSet` data structure, setting or clearing it based on the provided `value`, while ensuring the square is valid. The [`sqSetGet`](#sqSetGet) function retrieves the value of a specific bit from the `sqSet`, again checking for validity. This code is part of a larger library, as indicated by the inclusion of "chesslib/squareset.h", and it uses bitwise operations to efficiently manage the state of chessboard squares.
# Imports and Dependencies

---
- `stdlib.h`
- `chesslib/squareset.h`


# Functions

---
### sqSetSet<!-- {{#callable:sqSetSet}} -->
The function `sqSetSet` modifies a bit in a `sqSet` based on the index of a square and a given value.
- **Inputs**:
    - `ss`: A pointer to a `sqSet`, which is a data structure representing a set of squares.
    - `s`: A square `s` of type `sq`, which is used to determine the bit position to modify in the `sqSet`.
    - `value`: A `uint8_t` value indicating whether to set (1) or clear (0) the bit corresponding to the square `s` in the `sqSet`.
- **Control Flow**:
    - Check if the square `s` is invalid using `sqEq(s, SQ_INVALID)`, and return immediately if it is.
    - Calculate the bit position by shifting 1 left by the index of the square `s` obtained from `sqGetIndex(s)`.
    - If `value` is non-zero, set the bit in `sqSet` at the calculated position using bitwise OR.
    - If `value` is zero, clear the bit in `sqSet` at the calculated position using bitwise AND with the negated bit.
- **Output**: The function does not return a value; it modifies the `sqSet` in place.
- **Functions called**:
    - [`sqEq`](square.c.driver.md#sqEq)
    - [`sqGetIndex`](square.c.driver.md#sqGetIndex)


---
### sqSetGet<!-- {{#callable:sqSetGet}} -->
The function `sqSetGet` retrieves the value of a specific square from a square set, returning 0 if the square is invalid or the bit value at the square's index otherwise.
- **Inputs**:
    - `ss`: A pointer to a `sqSet`, which is a data structure representing a set of squares.
    - `s`: A `sq` type representing a specific square whose value is to be retrieved.
- **Control Flow**:
    - Check if the square `s` is invalid using `sqEq(s, SQ_INVALID)`; if true, return 0.
    - Calculate the index of the square `s` using `sqGetIndex(s)`.
    - Shift the bits of the square set `*ss` right by the index of the square.
    - Perform a bitwise AND operation with 1 to isolate the bit at the square's index.
    - Return the result of the bitwise operation, which is either 0 or 1.
- **Output**: The function returns a `uint8_t` value, which is 0 if the square is invalid or the bit value (0 or 1) at the specified square's index in the square set.
- **Functions called**:
    - [`sqEq`](square.c.driver.md#sqEq)
    - [`sqGetIndex`](square.c.driver.md#sqGetIndex)


