# Purpose
This C header file defines a structure and associated functions for handling chessboard squares. The `sq` struct represents a square on a chessboard using two `uint8_t` values for the file and rank, which are constrained to the range 1-8. The file provides utility functions for creating squares from integer coordinates or Standard Algebraic Notation (SAN) strings, converting squares to and from a linear index (0-63), and obtaining the SAN string representation of a square. Additionally, it includes functions to determine if a square is dark-colored and to compare two squares for equality. The `SQ_INVALID` macro defines an invalid square with both file and rank set to -1, which is useful for error handling or initialization.
# Imports and Dependencies

---
- `stdint.h`


# Global Variables

---
### sqGetStr
- **Type**: `function`
- **Description**: The `sqGetStr` function is a global function that takes a square `sq` as an argument and returns a constant character pointer. This pointer represents the SAN (Standard Algebraic Notation) string of the given square, which is a common notation used in chess to describe board positions.
- **Use**: This function is used to obtain the SAN string representation of a square without needing to free the returned string.


# Data Structures

---
### sq
- **Type**: `struct`
- **Members**:
    - `file`: Represents the file (column) of a square on a chessboard, ranging from 1 to 8.
    - `rank`: Represents the rank (row) of a square on a chessboard, ranging from 1 to 8.
- **Description**: The `sq` struct is a simple data structure used to represent a square on a chessboard, with `file` and `rank` as its members, both of which are 8-bit unsigned integers. The values for `file` and `rank` are expected to be in the range of 1 to 8, corresponding to the columns and rows of a standard chessboard. This struct is used in various functions to create, manipulate, and compare chessboard squares, as well as to convert between different representations of squares, such as index and SAN (Standard Algebraic Notation) strings.


# Function Declarations (Public API)

---
### sqI<!-- {{#callable_declaration:sqI}} -->
Create a square from file and rank values.
- **Description**: This function constructs a square object using the provided file and rank values, which represent positions on a chessboard. It is useful when you need to create a square based on specific file and rank coordinates. The function expects both file and rank to be within the range of 1 to 8, inclusive, corresponding to valid chessboard positions. If either value is outside this range, the function returns a special invalid square constant, SQ_INVALID, indicating an error in the input values.
- **Inputs**:
    - `file`: The file component of the square, representing the column on a chessboard. Valid values are from 1 to 8, inclusive. If the value is outside this range, the function returns SQ_INVALID.
    - `rank`: The rank component of the square, representing the row on a chessboard. Valid values are from 1 to 8, inclusive. If the value is outside this range, the function returns SQ_INVALID.
