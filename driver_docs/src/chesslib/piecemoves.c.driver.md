# Purpose
This C source code file is part of a chess game implementation, specifically focusing on the movement logic for different chess pieces. The file defines functions that calculate possible moves for each type of chess piece, including pawns, knights, bishops, rooks, queens, and kings. The code is structured to handle the unique movement patterns of each piece, such as the leaping ability of knights and the linear movement of rooks and bishops. The file includes helper functions like [`canMoveHere`](#canMoveHere) to determine if a piece can move to a specific square, considering the presence of other pieces and their colors.

The file is not a standalone executable but rather a component of a larger chess library, as indicated by the inclusion of "chesslib/piecemoves.h". It provides specific functionality related to chess piece movements, which can be utilized by other parts of the chess program. The functions return lists of possible moves (`moveList`) for each piece, taking into account the current state of the board and the rules of chess, such as pawn promotion and en passant captures. This file is crucial for implementing the core mechanics of chess piece movement within the game.
# Imports and Dependencies

---
- `chesslib/piecemoves.h`


# Global Variables

---
### knightOffsets
- **Type**: `int8_t[8][2]`
- **Description**: The `knightOffsets` variable is a two-dimensional array of integers that represents the possible moves a knight can make on a chessboard. Each sub-array contains two integers, where the first integer represents the change in the file (column) and the second integer represents the change in the rank (row) of the knight's position.
- **Use**: This variable is used to calculate the potential new positions a knight can move to from its current position on the chessboard.


---
### bishopOffsets
- **Type**: `int8_t[4][2]`
- **Description**: The `bishopOffsets` variable is a two-dimensional array of integers that represents the possible movement directions for a bishop in a chess game. Each sub-array contains two integers, which correspond to the change in file and rank, respectively, for a bishop's diagonal movement on the chessboard.
- **Use**: This variable is used to determine the valid movement directions for a bishop piece when generating its possible moves on a chessboard.


---
### rookOffsets
- **Type**: `int8_t[4][2]`
- **Description**: The `rookOffsets` variable is a two-dimensional array of integers that represents the possible movement directions for a rook in a chess game. Each sub-array contains two integers, where the first integer represents the change in the file (column) and the second integer represents the change in the rank (row). The four sub-arrays correspond to the rook's ability to move vertically and horizontally on the chessboard.
- **Use**: This variable is used to determine the possible movement directions for a rook when generating its move list in the `pmGetRookMoves` function.


---
### royalOffsets
- **Type**: `int8_t[8][2]`
- **Description**: The `royalOffsets` variable is a two-dimensional array of 8 elements, each containing a pair of integers. These pairs represent the possible movement directions for the queen and king pieces on a chessboard, covering all eight surrounding squares in a grid pattern.
- **Use**: This variable is used to determine the valid movement directions for the queen and king pieces in chess, allowing them to move in any direction on the board.


# Functions

---
### canMoveHere<!-- {{#callable:canMoveHere}} -->
The `canMoveHere` function checks if a piece can move to a specified square on the board without encountering a piece of the same color.
- **Inputs**:
    - `b`: A pointer to the board structure representing the current state of the chess board.
    - `s`: The square on the board to which the piece is attempting to move.
    - `ourColor`: The color of the piece attempting to move.
- **Control Flow**:
    - Retrieve the piece located at the specified square `s` on the board `b` using [`boardGetPiece`](board.c.driver.md#boardGetPiece) function.
    - Check if the retrieved piece is `pEmpty`, indicating the square is empty; if so, return 1 (true) to indicate the move is possible.
    - If the square is not empty, retrieve the color of the piece at the square using [`pieceGetColor`](piece.c.driver.md#pieceGetColor).
    - Compare the color of the piece at the square with `ourColor`; if they are different, return 1 (true) to indicate the move is possible, otherwise return 0 (false).
- **Output**:
    - Returns 1 (true) if the square is empty or occupied by an opponent's piece, otherwise returns 0 (false) if occupied by a piece of the same color.
- **Functions called**:
    - [`boardGetPiece`](board.c.driver.md#boardGetPiece)
    - [`pieceGetColor`](piece.c.driver.md#pieceGetColor)


---
### pmLeaperMoveList<!-- {{#callable:pmLeaperMoveList}} -->
The `pmLeaperMoveList` function generates a list of valid moves for leaper-type chess pieces from a given position on the board.
- **Inputs**:
    - `b`: A pointer to the chess board structure, representing the current state of the game.
    - `s`: The starting square (of type `sq`) from which the piece will attempt to move.
    - `pt`: The type of the piece (of type `pieceType`) that is expected to be at the starting square.
    - `dirs`: A 2D array of integers representing the possible directions the piece can move in terms of file and rank offsets.
    - `numDirs`: The number of directions available in the `dirs` array.
- **Control Flow**:
    - Create a new move list using `moveListCreate()` to store potential moves.
    - Retrieve the piece located at the starting square `s` using `boardGetPiece(b, s)`.
    - Check if the piece type matches the expected type `pt`; if not, return the empty move list.
    - Determine the color of the piece at the starting square.
    - Iterate over each direction in the `dirs` array.
    - Calculate the new square by adding the direction offsets to the current square's file and rank.
    - Check if the new square is within the bounds of the board (1 to 8 for both file and rank).
    - If the new square is valid and can be moved to (using [`canMoveHere`](#canMoveHere)), add the move to the move list using [`moveListAdd`](movelist.c.driver.md#moveListAdd).
    - Return the populated move list.
- **Output**:
    - A pointer to a `moveList` structure containing all valid moves for the leaper piece from the given starting square.
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
The `pmRiderMoveList` function generates a list of all possible moves for a rider-type chess piece (like a bishop, rook, or queen) from a given position on the board, considering the piece's movement directions and the board's current state.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chessboard.
    - `s`: The `sq` structure representing the starting square of the piece on the board.
    - `pt`: The `pieceType` enumeration value representing the type of the piece (e.g., bishop, rook, queen) for which moves are being generated.
    - `dirs`: A 2D array of integers representing the possible movement directions for the piece, where each direction is a pair of integers indicating file and rank offsets.
    - `numDirs`: The number of movement directions provided in the `dirs` array.
- **Control Flow**:
    - Create an empty move list using `moveListCreate()`.
    - Retrieve the piece located at the starting square `s` using `boardGetPiece()`.
    - Check if the piece type matches the specified `pt`; if not, return the empty move list.
    - Determine the color of the piece using `pieceGetColor()`.
    - Iterate over each direction in the `dirs` array.
    - For each direction, initialize `newSq` to the starting square `s`.
    - In a loop, update `newSq` by adding the current direction offsets to its file and rank.
    - Check if `newSq` is within the board boundaries (file and rank between 1 and 8); if not, break the loop.
    - Retrieve the piece at `newSq` using `boardGetPiece()`.
    - Check if the piece can move to `newSq` using `canMoveHere()`; if true, add the move to the list using `moveListAdd()`.
    - If `newSq` contains a piece (not empty), break the loop to stop further movement in that direction.
    - Return the populated move list.
- **Output**:
    - A pointer to a `moveList` structure containing all valid moves for the rider piece from the starting square `s`.
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
The `addPawnMoveToMoveList` function adds a pawn move to a move list, including promotion moves if the pawn reaches the first or eighth rank.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure where the move will be added.
    - `oldSq`: The starting square of the pawn, represented as a `sq` structure.
    - `newSq`: The destination square of the pawn, represented as a `sq` structure.
- **Control Flow**:
    - Check if the destination square `newSq` is on the first or eighth rank, indicating a promotion opportunity.
    - If it is a promotion, add four promotion moves to the list: promoting the pawn to a queen, rook, bishop, and knight respectively.
    - If it is not a promotion, add a regular pawn move from `oldSq` to `newSq` to the list.
- **Output**:
    - The function does not return a value; it modifies the `moveList` pointed to by `list` by adding the appropriate move(s).
- **Functions called**:
    - [`moveListAdd`](movelist.c.driver.md#moveListAdd)
    - [`movePromote`](move.c.driver.md#movePromote)
    - [`moveSq`](move.c.driver.md#moveSq)


---
### pmGetPawnMoves<!-- {{#callable:pmGetPawnMoves}} -->
The `pmGetPawnMoves` function generates a list of all possible legal moves for a pawn located at a given square on a chess board.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: A `sq` structure representing the square on the board where the pawn is located.
- **Control Flow**:
    - Create an empty move list using `moveListCreate()`.
    - Retrieve the piece at square `s` using `boardGetPiece()` and check if it is a pawn; if not, return the empty move list.
    - Determine the pawn's color and set the movement direction (`delta`) based on whether the pawn is white or black.
    - Calculate the square directly in front of the pawn and check if it is empty; if so, add this move to the list.
    - Check if the pawn is on its starting rank and can move two squares forward; if so, add this move to the list if the square is empty.
    - Check for possible captures to the left and right of the pawn's current position, including en passant captures, and add these moves to the list if valid.
    - Return the populated move list.
- **Output**:
    - A pointer to a `moveList` structure containing all legal moves for the pawn at the specified square.
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
The `pmGetPawnAttacks` function generates a list of potential attack moves for a pawn on a chessboard, based on its current position and color.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chessboard.
    - `s`: A `sq` structure representing the current position of the pawn on the board.
- **Control Flow**:
    - Create a new move list using `moveListCreate()` to store potential attack moves.
    - Retrieve the piece at the given square `s` using `boardGetPiece(b, s)`.
    - Check if the piece is a pawn using `pieceGetType(p) != ptPawn`; if not, return the empty move list.
    - Determine the pawn's color using `pieceGetColor(p)` and set `delta` to 1 for white pawns and -1 for black pawns.
    - Check if the pawn can attack to the left (file > 1) by calculating the new square and using `canMoveHere()` to verify if the move is possible; if so, add the move to the list.
    - Check if the pawn can attack to the right (file < 8) by calculating the new square and using `canMoveHere()` to verify if the move is possible; if so, add the move to the list.
    - Return the list of potential attack moves.
- **Output**:
    - A pointer to a `moveList` structure containing the potential attack moves for the pawn from its current position.
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
The `pmGetKnightMoves` function generates a list of all possible legal moves for a knight piece from a given position on a chess board.
- **Inputs**:
    - `b`: A pointer to the chess board structure representing the current state of the game.
    - `s`: The square structure representing the current position of the knight on the board.
- **Control Flow**:
    - The function calls [`pmLeaperMoveList`](#pmLeaperMoveList) with the board, the knight's current position, the piece type for a knight, the predefined knight move offsets, and the number of possible knight moves (8).
    - [`pmLeaperMoveList`](#pmLeaperMoveList) processes these inputs to generate a list of valid moves for the knight, considering the board boundaries and potential captures.
- **Output**:
    - A pointer to a `moveList` structure containing all valid moves for the knight from the given position.
- **Functions called**:
    - [`pmLeaperMoveList`](#pmLeaperMoveList)


---
### pmGetBishopMoves<!-- {{#callable:pmGetBishopMoves}} -->
The `pmGetBishopMoves` function generates a list of all possible moves for a bishop located at a given square on a chess board.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: A `sq` structure representing the current position of the bishop on the board.
- **Control Flow**:
    - The function calls [`pmRiderMoveList`](#pmRiderMoveList) with the board, the bishop's current square, the piece type `ptBishop`, the direction offsets for a bishop, and the number of directions (4).
    - [`pmRiderMoveList`](#pmRiderMoveList) handles the logic for generating moves for pieces that can move multiple squares in a straight line, like a bishop.
- **Output**:
    - A pointer to a `moveList` structure containing all valid moves for the bishop from the given square.
- **Functions called**:
    - [`pmRiderMoveList`](#pmRiderMoveList)


---
### pmGetRookMoves<!-- {{#callable:pmGetRookMoves}} -->
The `pmGetRookMoves` function generates a list of all possible legal moves for a rook located at a given square on a chess board.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: A `sq` structure representing the current position of the rook on the board.
- **Control Flow**:
    - The function calls [`pmRiderMoveList`](#pmRiderMoveList) with the board, the rook's current square, the piece type `ptRook`, the direction offsets for a rook, and the number of directions (4).
    - [`pmRiderMoveList`](#pmRiderMoveList) processes these inputs to generate a list of all possible moves for the rook, considering the board boundaries and other pieces on the board.
- **Output**:
    - A pointer to a `moveList` structure containing all possible legal moves for the rook from the given position.
- **Functions called**:
    - [`pmRiderMoveList`](#pmRiderMoveList)


---
### pmGetQueenMoves<!-- {{#callable:pmGetQueenMoves}} -->
The `pmGetQueenMoves` function generates a list of all possible moves for a queen piece from a given position on a chess board.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: A `sq` structure representing the current position of the queen on the board.
- **Control Flow**:
    - The function calls [`pmRiderMoveList`](#pmRiderMoveList) with the board, the queen's current position, the piece type `ptQueen`, the direction offsets for a queen (`royalOffsets`), and the number of directions (8).
    - [`pmRiderMoveList`](#pmRiderMoveList) processes these inputs to generate all possible moves for the queen, considering the board boundaries and other pieces on the board.
- **Output**:
    - A pointer to a `moveList` structure containing all valid moves for the queen from the given position.
- **Functions called**:
    - [`pmRiderMoveList`](#pmRiderMoveList)


---
### pmGetKingMoves<!-- {{#callable:pmGetKingMoves}} -->
The `pmGetKingMoves` function generates a list of all possible legal moves for a king piece from a given position on a chess board.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: A `sq` structure representing the current position of the king on the board.
- **Control Flow**:
    - The function calls [`pmLeaperMoveList`](#pmLeaperMoveList) with the board, the king's current position, the piece type `ptKing`, the array `royalOffsets` defining the king's movement directions, and the number of directions (8).
    - [`pmLeaperMoveList`](#pmLeaperMoveList) processes these inputs to generate a list of valid moves for the king based on its movement capabilities and the current board state.
- **Output**:
    - A pointer to a `moveList` structure containing all valid moves for the king from the specified position.
- **Functions called**:
    - [`pmLeaperMoveList`](#pmLeaperMoveList)


