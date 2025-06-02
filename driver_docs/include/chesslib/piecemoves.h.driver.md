# Purpose
This C source code file is part of a chess engine, specifically focusing on defining the movement logic for various chess pieces. It provides a set of functions that generate potential moves for each type of chess piece, including pawns, knights, bishops, rooks, queens, and kings. The file includes functions for both "leaper" pieces, which can move to specific squares based on predefined offsets (such as knights), and "rider" pieces, which can continue moving in a direction until they encounter an obstacle (such as bishops, rooks, and queens). The functions return a `moveList`, which is presumably a data structure that holds potential moves for a piece on a given board state. This file is intended to be included in other parts of the chess engine, as indicated by the `#pragma once` directive, which prevents multiple inclusions.

The code is organized around the concept of generating potential moves, which are not necessarily legal moves, as they might leave the player in check. This suggests that the file is part of a larger system where move validation and game rules are handled elsewhere. The inclusion of headers like "chesslib/board.h" and "chesslib/movelist.h" indicates that this file relies on external data structures and functions defined in those headers, likely for representing the chessboard and managing lists of moves. The file does not define public APIs or external interfaces directly but provides essential internal functionality for the chess engine's move generation subsystem.
# Imports and Dependencies

---
- `chesslib/board.h`
- `chesslib/movelist.h`


# Global Variables

---
### pmLeaperMoveList
- **Type**: `function`
- **Description**: The `pmLeaperMoveList` function is designed to generate a list of potential moves for a leaper piece on a chessboard. It takes a board, a starting square, a piece type, an array of directional offsets, and the number of directions as parameters. The function returns a moveList, which contains all possible moves for the leaper based on the given directions.
- **Use**: This function is used to calculate and return all potential moves for leaper-type chess pieces, such as knights, based on specified directional offsets.


---
### pmRiderMoveList
- **Type**: `function pointer`
- **Description**: The `pmRiderMoveList` is a function pointer that returns a pointer to a `moveList` structure. It is used to generate a list of potential moves for a rider piece on a chessboard, which can move in a fixed direction any number of times until it encounters an obstacle. The function takes a board pointer, a square, a piece type, an array of direction offsets, and the number of directions as parameters.
- **Use**: This function is used to calculate and return a list of potential moves for rider pieces like bishops, rooks, and queens in a chess game.


---
### pmGetPawnMoves
- **Type**: `function pointer`
- **Description**: The `pmGetPawnMoves` is a function pointer that returns a pointer to a `moveList` structure. It takes two parameters: a pointer to a `board` structure and a `sq` type, which likely represents a square on the chessboard. This function is designed to calculate and return a list of potential moves for a pawn located at a specific square on the given board.
- **Use**: This function is used to determine all possible moves a pawn can make from a given position on the chessboard.


---
### pmGetKnightMoves
- **Type**: `function pointer`
- **Description**: The `pmGetKnightMoves` is a function pointer that returns a pointer to a `moveList` structure. It is designed to calculate and return all potential moves for a knight piece on a chessboard, given the current state of the board and the position of the knight. The function does not account for moves that might leave the player in check.
- **Use**: This function is used to generate a list of all possible moves for a knight piece from a given position on the chessboard.


---
### pmGetBishopMoves
- **Type**: `function pointer`
- **Description**: The `pmGetBishopMoves` is a function pointer that returns a pointer to a `moveList` structure, which represents a list of potential moves for a bishop on a chessboard. It takes two parameters: a pointer to a `board` structure and a `sq` type representing the square on the board where the bishop is located.
- **Use**: This function is used to calculate and return all possible moves for a bishop from a given position on the chessboard.


---
### pmGetRookMoves
- **Type**: `function pointer`
- **Description**: The `pmGetRookMoves` is a function that returns a pointer to a `moveList`, which represents potential moves for a rook piece on a chess board. It takes two parameters: a pointer to a `board` structure and a `sq` type representing the square from which the rook is moving.
- **Use**: This function is used to calculate and return all possible moves for a rook from a given position on the chess board.


---
### pmGetQueenMoves
- **Type**: `function pointer`
- **Description**: The `pmGetQueenMoves` is a function pointer that returns a pointer to a `moveList` structure. It takes two parameters: a pointer to a `board` structure and a `sq` type, which likely represents a square on the chessboard. This function is designed to generate a list of potential moves for a queen piece on a given board position.
- **Use**: This function is used to calculate and return all possible moves for a queen from a specific square on the chessboard.


---
### pmGetKingMoves
- **Type**: `function pointer`
- **Description**: The `pmGetKingMoves` is a function pointer that returns a pointer to a `moveList` structure. It takes two parameters: a pointer to a `board` structure and a `sq` type, which likely represents a square on the chessboard. This function is designed to calculate and return all potential moves for a king piece on a given board position.
- **Use**: This function is used to determine the possible moves for a king piece on a chessboard, which can then be evaluated for legality and strategic value.


