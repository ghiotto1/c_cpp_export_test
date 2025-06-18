# Purpose
This C header file defines functions related to generating potential moves for chess pieces on a board, likely as part of a larger chess game application. It includes functions for both "leaper" and "rider" pieces, which are terms used to describe how certain chess pieces move; leapers like knights move to specific squares based on offsets, while riders like bishops and rooks can move continuously in a direction until blocked. The file provides specific functions to generate move lists for each type of chess piece, including pawns, knights, bishops, rooks, queens, and kings, with a special function for pawn attacks due to their unique movement rules. The header file avoids circular dependencies by not including itself in other headers, and it relies on external definitions from "chesslib/board.h" and "chesslib/movelist.h" to function.
# Imports and Dependencies

---
- `chesslib/board.h`
- `chesslib/movelist.h`


# Function Declarations (Public API)

---
### pmLeaperMoveList<!-- {{#callable_declaration:pmLeaperMoveList}} -->
Generates a list of potential moves for a leaper piece on a chessboard.
- **Description**: This function is used to determine all potential moves for a leaper piece, such as a knight, on a given chessboard. It should be called when you need to calculate the possible destinations a piece can move to from a specific square, based on its movement pattern defined by directional offsets. The function requires a valid board state and the piece type must match the piece located at the specified square. It returns a list of potential moves, which may include moves that leave the player in check. The function handles out-of-bounds moves by ignoring them.
- **Inputs**:
    - `b`: A pointer to the board structure representing the current state of the chessboard. Must not be null.
    - `s`: The square from which the leaper piece is moving. It should be a valid square on the board.
    - `pt`: The type of the piece expected at the square 's'. It is used to verify that the piece at the square matches the expected type.
    - `dirs`: An array of integer pairs representing the possible directional offsets for the leaper's movement. Each pair defines a file and rank offset.
    - `numDirs`: The number of directional offsets provided in the 'dirs' array. It determines how many potential moves are considered.
- **Output**: Returns a pointer to a moveList containing potential moves for the leaper piece. The list may be empty if no valid moves are found.
- **See also**: [`pmLeaperMoveList`](../../src/chesslib/piecemoves.c.driver.md#pmLeaperMoveList)  (Implementation)


---
### pmRiderMoveList<!-- {{#callable_declaration:pmRiderMoveList}} -->
Generates a list of potential moves for a rider piece from a given position.
- **Description**: This function is used to determine all possible moves for a rider piece, such as a rook, bishop, or queen, from a specified position on the board. It should be called when you need to evaluate the potential moves for these types of pieces, considering their ability to move in a straight line in any direction until they encounter another piece or the edge of the board. The function assumes that the piece at the starting position matches the specified piece type. It returns a list of potential moves, which may include moves that leave the current player in check. The function does not modify the board or any input parameters.
- **Inputs**:
    - `b`: A pointer to the board structure representing the current state of the chess game. Must not be null.
    - `s`: The starting square from which the rider piece will move. It should be a valid square on the board.
    - `pt`: The type of the piece expected at the starting square. The function checks if the piece at the starting square matches this type.
    - `dirs`: An array of direction offsets, where each offset is a pair of integers representing a direction in which the piece can move. The array must contain valid direction pairs for the piece type.
    - `numDirs`: The number of direction pairs in the dirs array. Must be a non-negative integer.
- **Output**: A pointer to a moveList structure containing all potential moves for the rider piece from the given position. The list may be empty if no valid moves are found.
- **See also**: [`pmRiderMoveList`](../../src/chesslib/piecemoves.c.driver.md#pmRiderMoveList)  (Implementation)


---
### pmGetPawnMoves<!-- {{#callable_declaration:pmGetPawnMoves}} -->
Generates a list of potential moves for a pawn on a chessboard.
- **Description**: This function is used to determine all potential moves for a pawn located at a specific square on a given chessboard. It should be called when you need to evaluate the possible moves a pawn can make, including forward moves and captures, but it does not account for whether these moves would leave the player in check. The function assumes the board and square are valid and that the square contains a pawn. It returns a move list that may include moves that are not legal in the context of the entire game, such as moves that would leave the king in check.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chessboard. Must not be null, and must be properly initialized before calling this function.
    - `s`: A square structure representing the position of the pawn on the board. Must be a valid square on the board and should contain a pawn piece.
- **Output**: A pointer to a moveList structure containing all potential moves for the pawn at the specified square. The list may be empty if no moves are possible.
- **See also**: [`pmGetPawnMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetPawnMoves)  (Implementation)


---
### pmGetKnightMoves<!-- {{#callable_declaration:pmGetKnightMoves}} -->
Generates a list of potential knight moves from a given board position.
- **Description**: This function is used to obtain a list of all potential moves for a knight located at a specific square on a given chess board. It is useful when determining possible actions for a knight piece during a game. The function must be called with a valid board and a square that contains a knight. The returned move list includes all potential moves, but it does not account for moves that would leave the player's king in check. This function is typically used in the context of evaluating game states or generating move options for a knight.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null, and should be properly initialized before calling this function.
    - `s`: A square on the board where the knight is currently located. It should be a valid square index within the board's dimensions.
- **Output**: A pointer to a moveList structure containing potential moves for the knight. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetKnightMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetKnightMoves)  (Implementation)


---
### pmGetBishopMoves<!-- {{#callable_declaration:pmGetBishopMoves}} -->
Generates a list of potential bishop moves from a given board position.
- **Description**: This function is used to obtain a list of all potential moves for a bishop located at a specific square on a chess board. It is useful when determining possible actions for a bishop during a game. The function must be called with a valid board state and a square that contains a bishop. The returned move list includes all potential moves, but it does not account for whether these moves would leave the player's king in check. Therefore, additional validation is required to ensure the legality of each move in the context of the game.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null, and should be a valid board configuration.
    - `s`: The square on the board where the bishop is located. It should be a valid square index within the board's boundaries.
- **Output**: A pointer to a moveList structure containing potential moves for the bishop. The caller is responsible for managing the memory of the returned move list.
- **See also**: [`pmGetBishopMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetBishopMoves)  (Implementation)


---
### pmGetRookMoves<!-- {{#callable_declaration:pmGetRookMoves}} -->
Generates a list of potential rook moves from a given board position.
- **Description**: Use this function to obtain all potential moves for a rook located at a specific square on the chess board. This function is useful when you need to evaluate possible rook moves without considering whether the moves leave the current player in check. It is important to ensure that the board and square parameters are valid and represent a current game state before calling this function. The function returns a moveList containing all possible moves for the rook, which may include moves that are not legal in the context of the entire game (e.g., moves that would leave the king in check).
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null and should be properly initialized.
    - `s`: The square on the board where the rook is currently located. Must be a valid square within the board's boundaries.
- **Output**: A pointer to a moveList structure containing potential moves for the rook from the specified square. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetRookMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetRookMoves)  (Implementation)


---
### pmGetQueenMoves<!-- {{#callable_declaration:pmGetQueenMoves}} -->
Generates a list of potential moves for a queen on a chessboard.
- **Description**: This function is used to obtain a list of all potential moves for a queen piece located at a specific square on a given chessboard. It is useful in chess engines or applications that need to calculate possible moves for a queen, taking into account the board's current state. The function returns a move list that includes all possible moves the queen can make, but it does not consider whether these moves would leave the player's king in check. Therefore, additional validation is required to ensure the legality of the moves in the context of the game rules.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chessboard. Must not be null, as it is used to determine the positions of all pieces on the board.
    - `s`: The square on the board where the queen is currently located. It must be a valid square within the board's boundaries, typically represented by an integer or an enumeration.
- **Output**: A pointer to a moveList structure containing all potential moves for the queen from the specified square. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetQueenMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetQueenMoves)  (Implementation)


