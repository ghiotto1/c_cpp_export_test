# Purpose
This C source code file provides functionality for handling chessboard squares, encapsulating operations related to the representation and manipulation of squares on a standard 8x8 chessboard. The code defines several functions that allow for the creation and manipulation of square objects, which are represented by the `sq` type. The primary operations include creating a square from file and rank integers ([`sqI`](#sqI)), from a Standard Algebraic Notation (SAN) string ([`sqS`](#sqS)), and from an index ([`sqIndex`](#sqIndex)). Additionally, the code provides utility functions to retrieve the SAN string representation of a square ([`sqGetStr`](#sqGetStr)), determine if a square is dark or light ([`sqIsDark`](#sqIsDark)), and compare two squares for equality ([`sqEq`](#sqEq)).

The file is part of a larger library, as indicated by the inclusion of the header file "chesslib/square.h", suggesting that it is intended to be used as part of a chess-related software system. The code defines a set of public APIs that facilitate the conversion between different representations of chessboard squares, ensuring that operations remain within the valid bounds of a chessboard. The use of constants and utility functions like `SQ_STRS` and [`sqGetIndex`](#sqGetIndex) further supports efficient and accurate square manipulation, making this file a focused and essential component for any chess application requiring square-based operations.
# Imports and Dependencies

---
- `chesslib/square.h`


# Global Variables

---
### SQ\_STRS
- **Type**: `const char *[64]`
- **Description**: `SQ_STRS` is a global constant array of 64 string literals, each representing a square on a standard 8x8 chessboard using algebraic notation. The array elements are ordered from 'a1' to 'h8', covering all possible squares on the board.
- **Use**: This array is used to map indices to their corresponding square names in algebraic notation, facilitating conversion between index-based and string-based square representations.


# Functions

---
### sqI<!-- {{#callable:sqI}} -->
The function `sqI` creates a chessboard square object from given file and rank values, ensuring they are within valid bounds.
- **Inputs**:
    - `file`: An unsigned 8-bit integer representing the file (column) of the chessboard square, expected to be between 1 and 8.
    - `rank`: An unsigned 8-bit integer representing the rank (row) of the chessboard square, expected to be between 1 and 8.
- **Control Flow**:
    - Check if the `file` is less than 1 or greater than 8, or if the `rank` is less than 1 or greater than 8.
    - If any of the above conditions are true, return `SQ_INVALID`.
    - If both `file` and `rank` are within valid bounds, create a `sq` object `s`.
    - Assign the `file` value to `s.file` and the `rank` value to `s.rank`.
    - Return the `sq` object `s`.
- **Output**:
    - The function returns a `sq` object representing a valid chessboard square if the inputs are within bounds, otherwise it returns `SQ_INVALID`.


---
### sqS<!-- {{#callable:sqS}} -->
The function `sqS` converts a string representing a chessboard square in SAN format to a `sq` structure with file and rank values.
- **Inputs**:
    - `str`: A pointer to a constant character string representing a chessboard square in SAN format (e.g., "e4").
- **Control Flow**:
    - Extract the first character `c1` from the input string `str`.
    - Check if `c1` is a valid file character ('a' to 'h'); if not, return `SQ_INVALID`.
    - Extract the second character `c2` from the input string `str`.
    - Check if `c2` is a valid rank character ('1' to '8'); if not, return `SQ_INVALID`.
    - Create a `sq` structure `s` and set its `file` field to the numeric value corresponding to `c1` ('a' = 1, ..., 'h' = 8).
    - Set the `rank` field of `s` to the numeric value of `c2` ('1' = 1, ..., '8' = 8).
    - Return the `sq` structure `s`.
- **Output**:
    - The function returns a `sq` structure representing the file and rank of the chessboard square, or `SQ_INVALID` if the input string is not a valid SAN square.


---
### sqIndex<!-- {{#callable:sqIndex}} -->
The `sqIndex` function converts a given index into a chessboard square using a predefined array of square strings.
- **Inputs**:
    - `index`: An unsigned 8-bit integer representing the index of the square, expected to be between 0 and 63 inclusive.
- **Control Flow**:
    - Check if the input index is less than 0 or greater than 63.
    - If the index is out of bounds, return `SQ_INVALID`.
    - If the index is valid, use it to access the `SQ_STRS` array to get the corresponding square string.
    - Call the [`sqS`](#sqS) function with the retrieved square string to convert it into a `sq` type and return it.
- **Output**:
    - The function returns a `sq` type representing the chessboard square corresponding to the given index, or `SQ_INVALID` if the index is out of bounds.
- **Functions called**:
    - [`sqS`](#sqS)


---
### sqGetIndex<!-- {{#callable:sqGetIndex}} -->
The function `sqGetIndex` calculates the zero-based index of a chessboard square given its file and rank.
- **Inputs**:
    - `s`: A structure representing a square on a chessboard, containing two fields: `file` and `rank`, both of which are expected to be integers between 1 and 8 inclusive.
- **Control Flow**:
    - Check if the `file` or `rank` of the square `s` is outside the valid range (1 to 8); if so, return -1 indicating an invalid square.
    - Calculate the index using the formula `(8 * (s.rank - 1)) + (s.file - 1)` which maps the 2D coordinates to a 1D array index.
- **Output**:
    - The function returns a `uint8_t` representing the zero-based index of the square on a chessboard, or -1 if the square is invalid.


---
### sqGetStr<!-- {{#callable:sqGetStr}} -->
The `sqGetStr` function returns the Standard Algebraic Notation (SAN) string representation of a given chess square.
- **Inputs**:
    - `s`: A chess square represented by the `sq` type, which contains file and rank information.
- **Control Flow**:
    - Call the [`sqGetIndex`](#sqGetIndex) function with the input square `s` to get its index.
    - Check if the index is greater than 63; if so, return the string '##' indicating an invalid square.
    - If the index is valid (0 to 63), return the corresponding SAN string from the `SQ_STRS` array.
- **Output**:
    - A constant character pointer to the SAN string representing the square, or '##' if the square is invalid.
- **Functions called**:
    - [`sqGetIndex`](#sqGetIndex)


---
### sqIsDark<!-- {{#callable:sqIsDark}} -->
The `sqIsDark` function determines if a given chessboard square is dark-colored based on its rank and file.
- **Inputs**:
    - `s`: A `sq` structure representing a square on a chessboard, containing `rank` and `file` fields.
- **Control Flow**:
    - The function uses bitwise AND to check the least significant bit of both the `rank` and `file` fields of the square `s`.
    - It then applies the XOR operation to these bits to determine if they are different.
    - The result of the XOR operation is negated to return 1 if the square is dark and 0 if it is light.
- **Output**:
    - Returns 1 if the square is dark-colored, otherwise returns 0.


---
### sqEq<!-- {{#callable:sqEq}} -->
The `sqEq` function checks if two chessboard squares are equal, considering invalid squares.
- **Inputs**:
    - `s1`: The first square to compare, represented by a structure with 'file' and 'rank' attributes.
    - `s2`: The second square to compare, also represented by a structure with 'file' and 'rank' attributes.
- **Control Flow**:
    - Check if the 'file' or 'rank' of 's1' is outside the valid range (1 to 8); if so, set 's1' to 'SQ_INVALID'.
    - Check if the 'file' or 'rank' of 's2' is outside the valid range (1 to 8); if so, set 's2' to 'SQ_INVALID'.
    - Compare the 'file' and 'rank' of 's1' and 's2' to determine if they are equal.
- **Output**:
    - Returns 1 if the squares are equal (both 'file' and 'rank' match), otherwise returns 0.


