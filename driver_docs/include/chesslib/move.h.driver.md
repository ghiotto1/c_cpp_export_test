# Purpose
This C header file defines structures and functions related to chess move operations, likely as part of a larger chess application. It includes necessary dependencies from other modules, specifically `square.h` and `piece.h`, which suggest that it relies on predefined types for squares and pieces. The `move` structure encapsulates a chess move, including the starting and ending squares and an optional promotion piece type. The file declares functions for creating moves ([`moveSq`](#moveSq) and [`movePromote`](#movePromote)), comparing moves ([`moveEq`](#moveEq)), and converting moves to and from UCI (Universal Chess Interface) notation ([`moveGetUci`](#moveGetUci) and [`moveFromUci`](#moveFromUci)). This header is designed to facilitate the manipulation and representation of chess moves within the application.
# Imports and Dependencies

---
- `chesslib/square.h`
- `chesslib/piece.h`


# Data Structures

---
### move
- **Type**: `struct`
- **Members**:
    - `from`: The starting square of the move.
    - `to`: The destination square of the move.
    - `promotion`: The type of piece to promote to, if applicable.
- **Description**: The `move` structure represents a chess move, encapsulating the starting and destination squares, as well as the type of piece to promote to if the move involves a pawn promotion. This structure is fundamental in representing and manipulating chess moves within the program, allowing for operations such as move creation, comparison, and conversion to UCI notation.


# Function Declarations (Public API)

---
### moveSq<!-- {{#callable_declaration:moveSq}} -->
Creates a move from one square to another without promotion.
- **Description**: Use this function to create a move structure representing a chess move from one square to another without any piece promotion. This function is typically used when a piece is moved on the board without changing its type, such as moving a pawn forward without reaching the promotion rank. Ensure that the squares provided are valid and represent positions on the chessboard.
- **Inputs**:
    - `from`: The starting square of the move. Must be a valid square on the chessboard.
    - `to`: The destination square of the move. Must be a valid square on the chessboard.
- **Output**: Returns a move structure with the specified from and to squares, and no promotion.
- **See also**: [`moveSq`](../../src/chesslib/move.c.driver.md#moveSq)  (Implementation)


---
### movePromote<!-- {{#callable_declaration:movePromote}} -->
Creates a move with a promotion from one square to another.
- **Description**: This function constructs a chess move that includes a promotion, specifying the starting square, the destination square, and the type of piece to promote to. It is typically used when a pawn reaches the opposite end of the board and is promoted to another piece. The function returns a move structure encapsulating these details. Ensure that the 'from' and 'to' squares are valid board positions and that the promotion piece type is appropriate for a promotion (e.g., not a pawn or king).
- **Inputs**:
    - `from`: The starting square of the move. Must be a valid square on the chessboard.
    - `to`: The destination square of the move. Must be a valid square on the chessboard.
    - `promotion`: The type of piece to promote to. Should be a valid piece type for promotion, typically a queen, rook, bishop, or knight.
- **Output**: Returns a move structure representing the move from the starting square to the destination square with the specified promotion.
- **See also**: [`movePromote`](../../src/chesslib/move.c.driver.md#movePromote)  (Implementation)


---
### moveEq<!-- {{#callable_declaration:moveEq}} -->
Compares two chess moves for equality.
- **Description**: Use this function to determine if two chess moves are identical in terms of their starting and ending squares, as well as any promotion involved. This function is useful when you need to check if two moves are the same in a chess game context. It requires both moves to be fully specified, including the promotion piece type if applicable. The function returns a non-zero value if the moves are equal and zero if they are not.
- **Inputs**:
    - `m1`: The first move to compare. It must be a valid move structure with defined 'from', 'to', and 'promotion' fields.
    - `m2`: The second move to compare. It must also be a valid move structure with defined 'from', 'to', and 'promotion' fields.
- **Output**: Returns a non-zero value if the moves are equal, otherwise returns zero.
- **See also**: [`moveEq`](../../src/chesslib/move.c.driver.md#moveEq)  (Implementation)


---
### moveGetUci<!-- {{#callable_declaration:moveGetUci}} -->
Converts a chess move to its UCI notation string.
- **Description**: This function generates a string representing a chess move in UCI (Universal Chess Interface) notation. It should be used when you need a textual representation of a move for logging, communication, or processing purposes. The function allocates memory for the resulting string, which includes the starting and ending squares of the move, and appends the promotion piece type if applicable. The caller is responsible for freeing the allocated memory to avoid memory leaks. Ensure that the move structure is properly initialized before calling this function.
- **Inputs**:
    - `m`: A move structure containing the starting square, ending square, and an optional promotion piece type. The structure must be properly initialized, and the squares must be valid chessboard positions. If the promotion field is non-zero, it should represent a valid piece type for promotion.
- **Output**: A dynamically allocated string containing the UCI notation of the move. The caller must free this string after use.
- **See also**: [`moveGetUci`](../../src/chesslib/move.c.driver.md#moveGetUci)  (Implementation)


---
### moveFromUci<!-- {{#callable_declaration:moveFromUci}} -->
Converts a UCI string to a move structure.
- **Description**: This function is used to convert a Universal Chess Interface (UCI) formatted string into a move structure, which includes the starting and ending squares and any promotion piece type. It is typically called when parsing moves from a UCI string representation. The function expects a valid UCI string of at least four characters, representing the starting and ending squares, and optionally a fifth character for promotion. If the promotion character is not provided or is invalid, no promotion is assumed. The function does not handle null pointers and expects the input string to be properly formatted.
- **Inputs**:
    - `uci`: A pointer to a null-terminated string representing a move in UCI format. The string must be at least four characters long, with the first two characters representing the starting square and the next two representing the ending square. An optional fifth character can specify a promotion piece ('n', 'b', 'r', 'q', 'k'). The caller retains ownership of the string, and it must not be null.
- **Output**: A move structure containing the parsed starting and ending squares and the promotion piece type, if specified.
- **See also**: [`moveFromUci`](../../src/chesslib/move.c.driver.md#moveFromUci)  (Implementation)


