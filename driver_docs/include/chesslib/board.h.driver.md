# Purpose
This C header file defines the structure and functionality for managing a chess board within a chess application. It provides a comprehensive set of functions and data structures to represent the state of a chess game, including the positions of pieces, the current player, castling rights, and other game-specific details. The file includes definitions for creating and initializing a board, either from scratch or from a Forsyth-Edwards Notation (FEN) string, which is a standard notation for describing a particular board position. The header also includes functions for manipulating the board, such as setting and getting pieces, generating possible moves, and checking for conditions like check or insufficient material.

The file is designed to be a part of a larger chess library, as indicated by the inclusion of other headers like "square.h", "piece.h", and "movelist.h". It defines a public API for interacting with the board, allowing other parts of the program to create and manipulate board states. The use of bitmasks for castling rights and functions for comparing board states suggest a focus on efficiency and precise control over game state management. This header file is essential for any chess application that requires detailed and accurate representation and manipulation of the game board.
# Imports and Dependencies

---
- `chesslib/square.h`
- `chesslib/piece.h`
- `chesslib/movelist.h`


# Global Variables

---
### boardCreate
- **Type**: `function`
- **Description**: The `boardCreate` function is a global function that allocates and initializes a new chess board structure, returning a pointer to this newly created board. It is designed to set up a board with the initial chess position and must be freed after use to avoid memory leaks.
- **Use**: This function is used to create a new chess board instance, initialized to the standard starting position, for use in a chess game application.


---
### boardCreateFromFen
- **Type**: `function`
- **Description**: The `boardCreateFromFen` function is a global function that allocates and initializes a chess board based on a given FEN (Forsyth-Edwards Notation) string. It returns a pointer to a `board` structure, which represents the state of a chess game, or NULL if the initialization fails.
- **Use**: This function is used to create a new chess board from a FEN string, allowing the game state to be set up from a specific position.


---
### boardGenerateMoves
- **Type**: `function pointer`
- **Description**: The `boardGenerateMoves` is a function that takes a pointer to a `board` structure as an argument and returns a pointer to a `moveList` structure. This function is responsible for generating all possible legal moves for the current player on the given chess board.
- **Use**: This function is used to calculate and retrieve all potential moves for the current player based on the current state of the chess board.


---
### boardPlayMove
- **Type**: `function`
- **Description**: The `boardPlayMove` function is a global function that takes a pointer to a `board` structure and a `move` as parameters. It returns a new `board` structure where the specified move has been applied to the given board. This function is part of a chess library and is used to simulate the effect of a move on a chess board, creating a new board state as a result.
- **Use**: This function is used to apply a move to a chess board and return the resulting board state.


---
### boardGetFen
- **Type**: `function`
- **Description**: The `boardGetFen` function is a global function that takes a pointer to a `board` structure as its parameter and returns a string representing the board's state in Forsyth-Edwards Notation (FEN). FEN is a standard notation for describing a particular board position of a chess game. This function is essential for serializing the board state into a human-readable format that can be used for saving, sharing, or analyzing the game state.
- **Use**: This function is used to convert the current state of a chess board into a FEN string for external use or storage.


# Data Structures

---
### board
- **Type**: `struct`
- **Members**:
    - `pieces`: An array of 64 `piece` elements representing the chess pieces on the board.
    - `currentPlayer`: A `pieceColor` indicating which player's turn it is to move.
    - `castleState`: A `uint8_t` bitmask that describes the castling rights for both players.
    - `epTarget`: A `sq` representing the en passant target square, if applicable.
    - `halfMoveClock`: An `unsigned int` tracking the number of half-moves since the last capture or pawn move.
    - `moveNumber`: An `unsigned int` indicating the current move number in the game.
- **Description**: The `board` structure is a comprehensive representation of a chess game state, encapsulating the positions of all pieces on the board, the current player's turn, castling rights, en passant target square, and move counters. It is designed to facilitate the management and manipulation of a chess game, providing the necessary data to track game progress and enforce rules such as castling and en passant. The structure is integral to functions that initialize, modify, and evaluate the board state, supporting operations like move generation and validation.


# Function Declarations (Public API)

---
### boardCreate<!-- {{#callable_declaration:boardCreate}} -->
Allocates and initializes a chess board to the standard starting position.
- **Description**: This function creates a new chess board initialized to the standard starting position, as defined by the Forsyth-Edwards Notation (FEN) string for the initial setup of a chess game. It returns a pointer to the newly allocated board structure. The caller is responsible for freeing the allocated memory when it is no longer needed. This function is useful for setting up a new game of chess with the standard initial configuration. It is expected to be called when a new game is started, and it handles any necessary memory allocation internally.
- **Inputs**:
    - None
