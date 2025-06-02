# Purpose
This C source code file implements a chess game engine, providing core functionalities for creating, managing, and interacting with a chess game state. The code is structured around a `chess` data structure, which encapsulates the current state of a chess game, including the board configuration, move history, and game status. The file includes functions to initialize a chess game from a standard starting position or a given FEN (Forsyth-Edwards Notation) string, manage the game's progression by playing and undoing moves, and determine the game's terminal state, such as checkmate or draw conditions. The code also provides utility functions to retrieve various aspects of the game state, such as the current board, legal moves, and move history in UCI (Universal Chess Interface) format.

The file is part of a broader chess library, as indicated by the inclusion of headers like "chesslib/chess.h" and "chesslib/move.h". It defines a public API for interacting with the chess game, allowing external code to create and manipulate chess games through a well-defined interface. Key technical components include memory management for dynamic data structures, such as board and move lists, and logic for calculating game state properties, such as legal moves and draw conditions. The code is designed to be integrated into larger applications, providing a robust foundation for building chess-related software, such as game engines, analysis tools, or user interfaces.
# Imports and Dependencies

---
- `stdlib.h`
- `chesslib/chess.h`
- `chesslib/move.h`


# Functions

---
### chessCreate<!-- {{#callable:chessCreate}} -->
The `chessCreate` function initializes a new chess game using the standard initial position in FEN notation.
- **Inputs**:
    - None