---
### pmGetPawnAttacks
- **Type**: `function pointer`
- **Description**: The `pmGetPawnAttacks` is a function that returns a pointer to a `moveList`, which represents potential attack moves for a pawn on a chessboard. It takes a pointer to a `board` structure and a square `s` as parameters, indicating the current state of the board and the position of the pawn, respectively.
- **Use**: This function is used to determine and return the possible attack moves for a pawn from a given position on the chessboard.


# Function Declarations (Public API)

---
### pmLeaperMoveList<!-- {{#callable_declaration:pmLeaperMoveList}} -->
Generates a list of potential moves for a leaper piece on a chessboard.
- **Description**: This function is used to determine all potential moves for a leaper piece, such as a knight, on a given chessboard. It requires the current state of the board, the position of the piece, the type of the piece, and an array of directional offsets that define how the piece can move. The function returns a list of potential moves, which may include moves that leave the player in check. It is important to ensure that the piece at the specified position matches the provided piece type before calling this function. The function handles out-of-bounds moves by ignoring them.
- **Inputs**:
    - `b`: A pointer to the board structure representing the current state of the chessboard. Must not be null.
    - `s`: The current position of the piece on the board, represented as a square structure. Must be a valid position on the board.
    - `pt`: The type of the piece for which moves are being generated. Must match the type of the piece at the given position.
    - `dirs`: An array of integer pairs representing the directional offsets for the leaper's movement. Each pair defines a possible move direction.
    - `numDirs`: The number of directional offsets provided in the dirs array. Must be greater than zero.