---
### pmGetKingMoves<!-- {{#callable_declaration:pmGetKingMoves}} -->
Generates a list of potential king moves from a given square on the board.
- **Description**: This function is used to determine all potential moves for a king piece located at a specific square on a chess board. It should be called when you need to evaluate the possible moves a king can make from its current position. The function returns a list of moves that the king can potentially make, but it does not account for moves that would leave the king in check. It is important to ensure that the board is properly initialized and the square is valid before calling this function.
- **Inputs**:
    - `b`: A pointer to a board structure representing the current state of the chess game. Must not be null, and should be properly initialized before calling this function.
    - `s`: The square on the board from which the king's moves are to be calculated. It should be a valid square within the board's boundaries.
- **Output**: A pointer to a moveList structure containing the potential moves for the king. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetKingMoves`](../../src/chesslib/piecemoves.c.driver.md#pmGetKingMoves)  (Implementation)


---
### pmGetPawnAttacks<!-- {{#callable_declaration:pmGetPawnAttacks}} -->
Generates a list of potential attack moves for a pawn on a given square.
- **Description**: This function is used to determine the potential attack moves for a pawn located on a specific square of the chess board. It should be called when you need to evaluate the attacking capabilities of a pawn, considering the current state of the board. The function assumes that the board and square are valid and that the square contains a pawn. It returns a list of moves that represent the squares the pawn can attack, which may include capturing an opponent's piece. The function does not validate whether the moves leave the player in check.
- **Inputs**:
    - `b`: A pointer to the board structure representing the current state of the chess game. Must not be null. The caller retains ownership.
    - `s`: The square on the board where the pawn is located. It must be a valid square index within the board's boundaries.
- **Output**: A pointer to a moveList structure containing potential attack moves for the pawn. The list may be empty if no valid attacks are possible. The caller is responsible for managing the memory of the returned moveList.
- **See also**: [`pmGetPawnAttacks`](../../src/chesslib/piecemoves.c.driver.md#pmGetPawnAttacks)  (Implementation)


