# Purpose
This C source code file is part of a chess-related software library, specifically handling the creation and manipulation of chess moves. The file provides functions to create moves, compare them, and convert them to and from the Universal Chess Interface (UCI) string format. The primary functions include [`moveSq`](#moveSq), which creates a basic move between two squares; [`movePromote`](#movePromote), which creates a move with an optional promotion piece; and [`moveEq`](#moveEq), which checks if two moves are equivalent. Additionally, the file includes [`moveGetUci`](#moveGetUci), which converts a move into its UCI string representation, and [`moveFromUci`](#moveFromUci), which parses a UCI string to create a move object. The code is designed to be part of a larger chess library, as indicated by the inclusion of "chesslib/move.h", and it provides essential functionality for handling chess moves in a programmatic way.

The file is not a standalone executable but rather a component of a larger system, likely intended to be used in conjunction with other parts of a chess engine or application. It defines a narrow set of functionalities focused on move operations, which are crucial for any chess software that needs to process and validate moves, especially in formats compatible with UCI, a common protocol used in chess engines. The code does not include error checking for UCI string parsing, which suggests that it assumes valid input or that error handling is managed elsewhere in the system.
# Imports and Dependencies

---
- `stdio.h`
- `stdlib.h`
- `ctype.h`
- `chesslib/move.h`


# Functions

---
### moveSq<!-- {{#callable:moveSq}} -->
The `moveSq` function creates a move from one square to another without any promotion in a chess game.
- **Inputs**:
    - `from`: The starting square of the move, represented by the type `sq`.
    - `to`: The destination square of the move, represented by the type `sq`.
- **Control Flow**:
    - The function calls [`movePromote`](#movePromote) with the `from` and `to` squares and `ptEmpty` as the promotion type.
    - The [`movePromote`](#movePromote) function constructs a `move` structure with the given `from`, `to`, and `promotion` values.
    - The constructed `move` is returned by [`movePromote`](#movePromote) and subsequently by `moveSq`.
- **Output**:
    - A `move` structure representing a move from the `from` square to the `to` square with no promotion.
- **Functions called**:
    - [`movePromote`](#movePromote)


---
### movePromote<!-- {{#callable:movePromote}} -->
The `movePromote` function creates and returns a `move` structure initialized with the given starting square, destination square, and promotion piece type.
- **Inputs**:
    - `from`: The starting square of the move, represented by the type `sq`.
    - `to`: The destination square of the move, represented by the type `sq`.
    - `promotion`: The type of piece to which a pawn is promoted, represented by the type `pieceType`.
- **Control Flow**:
    - A `move` structure `m` is declared.
    - The `from` field of `m` is set to the input `from`.
    - The `to` field of `m` is set to the input `to`.
    - The `promotion` field of `m` is set to the input `promotion`.
    - The function returns the `move` structure `m`.
- **Output**:
    - The function returns a `move` structure initialized with the specified `from`, `to`, and `promotion` values.


---
### moveEq<!-- {{#callable:moveEq}} -->
The `moveEq` function checks if two chess moves are equivalent by comparing their starting and ending squares and promotion types.
- **Inputs**:
    - `m1`: The first move to compare, represented as a `move` structure.
    - `m2`: The second move to compare, represented as a `move` structure.
- **Control Flow**:
    - The function calls [`sqEq`](square.c.driver.md#sqEq) to compare the `from` squares of `m1` and `m2`.
    - It then calls [`sqEq`](square.c.driver.md#sqEq) to compare the `to` squares of `m1` and `m2`.
    - Finally, it checks if the `promotion` fields of `m1` and `m2` are equal.
    - The function returns the logical AND of these three comparisons.
- **Output**:
    - The function returns a `uint8_t` value, which is `1` if the moves are equivalent and `0` otherwise.
- **Functions called**:
    - [`sqEq`](square.c.driver.md#sqEq)


---
### moveGetUci<!-- {{#callable:moveGetUci}} -->
The `moveGetUci` function generates a UCI (Universal Chess Interface) string representation of a given chess move, including promotion if applicable.
- **Inputs**:
    - `m`: A `move` structure containing the source square, destination square, and optional promotion piece type.
- **Control Flow**:
    - Initialize a character array `p` with two elements set to zero.
    - Check if the move includes a promotion piece type.
    - If there is a promotion, convert the promotion piece type to a lowercase letter and store it in `p[0]`, then allocate memory for a 6-character string.
    - If there is no promotion, allocate memory for a 5-character string.
    - Use `sprintf` to format the move's source square, destination square, and promotion letter into the allocated string.
    - Return the formatted string.
- **Output**:
    - A dynamically allocated string representing the UCI format of the move, which must be freed by the caller.
- **Functions called**:
    - [`pieceTypeGetLetter`](piece.c.driver.md#pieceTypeGetLetter)
    - [`sqGetStr`](square.c.driver.md#sqGetStr)


---
### moveFromUci<!-- {{#callable:moveFromUci}} -->
The `moveFromUci` function converts a UCI (Universal Chess Interface) string into a `move` structure, representing a chess move with optional promotion.
- **Inputs**:
    - `uci`: A string representing a chess move in UCI format, which typically consists of four characters for the starting and ending squares, and optionally a fifth character for promotion.
- **Control Flow**:
    - Extracts the first two characters from the `uci` string to form the `from` square and the next two characters to form the `to` square.
    - Initializes a `promotion` variable of type `pieceType` to determine if the move includes a promotion.
    - Uses a `switch` statement to check the fifth character of the `uci` string to set the `promotion` type, defaulting to `ptEmpty` if no valid promotion character is found.
    - Creates a `move` structure `m`, setting its `from` and `to` fields using the [`sqS`](square.c.driver.md#sqS) function to convert the square strings, and its `promotion` field to the determined promotion type.
    - Returns the constructed `move` structure `m`.
- **Output**:
    - The function returns a `move` structure representing the chess move described by the UCI string, including the starting and ending squares and any promotion type.
- **Functions called**:
    - [`sqS`](square.c.driver.md#sqS)