- **Output**: A pointer to a newly allocated and initialized board structure, or NULL if the allocation fails.
- **See also**: [`boardCreate`](../../src/chesslib/board.c.driver.md#boardCreate)  (Implementation)


---
### boardCreateFromFen<!-- {{#callable_declaration:boardCreateFromFen}} -->
Creates a chess board from a FEN string.
- **Description**: This function allocates memory for a new chess board and initializes it using the provided FEN (Forsyth-Edwards Notation) string, which describes a particular board position. It is useful for setting up a board to a specific state as described by the FEN. The function returns a pointer to the newly created board, or NULL if the initialization fails. The caller is responsible for freeing the allocated memory when the board is no longer needed. This function should be used when a specific board setup is required, and it is important to ensure that the FEN string is valid to avoid initialization failure.
- **Inputs**:
    - `fen`: A null-terminated string representing the board position in Forsyth-Edwards Notation. The string must be valid and correctly formatted, as invalid FEN strings will cause the function to return NULL.
- **Output**: Returns a pointer to a newly allocated and initialized board, or NULL if the FEN string is invalid or initialization fails.
- **See also**: [`boardCreateFromFen`](../../src/chesslib/board.c.driver.md#boardCreateFromFen)  (Implementation)


---
### boardInitInPlace<!-- {{#callable_declaration:boardInitInPlace}} -->
Initializes a chess board to the standard starting position.
- **Description**: This function sets up the provided chess board structure to represent the initial position of a standard chess game. It should be used when you want to reset or initialize a board to the starting configuration. The function must be called with a valid pointer to a `board` structure, which it will modify in place. Ensure that the board structure is properly allocated before calling this function.
- **Inputs**:
    - `b`: A pointer to a `board` structure that will be initialized. Must not be null, and the caller retains ownership of the memory. The function modifies the board in place to represent the initial chess position.
- **Output**: None
- **See also**: [`boardInitInPlace`](../../src/chesslib/board.c.driver.md#boardInitInPlace)  (Implementation)


---
### boardInitFromFenInPlace<!-- {{#callable_declaration:boardInitFromFenInPlace}} -->
Initializes a chess board from a FEN string in place.
- **Description**: This function sets up a chess board based on the provided FEN (Forsyth-Edwards Notation) string, directly modifying the given board structure. It should be used when you want to initialize or reset a board to a specific state described by a FEN string. The function expects a valid FEN string and a pre-allocated board structure. It returns an error code if the FEN string is malformed or if any part of the board setup fails. The function modifies the board's pieces, current player, castling rights, en passant target square, half-move clock, and full move number based on the FEN data.
- **Inputs**:
    - `b`: A pointer to a pre-allocated board structure that will be initialized. The caller retains ownership and must ensure it is valid and properly allocated.
    - `fen`: A null-terminated string containing the FEN representation of the board state. It must not be null and should be a valid FEN string. Invalid FEN strings will result in an error code being returned.
- **Output**: Returns 0 on successful initialization, or 1 if an error occurs due to an invalid FEN string.
- **See also**: [`boardInitFromFenInPlace`](../../src/chesslib/board.c.driver.md#boardInitFromFenInPlace)  (Implementation)


---
### boardSetPiece<!-- {{#callable_declaration:boardSetPiece}} -->
Sets a piece on the specified square of the board.
- **Description**: This function places a specified chess piece on a given square of the board. It is typically used to update the board state during gameplay or setup. The board must be properly initialized before calling this function. The function does not perform any validation on the square or piece, so it is the caller's responsibility to ensure that the square is within valid bounds and the piece is a valid chess piece. This function directly modifies the board's state.
- **Inputs**:
    - `b`: A pointer to the board structure where the piece will be placed. Must not be null and should point to a valid, initialized board.
    - `s`: The square on the board where the piece will be placed. It should be a valid square within the board's bounds.
    - `p`: The chess piece to place on the specified square. It should be a valid piece as defined in the chess library.
- **Output**: None
- **See also**: [`boardSetPiece`](../../src/chesslib/board.c.driver.md#boardSetPiece)  (Implementation)


---
### boardGetPiece<!-- {{#callable_declaration:boardGetPiece}} -->
Retrieve the piece located at a specific square on the board.
- **Description**: Use this function to obtain the piece that is currently positioned on a specified square of the chess board. This function is useful when you need to inspect the board's state or validate moves. It requires a valid board pointer and a square identifier. Ensure that the board has been properly initialized before calling this function to avoid undefined behavior.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null and should point to a valid, initialized board.
    - `s`: An identifier for the square on the board from which to retrieve the piece. Must be a valid square within the board's boundaries.
- **Output**: The piece located at the specified square on the board.
- **See also**: [`boardGetPiece`](../../src/chesslib/board.c.driver.md#boardGetPiece)  (Implementation)


---
### boardGenerateMoves<!-- {{#callable_declaration:boardGenerateMoves}} -->
Generates all legal moves for the current player on the board.
- **Description**: This function generates a list of all legal moves available to the current player on the given chess board. It should be called when you need to determine the possible actions a player can take in their turn. The function considers all pieces of the current player, including special moves like castling, and excludes moves that would leave the player in check. The caller is responsible for freeing the returned move list to avoid memory leaks.
- **Inputs**:
    - `b`: A pointer to a 'board' structure representing the current state of the chess game. Must not be null. The board should be properly initialized and represent a valid game state.
- **Output**: A pointer to a 'moveList' structure containing all legal moves for the current player. The list is dynamically allocated and must be freed by the caller.
- **See also**: [`boardGenerateMoves`](../../src/chesslib/board.c.driver.md#boardGenerateMoves)  (Implementation)


---
### boardIsSquareAttacked<!-- {{#callable_declaration:boardIsSquareAttacked}} -->
Determines if a square is attacked by a specified color.
- **Description**: Use this function to check if a specific square on the chess board is under attack by any piece of a given color. This is useful for determining threats and planning moves in a chess game. The function requires a valid board state and a square to check, along with the color of the potential attacker. It returns a non-zero value if the square is attacked, and zero if it is not. Ensure that the board is properly initialized before calling this function.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null and should be properly initialized.
    - `s`: The square to check for attacks. It should be a valid square on the board.
    - `attacker`: The color of the pieces to check for attacks. Must be a valid pieceColor value representing either white or black.
- **Output**: Returns a non-zero value if the square is attacked by the specified color, otherwise returns zero.
- **See also**: [`boardIsSquareAttacked`](../../src/chesslib/board.c.driver.md#boardIsSquareAttacked)  (Implementation)


---
### boardIsInCheck<!-- {{#callable_declaration:boardIsInCheck}} -->
Checks if the current player is in check.
- **Description**: Use this function to determine if the player whose turn it is currently is in check on the given chess board. This function is useful for validating game states and ensuring that moves do not leave the player's king in check. It should be called after the board has been properly initialized and set up for a game. The function assumes that the board structure is correctly populated and that the currentPlayer field accurately reflects the player whose turn it is.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. The board must be properly initialized and must not be null. The function does not modify the board.
- **Output**: Returns a non-zero value if the current player is in check, and zero if not.
- **See also**: [`boardIsInCheck`](../../src/chesslib/board.c.driver.md#boardIsInCheck)  (Implementation)


---
### boardIsPlayerInCheck<!-- {{#callable_declaration:boardIsPlayerInCheck}} -->
Determines if the specified player is in check on the given board.
- **Description**: This function checks whether the player of the specified color is currently in check on the provided chess board. It should be used when you need to verify the check status of a player during a game. The function requires a valid board pointer and a player color as inputs. It iterates over the board to find the player's king and checks if it is under attack by any opposing pieces. The function assumes that the board is correctly set up and that the player color is valid. It returns a non-zero value if the player is in check, and zero otherwise.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null, and should be properly initialized.
    - `player`: The color of the player to check, either pcWhite or pcBlack. Must be a valid pieceColor value.
- **Output**: Returns 1 if the specified player is in check, otherwise returns 0.
- **See also**: [`boardIsPlayerInCheck`](../../src/chesslib/board.c.driver.md#boardIsPlayerInCheck)  (Implementation)


---
### boardIsInsufficientMaterial<!-- {{#callable_declaration:boardIsInsufficientMaterial}} -->
Determines if a chess board position has insufficient material to checkmate.
- **Description**: This function checks whether the given chess board position is such that neither player has enough material to force a checkmate, resulting in a draw. It should be used when you need to determine if the game can be declared a draw due to insufficient material. The function assumes that the board is correctly initialized and contains valid chess pieces. It handles standard cases of insufficient material, such as only kings remaining, or a king with a single minor piece (knight or bishop), or only bishops on the same color. The function does not handle more complex scenarios beyond these standard cases.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null and should be properly initialized with valid chess pieces. The function does not modify the board.
- **Output**: Returns 1 if the position is a draw due to insufficient material, otherwise returns 0.
- **See also**: [`boardIsInsufficientMaterial`](../../src/chesslib/board.c.driver.md#boardIsInsufficientMaterial)  (Implementation)


---
### boardPlayMove<!-- {{#callable_declaration:boardPlayMove}} -->
Returns a new board with the specified move applied.
- **Description**: Use this function to create a new board state by applying a move to an existing board. This function is useful when you need to preserve the original board state and work with a modified version. It allocates memory for a new board, copies the current board state, applies the move, and returns the new board. The caller is responsible for freeing the allocated memory for the new board to avoid memory leaks. Ensure that the input board is valid and the move is legal within the context of the game rules.
- **Inputs**:
    - `b`: A pointer to the current board state. Must not be null and should represent a valid game state.
    - `m`: The move to be applied to the board. It should be a legal move according to the game rules.
- **Output**: A pointer to a new board with the move applied. The caller is responsible for freeing this memory.
- **See also**: [`boardPlayMove`](../../src/chesslib/board.c.driver.md#boardPlayMove)  (Implementation)


---
### boardPlayMoveInPlace<!-- {{#callable_declaration:boardPlayMoveInPlace}} -->
Executes a chess move on the given board, updating its state in place.
- **Description**: This function applies a specified chess move to an existing board, directly modifying the board's state to reflect the move. It should be used when you want to update the board without creating a new instance. The function handles special moves such as castling, en passant, and pawn promotion, and updates relevant game state variables like the half-move clock, move number, and castling rights. It assumes the board is in a valid state and the move is legal. The function does not return a value, so it is important to ensure the board and move are correctly set up before calling this function.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null, and the board should be properly initialized before calling this function. The function modifies this board in place.
    - `m`: A move structure representing the chess move to be played. The move should be valid and legal according to the current state of the board.
- **Output**: None
- **See also**: [`boardPlayMoveInPlace`](../../src/chesslib/board.c.driver.md#boardPlayMoveInPlace)  (Implementation)


---
### boardEq<!-- {{#callable_declaration:boardEq}} -->
Determine if two chess boards are identical in all aspects.
- **Description**: Use this function to check if two chess board states are completely identical, including the current player, castle state, en passant target square, half-move clock, move number, and the arrangement of pieces on the board. This function is useful for validating board states in applications such as chess engines or game state verification. It is important to ensure that both board pointers are valid and point to properly initialized board structures before calling this function. The function returns a boolean-like value indicating equality.
- **Inputs**:
    - `b1`: A pointer to the first board structure to compare. Must not be null and should point to a valid, initialized board.
    - `b2`: A pointer to the second board structure to compare. Must not be null and should point to a valid, initialized board.
- **Output**: Returns 1 if the boards are identical in all aspects, otherwise returns 0.
- **See also**: [`boardEq`](../../src/chesslib/board.c.driver.md#boardEq)  (Implementation)


---
### boardEqContext<!-- {{#callable_declaration:boardEqContext}} -->
Compares two chess boards for equality, ignoring move counters and filtering en passant target squares.
- **Description**: Use this function to determine if two chess board states are equivalent in terms of player turn, castling rights, piece positions, and valid en passant targets, while ignoring move counters. This function is useful when you need to compare board states for game logic purposes, such as detecting repeated positions or validating moves, without considering the half-move clock or move number. Ensure that both board pointers are valid and initialized before calling this function. The function returns a non-zero value if the boards are considered equal under these conditions, and zero otherwise.
- **Inputs**:
    - `b1`: A pointer to the first board structure to compare. Must not be null and should be properly initialized.
    - `b2`: A pointer to the second board structure to compare. Must not be null and should be properly initialized.
- **Output**: Returns 1 if the boards are equal in terms of player turn, castling rights, piece positions, and valid en passant targets; returns 0 otherwise.
- **See also**: [`boardEqContext`](../../src/chesslib/board.c.driver.md#boardEqContext)  (Implementation)


---
### boardGetFen<!-- {{#callable_declaration:boardGetFen}} -->
Generates a FEN string representing the current state of the chess board.
- **Description**: This function creates a Forsyth-Edwards Notation (FEN) string that describes the current state of the given chess board. It is useful for saving the board state or for interoperability with other chess software that uses FEN. The function allocates memory for the FEN string, which the caller is responsible for freeing. It assumes that the input board is properly initialized and contains valid game state information. The function handles all aspects of the FEN format, including piece placement, active color, castling availability, en passant target square, halfmove clock, and fullmove number.
- **Inputs**:
    - `b`: A pointer to a 'board' structure representing the current state of the chess game. Must not be null and should be properly initialized with valid game state data.
- **Output**: A dynamically allocated string containing the FEN representation of the board. The caller is responsible for freeing this string.
- **See also**: [`boardGetFen`](../../src/chesslib/board.c.driver.md#boardGetFen)  (Implementation)