- **Output**: Returns a square object with the specified file and rank if both are valid; otherwise, returns SQ_INVALID.
- **See also**: [`sqI`](../../src/chesslib/square.c.driver.md#sqI)  (Implementation)


---
### sqS<!-- {{#callable_declaration:sqS}} -->
Creates a square from a SAN string representation.
- **Description**: This function converts a Standard Algebraic Notation (SAN) string, representing a chessboard square, into a `sq` struct. It expects a two-character string where the first character is a file ('a' to 'h') and the second character is a rank ('1' to '8'). If the input string does not conform to this format, the function returns `SQ_INVALID`. This function is useful for parsing chess moves or positions from SAN strings into a structured format for further processing.
- **Inputs**:
    - `str`: A pointer to a null-terminated string representing a chessboard square in SAN format. The string must be exactly two characters long, with the first character being a file ('a' to 'h') and the second a rank ('1' to '8'). The caller retains ownership of the string, and it must not be null. If the string is invalid, the function returns `SQ_INVALID`.
- **Output**: Returns a `sq` struct representing the square if the input is valid, or `SQ_INVALID` if the input string is not a valid SAN square.
- **See also**: [`sqS`](../../src/chesslib/square.c.driver.md#sqS)  (Implementation)


---
### sqIndex<!-- {{#callable_declaration:sqIndex}} -->
Converts an index to a square representation.
- **Description**: This function converts a given index, ranging from 0 to 63, into a square structure representing a position on a chessboard. It is useful for translating linear index values into two-dimensional board coordinates. The function returns a special invalid square if the provided index is outside the valid range, ensuring that invalid inputs are safely handled.
- **Inputs**:
    - `index`: An unsigned 8-bit integer representing the index of the square, expected to be in the range 0 to 63. If the index is outside this range, the function returns an invalid square.
- **Output**: Returns a square structure corresponding to the given index, or an invalid square if the index is out of range.
- **See also**: [`sqIndex`](../../src/chesslib/square.c.driver.md#sqIndex)  (Implementation)


---
### sqGetIndex<!-- {{#callable_declaration:sqGetIndex}} -->
Converts a square to its corresponding index on a chessboard.
- **Description**: This function calculates the zero-based index of a given square on a chessboard, where the index ranges from 0 to 63. It is useful for mapping a square's file and rank to a single linear index, which can be used in array representations of a chessboard. The function expects the square's file and rank to be within the range of 1 to 8, inclusive. If the square's file or rank is outside this range, the function returns -1, indicating an invalid square.
- **Inputs**:
    - `s`: A square structure containing 'file' and 'rank' fields, both of which must be in the range 1 to 8. If either field is outside this range, the function returns -1. The caller retains ownership of the square structure.
- **Output**: Returns a uint8_t representing the zero-based index of the square on a chessboard, or -1 if the square is invalid.
- **See also**: [`sqGetIndex`](../../src/chesslib/square.c.driver.md#sqGetIndex)  (Implementation)


---
### sqGetStr<!-- {{#callable_declaration:sqGetStr}} -->
Returns the SAN string representation of a given square.
- **Description**: This function provides the Standard Algebraic Notation (SAN) string for a given square, which is useful for representing chessboard positions in a human-readable format. It should be used when you need to convert a square structure into its corresponding SAN string. The function expects a valid square structure as input, and if the square's index is out of the valid range (0-63), it returns a placeholder string "##". The returned string does not require deallocation by the caller.
- **Inputs**:
    - `s`: A square structure representing a position on a chessboard. The square must be valid, with an index in the range 0-63. If the index is outside this range, the function returns "##".
- **Output**: A pointer to a constant character string representing the SAN notation of the square, or "##" if the square is invalid.
- **See also**: [`sqGetStr`](../../src/chesslib/square.c.driver.md#sqGetStr)  (Implementation)


---
### sqIsDark<!-- {{#callable_declaration:sqIsDark}} -->
Determine if a chessboard square is dark-colored.
- **Description**: This function checks whether a given chessboard square, represented by the `sq` structure, is dark-colored. It is useful for applications that need to differentiate between dark and light squares on a chessboard. The function expects the `sq` structure to have `file` and `rank` values within the range of 1 to 8, as these represent valid chessboard coordinates. The function returns 1 if the square is dark and 0 if it is light. It is important to ensure that the `sq` structure is properly initialized with valid values before calling this function.
- **Inputs**:
    - `s`: A structure representing a chessboard square, with `file` and `rank` fields expected to be in the range 1-8. The caller must ensure these values are valid chessboard coordinates.
- **Output**: Returns 1 if the square is dark-colored, and 0 if it is light-colored.
- **See also**: [`sqIsDark`](../../src/chesslib/square.c.driver.md#sqIsDark)  (Implementation)


---
### sqEq<!-- {{#callable_declaration:sqEq}} -->
Compares two chessboard squares for equality.
- **Description**: Use this function to determine if two chessboard squares, represented by the `sq` struct, are equal in terms of their file and rank. The function checks if the file and rank of each square are within the valid range of 1 to 8, inclusive. If either square has a file or rank outside this range, it is considered invalid and set to `SQ_INVALID`. The function then compares the file and rank of the two squares and returns a result indicating whether they are equal. This function is useful in applications where you need to verify if two positions on a chessboard are the same.
- **Inputs**:
    - `s1`: The first square to compare, represented by the `sq` struct. The `file` and `rank` must be in the range 1 to 8. If out of range, it is treated as `SQ_INVALID`.
    - `s2`: The second square to compare, represented by the `sq` struct. The `file` and `rank` must be in the range 1 to 8. If out of range, it is treated as `SQ_INVALID`.
- **Output**: Returns 1 if the squares are equal (same file and rank), or 0 if they are not.
- **See also**: [`sqEq`](../../src/chesslib/square.c.driver.md#sqEq)  (Implementation)


