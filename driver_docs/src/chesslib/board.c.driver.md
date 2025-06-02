# Purpose
This C source code file implements a chess board management system, providing functionality to create, manipulate, and evaluate chess board states. The code is designed to handle chess board operations using the Forsyth-Edwards Notation (FEN), which is a standard notation for describing a particular board position of a chess game. The file includes functions to initialize a board from a FEN string, generate legal moves, check for check conditions, and determine if a board state has insufficient material for a checkmate. It also provides utilities for playing moves, checking board equality, and converting board states back to FEN strings.

The code is structured around a `board` data structure, which encapsulates the state of a chess game, including piece positions, current player, castling rights, en passant targets, and move counters. Key functions include [`boardCreateFromFen`](#boardCreateFromFen) for initializing a board from a FEN string, [`boardGenerateMoves`](#boardGenerateMoves) for generating all legal moves for the current player, and [`boardPlayMoveInPlace`](#boardPlayMoveInPlace) for executing a move on the board. The file also includes error handling for invalid FEN strings and provides mechanisms to check for special conditions like check, checkmate, and insufficient material. This code is intended to be part of a larger chess library, as indicated by the inclusion of headers like "chesslib/board.h" and "chesslib/piecemoves.h", and it does not define a main function, suggesting it is not an executable but rather a component to be used within a chess application.
# Imports and Dependencies

---
- `stdio.h`
- `ctype.h`
- `stdlib.h`
- `string.h`
- `chesslib/board.h`
- `chesslib/piecemoves.h`


# Functions

---
### boardCreate<!-- {{#callable:boardCreate}} -->
The `boardCreate` function initializes a new chess board using the standard initial position in FEN notation.
- **Inputs**:
    - None
- **Control Flow**:
    - The function calls [`boardCreateFromFen`](#boardCreateFromFen) with `INITIAL_FEN` as the argument, which represents the standard initial position of a chess game.
    - It returns the result of the [`boardCreateFromFen`](#boardCreateFromFen) function call.
- **Output**:
    - A pointer to a `board` structure initialized to the standard starting position, or `NULL` if initialization fails.
- **Functions called**:
    - [`boardCreateFromFen`](#boardCreateFromFen)


---
### boardCreateFromFen<!-- {{#callable:boardCreateFromFen}} -->
The `boardCreateFromFen` function creates a new chess board initialized from a given FEN string.
- **Inputs**:
    - `fen`: A string representing the board state in Forsyth-Edwards Notation (FEN).
- **Control Flow**:
    - Allocate memory for a new `board` structure.
    - Call [`boardInitFromFenInPlace`](#boardInitFromFenInPlace) to initialize the board with the FEN string.
    - If initialization fails (returns non-zero), free the allocated memory and return `NULL`.
    - If initialization succeeds, return the pointer to the newly created board.
- **Output**:
    - Returns a pointer to a newly allocated and initialized `board` structure, or `NULL` if initialization fails.
- **Functions called**:
    - [`boardInitFromFenInPlace`](#boardInitFromFenInPlace)


---
### boardInitInPlace<!-- {{#callable:boardInitInPlace}} -->
The `boardInitInPlace` function initializes a chess board to the standard starting position using the FEN string for the initial setup.
- **Inputs**:
    - `b`: A pointer to a `board` structure that will be initialized to the standard starting position.
- **Control Flow**:
    - The function calls [`boardInitFromFenInPlace`](#boardInitFromFenInPlace) with the board pointer `b` and the constant `INITIAL_FEN` which represents the standard starting position in FEN notation.
- **Output**:
    - The function does not return a value; it modifies the board in place to represent the initial chess position.
- **Functions called**:
    - [`boardInitFromFenInPlace`](#boardInitFromFenInPlace)


---
### boardInitFromFenInPlace<!-- {{#callable:boardInitFromFenInPlace}} -->
The function `boardInitFromFenInPlace` initializes a chess board structure from a given FEN (Forsyth-Edwards Notation) string, setting up the board's pieces, current player, castling rights, en passant target square, and move counters.
- **Inputs**:
    - `b`: A pointer to a `board` structure that will be initialized based on the FEN string.
    - `fen`: A constant character pointer representing the FEN string that describes the board state to be initialized.
- **Control Flow**:
    - Initialize the starting square to the top-left of the board (file 1, rank 8).
    - Iterate over the FEN string to read and set up the board pieces, handling numbers for empty squares, slashes for rank changes, and specific characters for different pieces.
    - Check for errors in the FEN string format, such as misplaced slashes or characters beyond the end of a rank, and return an error code if found.
    - After reading the piece placement, read the current player's turn ('w' or 'b') and validate it.
    - Parse the castling rights from the FEN string, updating the board's castling state accordingly.
    - Read the en passant target square from the FEN string, validating its format and updating the board's en passant target.
    - Finally, read the half-move clock and full move number from the FEN string using `sscanf`.
- **Output**:
    - Returns 0 on successful initialization, or 1 if an error is encountered in the FEN string.
- **Functions called**:
    - [`sqI`](square.c.driver.md#sqI)
    - [`boardSetPiece`](#boardSetPiece)
    - [`boardGetPiece`](#boardGetPiece)
    - [`sqS`](square.c.driver.md#sqS)


---
### boardSetPiece<!-- {{#callable:boardSetPiece}} -->
The `boardSetPiece` function sets a specific piece on a chess board at a given square.
- **Inputs**:
    - `b`: A pointer to the `board` structure where the piece is to be set.
    - `s`: The `sq` type representing the square on the board where the piece should be placed.
    - `p`: The `piece` type representing the chess piece to be placed on the board.
- **Control Flow**:
    - Calculate the index of the square `s` using the [`sqGetIndex`](square.c.driver.md#sqGetIndex) function.
    - Set the piece `p` at the calculated index in the `pieces` array of the board `b`.
- **Output**:
    - This function does not return any value; it modifies the board in place.
- **Functions called**:
    - [`sqGetIndex`](square.c.driver.md#sqGetIndex)


---
### boardGetPiece<!-- {{#callable:boardGetPiece}} -->
The `boardGetPiece` function retrieves the chess piece located at a specific square on a given chess board.
- **Inputs**:
    - `b`: A pointer to a `board` structure representing the current state of the chess board.
    - `s`: A `sq` type representing the specific square on the board from which to retrieve the piece.
- **Control Flow**:
    - The function calls [`sqGetIndex`](square.c.driver.md#sqGetIndex) with the square `s` to get the corresponding index in the board's piece array.
    - It then accesses the `pieces` array of the board `b` using the calculated index to retrieve the piece located at that square.
    - Finally, it returns the piece found at the specified index.
- **Output**:
    - The function returns a `piece` type, which represents the chess piece located at the specified square on the board.
- **Functions called**:
    - [`sqGetIndex`](square.c.driver.md#sqGetIndex)


---
### boardGenerateMoves<!-- {{#callable:boardGenerateMoves}} -->
The `boardGenerateMoves` function generates a list of all legal moves for the current player on a given chess board, including castling moves, and returns this list.
- **Inputs**:
    - `b`: A pointer to a `board` structure representing the current state of the chess game.
- **Control Flow**:
    - Create an empty move list using [`moveListCreate`](movelist.c.driver.md#moveListCreate).
    - Iterate over each square on the board (64 squares total).
    - For each square, retrieve the piece and check if it belongs to the current player; if not, continue to the next square.
    - Determine the type of piece and generate potential moves for that piece using the appropriate function (e.g., [`pmGetPawnMoves`](piecemoves.c.driver.md#pmGetPawnMoves) for pawns).
    - For each potential move, simulate the move on a copy of the board and check if the move results in the current player being in check; if not, add the move to the move list.
    - Check if castling is possible for the current player by verifying the conditions for castling (e.g., no pieces between the king and rook, squares not attacked).
    - Add valid castling moves to the move list if conditions are met.
    - Return the list of legal moves.
- **Output**:
    - A pointer to a `moveList` structure containing all legal moves for the current player, which must be freed after use.
- **Functions called**:
    - [`moveListCreate`](movelist.c.driver.md#moveListCreate)
    - [`sqIndex`](square.c.driver.md#sqIndex)
    - [`boardGetPiece`](#boardGetPiece)
    - [`pieceGetColor`](piece.c.driver.md#pieceGetColor)
    - [`pieceGetType`](piece.c.driver.md#pieceGetType)
    - [`pmGetPawnMoves`](piecemoves.c.driver.md#pmGetPawnMoves)
    - [`pmGetKnightMoves`](piecemoves.c.driver.md#pmGetKnightMoves)
    - [`pmGetBishopMoves`](piecemoves.c.driver.md#pmGetBishopMoves)
    - [`pmGetRookMoves`](piecemoves.c.driver.md#pmGetRookMoves)
    - [`pmGetQueenMoves`](piecemoves.c.driver.md#pmGetQueenMoves)
    - [`pmGetKingMoves`](piecemoves.c.driver.md#pmGetKingMoves)
    - [`boardPlayMoveInPlace`](#boardPlayMoveInPlace)
    - [`boardIsPlayerInCheck`](#boardIsPlayerInCheck)
    - [`moveListAdd`](movelist.c.driver.md#moveListAdd)
    - [`moveListFree`](movelist.c.driver.md#moveListFree)
    - [`sqI`](square.c.driver.md#sqI)
    - [`boardIsSquareAttacked`](#boardIsSquareAttacked)
    - [`moveSq`](move.c.driver.md#moveSq)


---
### boardIsSquareAttacked<!-- {{#callable:boardIsSquareAttacked}} -->
The function `boardIsSquareAttacked` checks if a specific square on a chess board is attacked by any piece of a given color.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `s`: The square (`sq` type) on the board to check for attacks.
    - `attacker`: The color (`pieceColor` type) of the pieces that might be attacking the square.
- **Control Flow**:
    - Iterate over all 64 squares on the board to find pieces of the specified attacker color.
    - For each piece found, determine its type and generate a list of possible moves or attacks for that piece using the appropriate function (e.g., [`pmGetPawnAttacks`](piecemoves.c.driver.md#pmGetPawnAttacks), [`pmGetKnightMoves`](piecemoves.c.driver.md#pmGetKnightMoves), etc.).
    - If a list of moves is generated, iterate through the moves to check if any move targets the specified square `s`.
    - If a move is found that targets the square `s`, free the move list and return 1, indicating the square is attacked.
    - If no attacking move is found after checking all pieces, return 0, indicating the square is not attacked.
- **Output**:
    - Returns 1 if the square is attacked by a piece of the specified color, otherwise returns 0.
- **Functions called**:
    - [`sqIndex`](square.c.driver.md#sqIndex)
    - [`boardGetPiece`](#boardGetPiece)
    - [`pieceGetColor`](piece.c.driver.md#pieceGetColor)
    - [`pieceGetType`](piece.c.driver.md#pieceGetType)
    - [`pmGetPawnAttacks`](piecemoves.c.driver.md#pmGetPawnAttacks)
    - [`pmGetKnightMoves`](piecemoves.c.driver.md#pmGetKnightMoves)
    - [`pmGetBishopMoves`](piecemoves.c.driver.md#pmGetBishopMoves)
    - [`pmGetRookMoves`](piecemoves.c.driver.md#pmGetRookMoves)
    - [`pmGetQueenMoves`](piecemoves.c.driver.md#pmGetQueenMoves)
    - [`pmGetKingMoves`](piecemoves.c.driver.md#pmGetKingMoves)
    - [`sqEq`](square.c.driver.md#sqEq)
    - [`moveListFree`](movelist.c.driver.md#moveListFree)


---
### boardIsInCheck<!-- {{#callable:boardIsInCheck}} -->
The `boardIsInCheck` function checks if the current player on a given chess board is in check.
- **Inputs**:
    - `b`: A pointer to a `board` structure representing the current state of the chess game.
- **Control Flow**:
    - The function calls [`boardIsPlayerInCheck`](#boardIsPlayerInCheck), passing the board `b` and the current player `b->currentPlayer` as arguments.
    - It returns the result of the [`boardIsPlayerInCheck`](#boardIsPlayerInCheck) function call, which determines if the current player's king is under attack.
- **Output**:
    - Returns a `uint8_t` value, where 1 indicates the current player is in check, and 0 indicates they are not.
- **Functions called**:
    - [`boardIsPlayerInCheck`](#boardIsPlayerInCheck)


---
### boardIsPlayerInCheck<!-- {{#callable:boardIsPlayerInCheck}} -->
The function `boardIsPlayerInCheck` checks if a player's king is currently in check on a given chess board.
- **Inputs**:
    - `b`: A pointer to a `board` structure representing the current state of the chess board.
    - `player`: A `pieceColor` value indicating the color of the player (either `pcWhite` or `pcBlack`) whose king's check status is being evaluated.
- **Control Flow**:
    - Determine the type of the player's king (`pWKing` for white or `pBKing` for black) and the opponent's color (`pcBlack` for white player and `pcWhite` for black player).
    - Iterate over all 64 squares of the board using a loop.
    - For each square, check if the piece on that square is the player's king.
    - If the player's king is found, check if the square is attacked by any piece of the opponent's color using [`boardIsSquareAttacked`](#boardIsSquareAttacked).
    - If the square is attacked, return 1 indicating the player is in check.
    - If the loop completes without finding the king in check, return 0 indicating the player is not in check.
- **Output**:
    - Returns a `uint8_t` value: 1 if the player's king is in check, 0 otherwise.
- **Functions called**:
    - [`sqIndex`](square.c.driver.md#sqIndex)
    - [`boardGetPiece`](#boardGetPiece)
    - [`boardIsSquareAttacked`](#boardIsSquareAttacked)


---
### boardIsInsufficientMaterial<!-- {{#callable:boardIsInsufficientMaterial}} -->
The function `boardIsInsufficientMaterial` checks if a chess board position is a draw due to insufficient material to checkmate.
- **Inputs**:
    - `b`: A pointer to a `board` structure representing the current state of the chess board.
- **Control Flow**:
    - Initialize counters for pieces, knights, bishops on dark squares, bishops on light squares, and kings.
    - Iterate over all 64 squares of the board to count the number of each type of piece.
    - Check if the board has only kings, which is always a draw, and return 1 if true.
    - Check if there is one white king and one black king, and if the total number of pieces equals the sum of kings and minor pieces (knights and bishops).
    - If there are only two kings and one minor piece, return 1 indicating a draw.
    - If there are only two kings and bishops all on the same color, return 1 indicating a draw.
    - If none of the draw conditions are met, return 0.
- **Output**:
    - Returns 1 if the position is a draw due to insufficient material, otherwise returns 0.
- **Functions called**:
    - [`sqIndex`](square.c.driver.md#sqIndex)
    - [`boardGetPiece`](#boardGetPiece)
    - [`pieceGetType`](piece.c.driver.md#pieceGetType)
    - [`sqIsDark`](square.c.driver.md#sqIsDark)


---
### boardPlayMove<!-- {{#callable:boardPlayMove}} -->
The `boardPlayMove` function creates a new chess board state by applying a given move to an existing board.
- **Inputs**:
    - `b`: A pointer to the current board structure representing the current state of the chess game.
    - `m`: A move structure representing the move to be applied to the board.
- **Control Flow**:
    - Allocate memory for a new board structure and copy the contents of the existing board into it.
    - Call [`boardPlayMoveInPlace`](#boardPlayMoveInPlace) to apply the move to the new board in place.
    - Return the pointer to the newly created board with the move applied.
- **Output**:
    - A pointer to a new board structure that represents the state of the board after the move has been applied.
- **Functions called**:
    - [`boardPlayMoveInPlace`](#boardPlayMoveInPlace)


---
### boardPlayMoveInPlace<!-- {{#callable:boardPlayMoveInPlace}} -->
The `boardPlayMoveInPlace` function executes a given chess move on a board, updating the board's state accordingly.
- **Inputs**:
    - `b`: A pointer to the `board` structure representing the current state of the chess board.
    - `m`: A `move` structure representing the move to be played, including the starting and ending positions and any promotion details.
- **Control Flow**:
    - If the current player is black, increment the move number.
    - Determine if the move is irreversible (pawn move or capture) and reset or increment the half-move clock accordingly.
    - Check if the move is a castling move and update the rook's position and castling rights.
    - If a rook moves or is captured, update the castling rights by clearing the appropriate flags.
    - Handle en passant captures by removing the captured pawn from the board.
    - Move the piece from the source to the destination square, handling promotions if necessary.
    - Set the en passant target square if a pawn moves two squares forward, otherwise invalidate it.
    - Switch the current player to the other player.
- **Output**:
    - The function does not return a value; it modifies the board in place to reflect the move played.
- **Functions called**:
    - [`pieceGetType`](piece.c.driver.md#pieceGetType)
    - [`boardGetPiece`](#boardGetPiece)
    - [`boardSetPiece`](#boardSetPiece)
    - [`sqI`](square.c.driver.md#sqI)
    - [`sqEq`](square.c.driver.md#sqEq)
    - [`pieceMake`](piece.c.driver.md#pieceMake)


---
### boardEq<!-- {{#callable:boardEq}} -->
The `boardEq` function checks if two chess board states are fully equal by comparing various attributes and the board's memory.
- **Inputs**:
    - `b1`: A pointer to the first board structure to be compared.
    - `b2`: A pointer to the second board structure to be compared.
- **Control Flow**:
    - Check if the current player of both boards is the same; if not, return 0.
    - Check if the castling state of both boards is the same; if not, return 0.
    - Check if the en passant target squares of both boards are equal using [`sqEq`](square.c.driver.md#sqEq); if not, return 0.
    - Check if the half-move clock values of both boards are the same; if not, return 0.
    - Check if the move numbers of both boards are the same; if not, return 0.
    - Use `memcmp` to compare the memory of both boards for the first 64 pieces; if they differ, return 0.
    - If all checks pass, return 1 indicating the boards are fully equal.
- **Output**:
    - Returns 1 if the boards are fully equal, otherwise returns 0.
- **Functions called**:
    - [`sqEq`](square.c.driver.md#sqEq)


---
### boardEqContext<!-- {{#callable:boardEqContext}} -->
The `boardEqContext` function checks if two chess boards are contextually equal, ignoring move counters and filtering en passant target squares.
- **Inputs**:
    - `b1`: A pointer to the first board structure to compare.
    - `b2`: A pointer to the second board structure to compare.
- **Control Flow**:
    - Check if the current player on both boards is the same; if not, return 0.
    - Check if the castling state on both boards is the same; if not, return 0.
    - Compare the memory of both boards for the first 64 pieces; if they differ, return 0.
    - For each board, check if the en passant target square is valid and if any pawns can attack it; if not, set it to invalid.
    - Compare the en passant target squares of both boards; if they differ, return 0.
    - If all checks pass, return 1 indicating the boards are contextually equal.
- **Output**:
    - Returns 1 if the boards are contextually equal, otherwise returns 0.
- **Functions called**:
    - [`sqEq`](square.c.driver.md#sqEq)
    - [`sqI`](square.c.driver.md#sqI)
    - [`boardGetPiece`](#boardGetPiece)
    - [`boardPlayMoveInPlace`](#boardPlayMoveInPlace)
    - [`moveSq`](move.c.driver.md#moveSq)
    - [`boardIsPlayerInCheck`](#boardIsPlayerInCheck)


---
### boardGetFen<!-- {{#callable:boardGetFen}} -->
The `boardGetFen` function generates a FEN (Forsyth-Edwards Notation) string representing the current state of a chess board.
- **Inputs**:
    - `b`: A pointer to a `board` structure representing the current state of the chess game.
- **Control Flow**:
    - Initialize a buffer `buf` to store the FEN string and a pointer `c` to traverse the buffer.
    - Iterate over each rank from 8 to 1 and each file from 1 to 8 to process each square on the board.
    - For each square, check if it contains a piece; if so, append the piece's letter to the buffer, otherwise increment a blank counter.
    - If there are blanks at the end of a rank, append the count to the buffer and add a '/' if not the last rank.
    - Append the current player's turn ('w' or 'b') to the buffer.
    - Determine the castling rights and append the appropriate characters ('K', 'Q', 'k', 'q') or '-' if none.
    - Check the en passant target square and append its coordinates or '-' if invalid.
    - Use `sprintf` to append the half-move clock and move number to the buffer.
    - Allocate memory for the FEN string, copy the buffer content to it, and return the string.
- **Output**:
    - A dynamically allocated string containing the FEN representation of the board, which must be freed by the caller.
- **Functions called**:
    - [`sqI`](square.c.driver.md#sqI)
    - [`boardGetPiece`](#boardGetPiece)
    - [`pieceGetLetter`](piece.c.driver.md#pieceGetLetter)
    - [`sqEq`](square.c.driver.md#sqEq)
    - [`sqGetStr`](square.c.driver.md#sqGetStr)