- **Control Flow**:
    - The function calls [`chessCreateFen`](#chessCreateFen) with `INITIAL_FEN` as the argument, which represents the standard starting position of a chess game.
    - The [`chessCreateFen`](#chessCreateFen) function allocates memory for a new `chess` structure and initializes it using the provided FEN string.
    - If the initialization is successful, the new `chess` structure is returned; otherwise, the allocated memory is freed and `NULL` is returned.
- **Output**:
    - A pointer to a newly created `chess` structure initialized to the standard starting position, or `NULL` if initialization fails.
- **Functions called**:
    - [`chessCreateFen`](#chessCreateFen)


---
### chessCreateFen<!-- {{#callable:chessCreateFen}} -->
The `chessCreateFen` function allocates and initializes a new chess game state from a given FEN string.
- **Inputs**:
    - `fen`: A string representing the board position in Forsyth-Edwards Notation (FEN).
- **Control Flow**:
    - Allocate memory for a new `chess` structure.
    - Call [`chessInitFenInPlace`](#chessInitFenInPlace) to initialize the `chess` structure with the given FEN string.
    - If initialization fails (returns non-zero), free the allocated memory and return `NULL`.
    - If initialization succeeds, return the pointer to the newly created `chess` structure.
- **Output**:
    - Returns a pointer to a newly allocated and initialized `chess` structure, or `NULL` if initialization fails.
- **Functions called**:
    - [`chessInitFenInPlace`](#chessInitFenInPlace)


---
### chessInitInPlace<!-- {{#callable:chessInitInPlace}} -->
The `chessInitInPlace` function initializes a given chess game structure to the starting position using the standard initial FEN string.
- **Inputs**:
    - `c`: A pointer to a `chess` structure that will be initialized to the starting position.
- **Control Flow**:
    - The function calls [`chessInitFenInPlace`](#chessInitFenInPlace) with the provided `chess` structure pointer `c` and the constant `INITIAL_FEN` to set up the chess board to the initial game state.
- **Output**:
    - This function does not return any value; it initializes the chess structure in place.
- **Functions called**:
    - [`chessInitFenInPlace`](#chessInitFenInPlace)


---
### chessInitFenInPlace<!-- {{#callable:chessInitFenInPlace}} -->
The `chessInitFenInPlace` function initializes a chess game state from a given FEN string and sets up the necessary data structures for tracking the game's progress.
- **Inputs**:
    - `c`: A pointer to a `chess` structure that will be initialized.
    - `fen`: A constant character pointer representing the FEN (Forsyth-Edwards Notation) string used to set up the initial board state.
- **Control Flow**:
    - Create a new board from the provided FEN string using [`boardCreateFromFen`](board.c.driver.md#boardCreateFromFen) and assign it to `b`.
    - Check if `b` is `NULL`, indicating an error in board creation, and return 1 if so.
    - Initialize `c->boardHistory` with a new board list and add the created board `b` to this list.
    - Initialize `c->moveHistory` with a new move list.
    - Set `c->currentLegalMoves` to `NULL`, `c->repetitions` to 1, and `c->terminal` to `tsOngoing`.
    - Call [`chessCalculateFields`](#chessCalculateFields) to compute the repetitions and terminal state of the game.
    - Return 0 to indicate successful initialization.
- **Output**:
    - Returns 0 on successful initialization, or 1 if the board creation from the FEN string fails.
- **Functions called**:
    - [`boardCreateFromFen`](board.c.driver.md#boardCreateFromFen)
    - [`boardListCreate`](boardlist.c.driver.md#boardListCreate)
    - [`boardListAdd`](boardlist.c.driver.md#boardListAdd)
    - [`moveListCreate`](movelist.c.driver.md#moveListCreate)
    - [`chessCalculateFields`](#chessCalculateFields)


---
### chessFree<!-- {{#callable:chessFree}} -->
The `chessFree` function deallocates memory associated with a chess game instance, including its board history, move history, and current legal moves.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the chess game instance to be freed.
- **Control Flow**:
    - Call [`boardListFree`](boardlist.c.driver.md#boardListFree) to free the memory allocated for the board history of the chess game.
    - Call [`moveListFree`](movelist.c.driver.md#moveListFree) to free the memory allocated for the move history of the chess game.
    - Call [`moveListFree`](movelist.c.driver.md#moveListFree) again to free the memory allocated for the current legal moves of the chess game.
    - Call `free` to deallocate the memory for the `chess` structure itself.
- **Output**:
    - This function does not return any value; it performs memory deallocation for the provided chess game instance.
- **Functions called**:
    - [`boardListFree`](boardlist.c.driver.md#boardListFree)
    - [`moveListFree`](movelist.c.driver.md#moveListFree)


---
### chessGetBoard<!-- {{#callable:chessGetBoard}} -->
The function `chessGetBoard` retrieves the current board state from a chess game instance.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of a chess game.
- **Control Flow**:
    - Access the `boardHistory` field of the `chess` structure pointed to by `c`.
    - Retrieve the `tail` node from the `boardHistory` linked list, which represents the most recent board state.
    - Return the `board` field from the `tail` node, which is the current board state.
- **Output**:
    - A pointer to a `board` structure representing the current state of the chess board.


---
### chessGetLegalMoves<!-- {{#callable:chessGetLegalMoves}} -->
The function `chessGetLegalMoves` retrieves the list of currently legal moves for a given chess game state.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function directly accesses the `currentLegalMoves` field of the `chess` structure pointed to by `c`.
    - It returns the value of `currentLegalMoves`, which is a pointer to a `moveList` structure containing the legal moves.
- **Output**:
    - A pointer to a `moveList` structure representing the current legal moves available in the chess game.


---
### chessGetTerminalState<!-- {{#callable:chessGetTerminalState}} -->
The function `chessGetTerminalState` retrieves the current terminal state of a chess game.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function accesses the `terminal` field of the `chess` structure pointed to by `c`.
    - It returns the value of the `terminal` field, which represents the current terminal state of the game.
- **Output**:
    - The function returns a `terminalState` value, indicating the current terminal state of the chess game, such as ongoing, checkmate, stalemate, or various draw conditions.


---
### chessGetBoardHistory<!-- {{#callable:chessGetBoardHistory}} -->
The function `chessGetBoardHistory` retrieves the history of board states from a chess game instance.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of a chess game.
- **Control Flow**:
    - The function accesses the `boardHistory` member of the `chess` structure pointed to by `c`.
    - It returns the `boardHistory`, which is a list of board states representing the history of the game.
- **Output**:
    - A pointer to a `boardList` structure, which contains the history of board states for the chess game.


---
### chessGetMoveHistory<!-- {{#callable:chessGetMoveHistory}} -->
The function `chessGetMoveHistory` retrieves the move history of a chess game.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function directly accesses the `moveHistory` member of the `chess` structure pointed to by `c`.
    - It returns the `moveHistory`, which is a pointer to a `moveList` structure.
- **Output**:
    - A pointer to a `moveList` structure that contains the history of moves made in the chess game.


---
### chessGetRepetitions<!-- {{#callable:chessGetRepetitions}} -->
The function `chessGetRepetitions` retrieves the number of times the current board position has been repeated in the game.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function directly accesses the `repetitions` field of the `chess` structure pointed to by `c`.
    - It returns the value of the `repetitions` field.
- **Output**:
    - The function returns an 8-bit unsigned integer (`uint8_t`) representing the number of repetitions of the current board position.


---
### chessPlayMove<!-- {{#callable:chessPlayMove}} -->
The `chessPlayMove` function attempts to play a given move in a chess game, updating the game state and history if the move is legal and the game is ongoing.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
    - `m`: A `move` structure representing the move to be played.
- **Control Flow**:
    - Check if the game is ongoing by verifying if `c->terminal` is `tsOngoing`; if not, return 1 indicating failure.
    - Initialize a `found` flag to 0 and iterate over the list of current legal moves.
    - For each legal move, check if it matches the move `m` using [`moveEq`](move.c.driver.md#moveEq); if a match is found, set `found` to 1 and break the loop.
    - If `found` is still 0 after the loop, return 1 indicating the move is not legal.
    - If the move is legal, use [`boardPlayMove`](board.c.driver.md#boardPlayMove) to apply the move to the current board and obtain a new board state.
    - Add the new board state to the board history and the move to the move history.
    - Call [`chessCalculateFields`](#chessCalculateFields) to update the game state, including legal moves and terminal state.
    - Return 0 indicating the move was successfully played.
- **Output**:
    - Returns 0 if the move was successfully played, or 1 if the move was illegal or the game is not ongoing.
- **Functions called**:
    - [`moveEq`](move.c.driver.md#moveEq)
    - [`boardPlayMove`](board.c.driver.md#boardPlayMove)
    - [`chessGetBoard`](#chessGetBoard)
    - [`boardListAdd`](boardlist.c.driver.md#boardListAdd)
    - [`moveListAdd`](movelist.c.driver.md#moveListAdd)
    - [`chessCalculateFields`](#chessCalculateFields)


---
### chessUndo<!-- {{#callable:chessUndo}} -->
The `chessUndo` function reverts the last move in a chess game, updating the game state accordingly.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - Check if there is only one board in the history (indicating no moves have been made); if so, return failure (1).
    - If the game is in a terminal state due to a draw claim (threefold repetition or 50-move rule), reset the terminal state to ongoing.
    - Otherwise, undo the last board and move in their respective histories.
    - Recalculate the game fields to update the current state of the game.
    - Return success (0) after successfully undoing the move.
- **Output**:
    - Returns 0 on success (move undone) or 1 on failure (no moves to undo).
- **Functions called**:
    - [`boardListUndo`](boardlist.c.driver.md#boardListUndo)
    - [`moveListUndo`](movelist.c.driver.md#moveListUndo)
    - [`chessCalculateFields`](#chessCalculateFields)


---
### chessGetPiece<!-- {{#callable:chessGetPiece}} -->
The `chessGetPiece` function retrieves the chess piece located at a specific square on the board of a given chess game state.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
    - `s`: A `sq` type representing the specific square on the chess board from which to retrieve the piece.
- **Control Flow**:
    - The function calls [`chessGetBoard`](#chessGetBoard) with the chess game state `c` to obtain the current board.
    - It then calls [`boardGetPiece`](board.c.driver.md#boardGetPiece) with the obtained board and the square `s` to retrieve the piece at that square.
    - The retrieved piece is returned as the output of the function.
- **Output**:
    - The function returns a `piece` type, which represents the chess piece located at the specified square on the board.
- **Functions called**:
    - [`boardGetPiece`](board.c.driver.md#boardGetPiece)
    - [`chessGetBoard`](#chessGetBoard)


---
### chessGetPlayer<!-- {{#callable:chessGetPlayer}} -->
The function `chessGetPlayer` retrieves the current player's color from a chess game state.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function calls [`chessGetBoard`](#chessGetBoard) with the chess game state `c` to obtain the current board.
    - It accesses the `currentPlayer` field of the board structure to get the current player's color.
    - The function returns the value of `currentPlayer`.
- **Output**:
    - The function returns a `pieceColor` value indicating the color of the current player (either white or black).
- **Functions called**:
    - [`chessGetBoard`](#chessGetBoard)


---
### chessGetCastleState<!-- {{#callable:chessGetCastleState}} -->
The function `chessGetCastleState` retrieves the current castling rights state from a chess game structure.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of a chess game.
- **Control Flow**:
    - The function calls [`chessGetBoard`](#chessGetBoard) with the chess structure `c` to obtain the current board state.
    - It accesses the `castleState` field of the board structure and returns it.
- **Output**:
    - The function returns an 8-bit unsigned integer representing the castling rights state of the current board.
- **Functions called**:
    - [`chessGetBoard`](#chessGetBoard)


---
### chessGetEpTarget<!-- {{#callable:chessGetEpTarget}} -->
The function `chessGetEpTarget` retrieves the en passant target square from the current board state of a chess game.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of a chess game.
- **Control Flow**:
    - The function calls [`chessGetBoard`](#chessGetBoard) with the chess game pointer `c` to obtain the current board state.
    - It then accesses the `epTarget` field of the board structure and returns it.
- **Output**:
    - The function returns a value of type `sq`, which represents the en passant target square on the chess board.
- **Functions called**:
    - [`chessGetBoard`](#chessGetBoard)


---
### chessGetHalfMoveClock<!-- {{#callable:chessGetHalfMoveClock}} -->
The function `chessGetHalfMoveClock` retrieves the half-move clock value from the current board state of a chess game.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of a chess game.
- **Control Flow**:
    - The function calls [`chessGetBoard`](#chessGetBoard) with the chess game pointer `c` to obtain the current board state.
    - It accesses the `halfMoveClock` field from the board structure and returns its value.
- **Output**:
    - The function returns an unsigned integer representing the half-move clock, which counts the number of half-moves since the last capture or pawn advance.
- **Functions called**:
    - [`chessGetBoard`](#chessGetBoard)


---
### chessGetMoveNumber<!-- {{#callable:chessGetMoveNumber}} -->
The function `chessGetMoveNumber` retrieves the current move number from a chess game state.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of a chess game.
- **Control Flow**:
    - The function calls [`chessGetBoard`](#chessGetBoard) with the chess game state `c` to obtain the current board.
    - It accesses the `moveNumber` field from the board structure and returns it.
- **Output**:
    - The function returns an unsigned integer representing the current move number in the chess game.
- **Functions called**:
    - [`chessGetBoard`](#chessGetBoard)


---
### chessGetMoveHistoryUci<!-- {{#callable:chessGetMoveHistoryUci}} -->
The function `chessGetMoveHistoryUci` retrieves the move history of a chess game in UCI (Universal Chess Interface) format.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function calls [`chessGetMoveHistory`](#chessGetMoveHistory) with the chess game pointer `c` to obtain the move history as a `moveList`.
    - It then calls [`moveListGetUciString`](movelist.c.driver.md#moveListGetUciString) with the retrieved move history to convert it into a UCI string format.
    - Finally, it returns the UCI string representing the move history.
- **Output**:
    - A string representing the move history of the chess game in UCI format.
- **Functions called**:
    - [`moveListGetUciString`](movelist.c.driver.md#moveListGetUciString)
    - [`chessGetMoveHistory`](#chessGetMoveHistory)


---
### chessIsInCheck<!-- {{#callable:chessIsInCheck}} -->
The `chessIsInCheck` function checks if the current player's king is in check on the chess board.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function calls [`chessGetBoard`](#chessGetBoard) with the `chess` pointer `c` to retrieve the current board state.
    - It then calls [`boardIsInCheck`](board.c.driver.md#boardIsInCheck) with the retrieved board to determine if the current player's king is in check.
    - The result from [`boardIsInCheck`](board.c.driver.md#boardIsInCheck) is returned as the output of the function.
- **Output**:
    - Returns a `uint8_t` value indicating whether the current player's king is in check (non-zero if in check, zero otherwise).
- **Functions called**:
    - [`boardIsInCheck`](board.c.driver.md#boardIsInCheck)
    - [`chessGetBoard`](#chessGetBoard)


---
### chessIsSquareAttacked<!-- {{#callable:chessIsSquareAttacked}} -->
The function `chessIsSquareAttacked` checks if a specific square on the chessboard is attacked by the opponent's pieces.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
    - `s`: A square (`sq` type) on the chessboard to check if it is attacked.
- **Control Flow**:
    - Retrieve the current board from the chess game structure `c` using [`chessGetBoard`](#chessGetBoard) function.
    - Determine the opponent's color based on the current player stored in the board structure.
    - Call [`boardIsSquareAttacked`](board.c.driver.md#boardIsSquareAttacked) with the board, the square `s`, and the opponent's color to check if the square is attacked.
- **Output**:
    - Returns a `uint8_t` value indicating whether the square is attacked (non-zero) or not (zero).
- **Functions called**:
    - [`chessGetBoard`](#chessGetBoard)
    - [`boardIsSquareAttacked`](board.c.driver.md#boardIsSquareAttacked)


---
### chessGetFen<!-- {{#callable:chessGetFen}} -->
The `chessGetFen` function retrieves the FEN (Forsyth-Edwards Notation) string representation of the current board state in a chess game.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function calls [`chessGetBoard`](#chessGetBoard) with the `chess` pointer `c` to obtain the current board from the chess game.
    - It then calls [`boardGetFen`](board.c.driver.md#boardGetFen) with the retrieved board to get the FEN string representation of the board.
- **Output**:
    - A string representing the FEN notation of the current board state.
- **Functions called**:
    - [`boardGetFen`](board.c.driver.md#boardGetFen)
    - [`chessGetBoard`](#chessGetBoard)


---
### chessCanClaimDraw50<!-- {{#callable:chessCanClaimDraw50}} -->
The function `chessCanClaimDraw50` checks if a chess game can claim a draw based on the 50-move rule.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - Check if the game's terminal state is `tsOngoing`, indicating the game is still in progress.
    - Retrieve the current board from the chess game structure using `chessGetBoard(c)`.
    - Check if the `halfMoveClock` of the current board is greater than or equal to 100, which corresponds to 50 moves without a pawn move or capture.
- **Output**:
    - Returns a `uint8_t` value (1 or 0) indicating whether a draw can be claimed based on the 50-move rule.
- **Functions called**:
    - [`chessGetBoard`](#chessGetBoard)


---
### chessCanClaimDrawThreefold<!-- {{#callable:chessCanClaimDrawThreefold}} -->
The function `chessCanClaimDrawThreefold` checks if a chess game can claim a draw due to the threefold repetition rule.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function checks if the game's terminal state is `tsOngoing`, indicating the game is still in progress.
    - It then checks if the number of repetitions of the current board position is 3 or more.
- **Output**:
    - Returns a `uint8_t` value that is non-zero (true) if the game can claim a draw due to threefold repetition, otherwise zero (false).


---
### chessClaimDraw50<!-- {{#callable:chessClaimDraw50}} -->
The function `chessClaimDraw50` sets the terminal state of a chess game to a draw due to the 50-move rule if the conditions for claiming such a draw are met.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function checks if a draw can be claimed due to the 50-move rule by calling [`chessCanClaimDraw50`](#chessCanClaimDraw50) with the chess game state `c`.
    - If [`chessCanClaimDraw50`](#chessCanClaimDraw50) returns true, the function sets the `terminal` field of the chess game state `c` to `tsDrawClaimed50MoveRule`.
- **Output**:
    - The function does not return a value; it modifies the `terminal` field of the `chess` structure if the draw condition is met.
- **Functions called**:
    - [`chessCanClaimDraw50`](#chessCanClaimDraw50)


---
### chessClaimDrawThreefold<!-- {{#callable:chessClaimDrawThreefold}} -->
The function `chessClaimDrawThreefold` sets the terminal state of a chess game to a draw due to threefold repetition if the conditions are met.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - The function checks if a draw can be claimed due to threefold repetition by calling [`chessCanClaimDrawThreefold`](#chessCanClaimDrawThreefold) with the chess game state `c`.
    - If the condition is true, it sets the `terminal` field of the chess game state `c` to `tsDrawClaimedThreefold`.
- **Output**:
    - The function does not return a value; it modifies the `terminal` field of the `chess` structure if the draw condition is met.
- **Functions called**:
    - [`chessCanClaimDrawThreefold`](#chessCanClaimDrawThreefold)


---
### chessCalculateFields<!-- {{#callable:chessCalculateFields}} -->
The `chessCalculateFields` function updates the state of a chess game by recalculating the number of board repetitions, generating legal moves, and determining the terminal state of the game.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game.
- **Control Flow**:
    - Retrieve the current board from the chess game structure `c`.
    - Initialize the repetition count to zero.
    - Iterate over the board history to count how many times the current board state has occurred.
    - Free the current list of legal moves if it exists.
    - Generate a new list of legal moves for the current board state and assign it to `c->currentLegalMoves`.
    - Check if there are no legal moves available; if so, determine if the game is in checkmate or stalemate and set the terminal state accordingly.
    - If there are legal moves, check for draw conditions such as fivefold repetition, 75-move rule, or insufficient material, and update the terminal state accordingly.
    - If none of the draw conditions are met and the terminal state is not a claimed draw, set the terminal state to ongoing.
- **Output**:
    - The function does not return a value but updates the `repetitions`, `currentLegalMoves`, and `terminal` fields of the `chess` structure `c`.
- **Functions called**:
    - [`chessGetBoard`](#chessGetBoard)
    - [`boardEqContext`](board.c.driver.md#boardEqContext)
    - [`moveListFree`](movelist.c.driver.md#moveListFree)
    - [`boardGenerateMoves`](board.c.driver.md#boardGenerateMoves)
    - [`boardIsInCheck`](board.c.driver.md#boardIsInCheck)
    - [`boardIsInsufficientMaterial`](board.c.driver.md#boardIsInsufficientMaterial)


