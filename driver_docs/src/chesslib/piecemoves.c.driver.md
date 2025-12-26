# Purpose
This C source code file is part of a chess engine, specifically focusing on the movement logic for different chess pieces. It provides implementations for generating possible moves for each type of chess piece, including pawns, knights, bishops, rooks, queens, and kings. The file defines several functions that calculate valid moves based on the current state of the chessboard, taking into account the rules of chess such as piece-specific movement patterns, capturing logic, and special moves like pawn promotion. The code is structured to avoid circular dependencies by including the necessary header file `chesslib/piecemoves.h`, which likely contains declarations for the functions and types used here.

The file contains helper functions like [`canMoveHere`](#canMoveHere) to determine if a piece can move to a specific square, and [`addPawnMoveToMoveList`](#addPawnMoveToMoveList) to handle pawn promotions. It uses two main movement strategies: "leaper" for pieces like knights and kings, which move to a fixed set of squares, and "rider" for pieces like bishops, rooks, and queens, which can move any number of squares in a direction until blocked. The code is modular, with each piece type having its own function to generate moves, ensuring clarity and maintainability. This file is not an executable but rather a library component intended to be used by other parts of the chess engine to evaluate and execute piece movements.
# Imports and Dependencies

---
- `chesslib/piecemoves.h`


# Global Variables

---
### knightOffsets
- **Type**: `int8_t[8][2]`
- **Description**: The `knightOffsets` variable is a two-dimensional array of integers that represents the possible moves a knight can make on a chessboard. Each sub-array contains two integers, representing the change in file and rank, respectively, for each of the knight's eight possible moves.
- **Use**: This variable is used to calculate the potential new positions a knight can move to from its current position on the chessboard.


---
### bishopOffsets
- **Type**: `int8_t[4][2]`
- **Description**: The `bishopOffsets` variable is a two-dimensional array of integers that represents the possible movement directions for a bishop in a chess game. Each sub-array contains two integers, indicating the change in file and rank for a bishop's diagonal movement on the chessboard.
- **Use**: This variable is used to determine the possible moves for a bishop by providing direction vectors for diagonal movement in the `pmGetBishopMoves` function.


---
### rookOffsets
- **Type**: `int8_t[4][2]`
- **Description**: The `rookOffsets` variable is a two-dimensional array of integers that represents the possible movement directions for a rook in a chess game. Each sub-array contains two integers, where the first integer represents the change in the file (column) and the second integer represents the change in the rank (row).
- **Use**: This variable is used to determine the valid movement directions for a rook piece on a chessboard.


---
### royalOffsets
- **Type**: `int8_t[8][2]`
- **Description**: The `royalOffsets` variable is a two-dimensional array of 8 elements, each containing a pair of integers. These pairs represent the possible movement directions for chess pieces that can move one square in any direction, such as the king and queen. The array includes all eight possible directions: north, northeast, east, southeast, south, southwest, west, and northwest.
- **Use**: This variable is used to determine the movement directions for the king and queen in chess, allowing them to move one square in any of the eight possible directions on the board.


# Functions

---
### canMoveHere<!-- {{#callable:canMoveHere}} -->
The `canMoveHere` function determines if a piece can move to a specified square on the board without encountering a piece of the same color.
- **Inputs**:
    - `b`: A pointer to the board structure representing the current state of the chess board.
    - `s`: The square on the board to which the piece is attempting to move.
    - `ourColor`: The color of the piece attempting to move, represented by the `pieceColor` type.
- **Control Flow**:
    - Retrieve the piece located at square `s` on the board `b` using [`boardGetPiece`](board.c.driver.md#boardGetPiece) function.
    - Check if the retrieved piece is `pEmpty`, indicating the square is empty; if so, return 1 (true) allowing the move.
    - If the square is not empty, get the color of the piece on the square using [`pieceGetColor`](piece.c.driver.md#pieceGetColor).
    - Compare the color of the piece on the square with `ourColor`; if they are different, return 1 (true), otherwise return 0 (false).
- **Output**: Returns an integer value: 1 if the move is possible (either the square is empty or occupied by an opponent's piece), and 0 if the square is occupied by a piece of the same color.
- **Functions called**:
    - [`boardGetPiece`](board.c.driver.md#boardGetPiece)
    - [`pieceGetColor`](piece.c.driver.md#pieceGetColor)


---
### pmLeaperMoveList<!-- {{#callable:pmLeaperMoveList}} -->
The `pmLeaperMoveList` function generates a list of valid moves for leaper-type chess pieces from a given position on the board.
- **Inputs**:
    - `b`: A pointer to the chess board structure, representing the current state of the game.
    - `s`: The current square (position) of the piece on the board, represented as a structure containing file and rank.
    - `pt`: The type of the piece for which the move list is being generated, ensuring the function only processes moves for the correct piece type.
    - `dirs`: A 2D array of integers representing the possible directions the piece can move, with each direction being a pair of file and rank offsets.
    - `numDirs`: The number of directions available in the `dirs` array, indicating how many potential moves need to be evaluated.
- **Control Flow**:
    - Create an empty move list using [`moveListCreate`](movelist.c.driver.md#moveListCreate).
    - Retrieve the piece at the given square `s` on the board `b`.
    - Check if the piece type matches the specified `pt`; if not, return the empty move list.
    - Determine the color of the piece to ensure moves are valid for the piece's color.
    - Iterate over each direction in `dirs` to calculate potential new squares by applying the direction offsets to the current square `s`.
    - Check if the new square is within the bounds of the board (file and rank between 1 and 8).
    - Use [`canMoveHere`](#canMoveHere) to determine if the piece can legally move to the new square, considering the presence of other pieces.
    - If the move is valid, add it to the move list using [`moveListAdd`](movelist.c.driver.md#moveListAdd).
    - Return the populated move list containing all valid moves for the piece.
- **Output**: A pointer to a `moveList` structure containing all valid moves for the leaper piece from the given position.
- **Functions called**:
    - [`moveListCreate`](movelist.c.driver.md#moveListCreate)
    - [`boardGetPiece`](board.c.driver.md#boardGetPiece)
    - [`pieceGetType`](piece.c.driver.md#pieceGetType)
    - [`pieceGetColor`](piece.c.driver.md#pieceGetColor)
    - [`canMoveHere`](#canMoveHere)
    - [`moveListAdd`](movelist.c.driver.md#moveListAdd)
    - [`moveSq`](move.c.driver.md#moveSq)


---
### pmRiderMoveList<!-- {{#callable:pmRiderMoveList}} -->
The `pmRiderMoveList` function generates a list of all possible moves for a rider-type chess piece (like a rook, bishop, or queen) from a given position on the board, considering the piece's movement directions and the board's current state.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: The starting square (`sq` type) from which the piece will attempt to move.
    - `pt`: The type of the piece (`pieceType`) that is expected to be at the starting square.
    - `dirs`: A 2D array of integers representing the possible movement directions for the piece.
    - `numDirs`: The number of directions available in the `dirs` array.
- **Control Flow**:
    - Create a new move list using `moveListCreate()` to store possible moves.
    - Retrieve the piece at the starting square `s` using `boardGetPiece()` and check if its type matches `pt`; if not, return the empty move list.
    - Determine the color of the piece at the starting square.
    - Iterate over each direction in `dirs` to explore potential moves.
    - For each direction, repeatedly move the piece in that direction until it goes off the board or encounters another piece.
    - If the new square is within bounds and the piece can move there (checked using `canMoveHere()`), add the move to the list using `moveListAdd()`.
    - If a piece is encountered that is not empty, stop further movement in that direction.
- **Output**: A pointer to a `moveList` structure containing all valid moves for the rider piece from the starting square.
- **Functions called**:
    - [`moveListCreate`](movelist.c.driver.md#moveListCreate)
    - [`boardGetPiece`](board.c.driver.md#boardGetPiece)
    - [`pieceGetType`](piece.c.driver.md#pieceGetType)
    - [`pieceGetColor`](piece.c.driver.md#pieceGetColor)
    - [`canMoveHere`](#canMoveHere)
    - [`moveListAdd`](movelist.c.driver.md#moveListAdd)
    - [`moveSq`](move.c.driver.md#moveSq)


---
### addPawnMoveToMoveList<!-- {{#callable:addPawnMoveToMoveList}} -->
The `addPawnMoveToMoveList` function adds a pawn move to a move list, handling promotions if the move reaches the first or eighth rank.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure where the move will be added.
    - `oldSq`: The starting square of the pawn, represented as a `sq` structure.
    - `newSq`: The destination square of the pawn, represented as a `sq` structure.
- **Control Flow**:
    - Check if the destination square `newSq` is on the first or eighth rank, indicating a promotion opportunity.
    - If it is a promotion, add four moves to the list, each promoting the pawn to a different piece type: Queen, Rook, Bishop, and Knight.
    - If it is not a promotion, add a regular move from `oldSq` to `newSq` to the list.
- **Output**: The function does not return a value; it modifies the `moveList` pointed to by `list` by adding the appropriate move(s).
- **Functions called**:
    - [`moveListAdd`](movelist.c.driver.md#moveListAdd)
    - [`movePromote`](move.c.driver.md#movePromote)
    - [`moveSq`](move.c.driver.md#moveSq)


---
### pmGetPawnMoves<!-- {{#callable:pmGetPawnMoves}} -->
The `pmGetPawnMoves` function generates a list of all possible legal moves for a pawn located at a given square on a chess board.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: A `sq` structure representing the current position of the pawn on the board.
- **Control Flow**:
    - Create an empty move list using [`moveListCreate`](movelist.c.driver.md#moveListCreate).
    - Retrieve the piece at the given square `s` using [`boardGetPiece`](board.c.driver.md#boardGetPiece).
    - Check if the piece is a pawn; if not, return the empty move list.
    - Determine the pawn's color and set the movement direction (`delta`) based on the color.
    - Calculate the square directly in front of the pawn and check if it is empty; if so, add this move to the list.
    - Check if the pawn is in its initial position and can move two squares forward; if so, add this move to the list.
    - Check for possible captures to the left and right of the pawn's current position, including en passant captures, and add these moves to the list if valid.
    - Return the populated move list.
- **Output**: A pointer to a `moveList` structure containing all possible legal moves for the pawn at the given position.
- **Functions called**:
    - [`moveListCreate`](movelist.c.driver.md#moveListCreate)
    - [`boardGetPiece`](board.c.driver.md#boardGetPiece)
    - [`pieceGetType`](piece.c.driver.md#pieceGetType)
    - [`pieceGetColor`](piece.c.driver.md#pieceGetColor)
    - [`sqI`](square.c.driver.md#sqI)
    - [`addPawnMoveToMoveList`](#addPawnMoveToMoveList)
    - [`canMoveHere`](#canMoveHere)
    - [`sqEq`](square.c.driver.md#sqEq)


---
### pmGetPawnAttacks<!-- {{#callable:pmGetPawnAttacks}} -->
The function `pmGetPawnAttacks` generates a list of potential attack moves for a pawn on a chessboard, considering only diagonal squares where it could attack if an opponent's piece were present.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chessboard.
    - `s`: A `sq` structure representing the current position of the pawn on the board.
- **Control Flow**:
    - Create an empty move list using `moveListCreate()`.
    - Retrieve the piece at the given square `s` using `boardGetPiece(b, s)`.
    - Check if the piece is a pawn using `pieceGetType(p) != ptPawn`; if not, return the empty move list.
    - Determine the pawn's color using `pieceGetColor(p)` and set `delta` to 1 for white pawns and -1 for black pawns.
    - Check if the pawn can attack diagonally to the left (file > 1); if so, calculate the new square and add the move to the list if it's a valid attack square using `canMoveHere(b, newSq, color)`.
    - Check if the pawn can attack diagonally to the right (file < 8); if so, calculate the new square and add the move to the list if it's a valid attack square using `canMoveHere(b, newSq, color)`.
    - Return the move list containing potential attack moves.
- **Output**: A pointer to a `moveList` structure containing potential attack moves for the pawn from its current position.
- **Functions called**:
    - [`moveListCreate`](movelist.c.driver.md#moveListCreate)
    - [`boardGetPiece`](board.c.driver.md#boardGetPiece)
    - [`pieceGetType`](piece.c.driver.md#pieceGetType)
    - [`pieceGetColor`](piece.c.driver.md#pieceGetColor)
    - [`sqI`](square.c.driver.md#sqI)
    - [`canMoveHere`](#canMoveHere)
    - [`moveListAdd`](movelist.c.driver.md#moveListAdd)
    - [`moveSq`](move.c.driver.md#moveSq)


---
### pmGetKnightMoves<!-- {{#callable:pmGetKnightMoves}} -->
The function `pmGetKnightMoves` generates a list of all possible legal moves for a knight located at a given square on a chessboard.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chessboard.
    - `s`: A `sq` structure representing the current position of the knight on the board.
- **Control Flow**:
    - The function calls [`pmLeaperMoveList`](#pmLeaperMoveList) with the board, the knight's current square, the piece type `ptKnight`, the predefined `knightOffsets` array, and the number of directions (8).
    - [`pmLeaperMoveList`](#pmLeaperMoveList) processes these inputs to determine all valid moves for the knight based on its unique movement pattern.
- **Output**: A pointer to a `moveList` structure containing all valid moves for the knight from the given position.
- **Functions called**:
    - [`pmLeaperMoveList`](#pmLeaperMoveList)


---
### pmGetBishopMoves<!-- {{#callable:pmGetBishopMoves}} -->
The `pmGetBishopMoves` function generates a list of all possible moves for a bishop located at a given square on a chessboard.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chessboard.
    - `s`: A `sq` structure representing the current position of the bishop on the board.
- **Control Flow**:
    - The function calls [`pmRiderMoveList`](#pmRiderMoveList) with the board, the bishop's current square, the piece type `ptBishop`, the `bishopOffsets` array, and the number 4 as arguments.
    - The [`pmRiderMoveList`](#pmRiderMoveList) function processes the bishop's movement by iterating over the diagonal directions specified in `bishopOffsets`.
    - For each direction, it continues moving the bishop in that direction until it either reaches the edge of the board or encounters another piece.
    - If the encountered piece is of the opposite color, the move is added to the list and the iteration for that direction stops.
- **Output**: A pointer to a `moveList` structure containing all valid moves for the bishop from the given square.
- **Functions called**:
    - [`pmRiderMoveList`](#pmRiderMoveList)


---
### pmGetRookMoves<!-- {{#callable:pmGetRookMoves}} -->
The function `pmGetRookMoves` generates a list of all possible legal moves for a rook located at a given square on a chess board.
- **Inputs**:
    - `b`: A pointer to the chess board structure representing the current state of the game.
    - `s`: A structure representing the square on the board where the rook is currently located.
- **Control Flow**:
    - The function calls [`pmRiderMoveList`](#pmRiderMoveList) with the board, square, piece type for rook, rook movement offsets, and the number of directions (4) as arguments.
    - [`pmRiderMoveList`](#pmRiderMoveList) handles the logic for generating moves for pieces that can move multiple squares in a straight line, like the rook.
- **Output**: A pointer to a `moveList` structure containing all possible legal moves for the rook from the given square.
- **Functions called**:
    - [`pmRiderMoveList`](#pmRiderMoveList)


---
### pmGetQueenMoves<!-- {{#callable:pmGetQueenMoves}} -->
The function `pmGetQueenMoves` generates a list of all possible legal moves for a queen located at a given square on a chessboard.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chessboard.
    - `s`: A `sq` structure representing the current position of the queen on the board.
- **Control Flow**:
    - The function calls [`pmRiderMoveList`](#pmRiderMoveList) with the board, the queen's current position, the piece type `ptQueen`, the direction offsets for a queen (`royalOffsets`), and the number of directions (8).
    - [`pmRiderMoveList`](#pmRiderMoveList) iterates over each direction in `royalOffsets`, moving the queen in that direction until it either reaches the edge of the board or encounters another piece.
    - If the square is within bounds and either empty or occupied by an opponent's piece, the move is added to the move list.
    - The iteration stops in a direction if a piece is encountered, as the queen cannot move past it.
- **Output**: A pointer to a `moveList` structure containing all possible legal moves for the queen from the given position.
- **Functions called**:
    - [`pmRiderMoveList`](#pmRiderMoveList)


---
### pmGetKingMoves<!-- {{#callable:pmGetKingMoves}} -->
The `pmGetKingMoves` function generates a list of all possible legal moves for a king piece from a given position on a chess board.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: A `sq` structure representing the current position of the king on the board.
- **Control Flow**:
    - The function calls [`pmLeaperMoveList`](#pmLeaperMoveList) with the board, the king's current position, the piece type `ptKing`, the array `royalOffsets` representing the king's possible move directions, and the number of directions (8).
    - [`pmLeaperMoveList`](#pmLeaperMoveList) processes these inputs to generate a list of valid moves for the king based on its leaping movement pattern.
- **Output**: A pointer to a `moveList` structure containing all valid moves for the king from the specified position.
- **Functions called**:
    - [`pmLeaperMoveList`](#pmLeaperMoveList)