- **Output**: A pointer to a moveList structure containing the potential moves for the leaper piece. The list may be empty if no valid moves are found.
- **See also**: [`pmLeaperMoveList`](../../src/chesslib/piecemoves.c.driver.md#pmLeaperMoveList)  (Implementation)


---
### pmRiderMoveList<!-- {{#callable_declaration:pmRiderMoveList}} -->
Generates a list of potential moves for a rider piece from a given position.
- **Description**: This function is used to determine all potential moves for a rider-type chess piece (such as a rook, bishop, or queen) from a specified position on the board. It calculates moves in all specified directions until an obstruction is encountered or the edge of the board is reached. The function should be called when you need to evaluate possible moves for a rider piece, taking into account the current board state. It returns a list of potential moves, which may include moves that leave the player in check, so further validation may be necessary.
- **Inputs**:
    - `b`: A pointer to the board structure representing the current state of the chess game. Must not be null.
    - `s`: The starting square from which the rider piece will attempt to move. It should be a valid square on the board.
    - `pt`: The type of the piece expected at the starting square. This is used to verify that the piece at the square matches the expected type.
    - `dirs`: An array of direction offsets, where each direction is represented as a pair of integers indicating file and rank changes. This array defines the directions in which the rider can move.
    - `numDirs`: The number of directions provided in the dirs array. It must be a positive integer that does not exceed the actual size of the dirs array.
- **Output**: A pointer to a moveList structure containing all potential moves for the rider piece from the given position.
- **See also**: [`pmRiderMoveList`](../../src/chesslib/piecemoves.c.driver.md#pmRiderMoveList)  (Implementation)


---
### pmGetPawnMoves<!-- {{#callable_declaration:pmGetPawnMoves}} -->
Generates a list of potential moves for a pawn on a given board square.
- **Description**: This function is used to determine all potential moves for a pawn located at a specific square on a chess board. It should be called when you need to evaluate the possible actions a pawn can take, including forward moves and captures. The function assumes that the board and square are valid and that the square contains a pawn. It returns a move list that may include moves that leave the player in check, so further validation is required to ensure legality in a game context. The function handles both single and double forward moves, as well as diagonal captures, including en passant.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null, and should be properly initialized before calling this function.
    - `s`: A square structure representing the position of the pawn on the board. Must be a valid square on the board and should contain a pawn piece.
- **Output**: A pointer to a moveList structure containing potential moves for the pawn. The list may be empty if no moves are possible.
- **See also**: [`pmGetPawnMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetPawnMoves)  (Implementation)


---
### pmGetKnightMoves<!-- {{#callable_declaration:pmGetKnightMoves}} -->
Returns a list of potential knight moves from a given square on the board.
- **Description**: This function generates and returns a list of all potential moves for a knight piece located at a specified square on the chess board. It is useful for determining the possible moves a knight can make, regardless of whether these moves would leave the player in check. The function should be called when you need to evaluate the knight's movement options from a specific position on the board. Ensure that the board is properly initialized before calling this function.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess board. Must not be null, and should be a valid, initialized board.
    - `s`: The square from which the knight's potential moves are to be calculated. It should be a valid square on the board, typically represented by an integer or an enumeration.
- **Output**: A pointer to a moveList structure containing the potential moves for the knight. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetKnightMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetKnightMoves)  (Implementation)


---
### pmGetBishopMoves<!-- {{#callable_declaration:pmGetBishopMoves}} -->
Generates potential bishop moves from a given square on the board.
- **Description**: This function is used to obtain a list of all potential moves for a bishop located at a specific square on a chess board. It should be called when you need to determine the possible moves a bishop can make, considering the current state of the board. The function returns a move list that includes all potential moves, but it does not account for whether these moves would leave the player's king in check. It is important to ensure that the board is properly initialized before calling this function.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null, and should be properly initialized before calling this function.
    - `s`: The square from which the bishop's potential moves are to be calculated. It should be a valid square on the board, typically represented by an enumeration or integer within the bounds of the board.
- **Output**: A pointer to a moveList structure containing the potential moves for the bishop from the specified square. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetBishopMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetBishopMoves)  (Implementation)


---
### pmGetRookMoves<!-- {{#callable_declaration:pmGetRookMoves}} -->
Generates a list of potential rook moves from a given board position.
- **Description**: This function is used to determine all potential moves for a rook piece located at a specific square on a chess board. It should be called when you need to evaluate the possible moves a rook can make from its current position. The function returns a list of moves that the rook can potentially make, but it does not account for whether these moves would leave the player's king in check. It is important to ensure that the board is properly initialized and that the square corresponds to a valid position on the board before calling this function.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null, and should be properly initialized before calling this function.
    - `s`: The square on the board where the rook is currently located. It should be a valid square within the board's boundaries.
- **Output**: A pointer to a moveList structure containing all potential moves for the rook from the specified square. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetRookMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetRookMoves)  (Implementation)


---
### pmGetQueenMoves<!-- {{#callable_declaration:pmGetQueenMoves}} -->
Generates a list of potential moves for a queen on a chessboard.
- **Description**: This function is used to obtain a list of all potential moves for a queen piece located at a specific square on a given chessboard. It is useful in chess engines or applications that need to calculate possible moves for a queen, considering its ability to move any number of squares along a rank, file, or diagonal. The function does not account for whether the moves leave the current player in check, so additional validation may be necessary. It should be called with a valid board and a square that contains a queen piece.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chessboard. Must not be null, and should be properly initialized before calling this function.
    - `s`: A square on the board where the queen is located. It should be a valid square index within the board's boundaries.
- **Output**: A pointer to a moveList structure containing potential moves for the queen. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetQueenMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetQueenMoves)  (Implementation)


---
### pmGetKingMoves<!-- {{#callable_declaration:pmGetKingMoves}} -->
Generates a list of potential king moves from a given square on the board.
- **Description**: This function is used to determine all potential moves a king can make from a specified square on a chess board. It is useful for evaluating possible king movements during a game, but it does not account for moves that would leave the king in check. The function should be called with a valid board state and a square that contains a king. The caller is responsible for ensuring that the square is within the bounds of the board and that the board is properly initialized.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null and should be properly initialized before calling this function.
    - `s`: The square from which to calculate the king's potential moves. It should be a valid square on the board, and ideally, it should contain a king piece.
- **Output**: A pointer to a moveList structure containing the potential moves for the king from the specified square. The list may include moves that place the king in check.
- **See also**: [`pmGetKingMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetKingMoves)  (Implementation)


---
### pmGetPawnAttacks<!-- {{#callable_declaration:pmGetPawnAttacks}} -->
Generates a list of potential attack moves for a pawn on a given square.
- **Description**: This function is used to determine the potential attack moves for a pawn located at a specific square on the chess board. It should be called when you need to evaluate the attacking capabilities of a pawn, considering the pawn's color and position. The function returns a list of moves that represent possible attacks, which may not necessarily be legal in terms of leaving the player in check. It is important to ensure that the square provided contains a pawn, as the function will return an empty move list if the piece on the square is not a pawn.
- **Inputs**:
    - `b`: A pointer to the board structure representing the current state of the chess game. Must not be null, and the board should be properly initialized before calling this function.
    - `s`: The square on the board where the pawn is located. It should be a valid square within the board's boundaries, and ideally, it should contain a pawn piece. If the square does not contain a pawn, the function will return an empty move list.
- **Output**: Returns a pointer to a moveList structure containing potential attack moves for the pawn. The list may be empty if the square does not contain a pawn or if there are no valid attack moves.
- **See also**: [`pmGetPawnAttacks`](../../src/chesslib/piecemoves.c.driver.md#pmGetPawnAttacks)  (Implementation)


