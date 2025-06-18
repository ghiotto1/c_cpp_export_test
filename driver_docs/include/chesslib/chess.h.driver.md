# Purpose
This C header file defines the structure and functionality for managing a chess game, encapsulating the game's state and operations. It provides a comprehensive API for creating, initializing, and manipulating a chess game, including functions to handle game state transitions, move execution, and draw claims. The file includes definitions for a `chess` struct, which maintains the current legal moves, terminal state, board history, move history, and repetition count. The `terminalState` enumeration defines various end-game conditions, such as checkmate and different types of draws.

The file offers a range of functions for interacting with the chess game, including creating a new game from scratch or from a FEN string, retrieving game state information, and executing or undoing moves. It also provides utility functions that mirror operations on the board structure for convenience, such as getting the piece at a specific square or checking if a square is attacked. Additionally, the file includes functions for handling draw claims based on the 50-move rule and threefold repetition. This header file is designed to be included in other C source files, providing a robust interface for chess game management and facilitating the development of chess-related applications.
# Imports and Dependencies

---
- `chesslib/boardlist.h`
- `chesslib/movelist.h`
- `chesslib/squareset.h`


# Data Structures

---
### terminalState
- **Type**: `enum`
- **Members**:
    - `tsOngoing`: Represents a game state where the game is still ongoing.
    - `tsCheckmate`: Indicates that the game has ended in checkmate.
    - `tsDrawStalemate`: Represents a draw due to stalemate.
    - `tsDrawClaimed50MoveRule`: Indicates a draw claimed by the 50-move rule.
    - `tsDraw75MoveRule`: Represents a draw automatically enforced by the 75-move rule.
    - `tsDrawClaimedThreefold`: Indicates a draw claimed by threefold repetition.
    - `tsDrawFivefold`: Represents a draw automatically enforced by fivefold repetition.
    - `tsDrawInsufficient`: Indicates a draw due to insufficient material to checkmate.
- **Description**: The `terminalState` enum defines the possible end states of a chess game, including ongoing play, checkmate, and various types of draws such as stalemate, 50-move rule, threefold repetition, and insufficient material. It is used to track the current status of a chess game and determine if the game has reached a conclusion.


---
### chess
- **Type**: `struct`
- **Members**:
    - `currentLegalMoves`: A pointer to a list of currently legal moves in the chess game.
    - `terminal`: An enumeration indicating the terminal state of the game, such as ongoing, checkmate, or draw.
    - `boardHistory`: A pointer to a list of all board states that have occurred during the game.
    - `moveHistory`: A pointer to a list of all moves that have been played in the game.
    - `repetitions`: A counter for how many times the current board position has been repeated.
- **Description**: The 'chess' struct is a comprehensive data structure designed to encapsulate the state of a chess game. It includes pointers to lists of legal moves, board history, and move history, allowing for tracking the progression of the game. The 'terminal' field indicates the current state of the game, such as whether it is ongoing or has ended in checkmate or a draw. The 'repetitions' field helps in determining draw conditions based on repeated positions. This struct is central to managing and manipulating the state of a chess game programmatically.


# Function Declarations (Public API)

---
### chessCreate<!-- {{#callable_declaration:chessCreate}} -->
Creates and initializes a new chess game instance.
- **Description**: This function is used to create and initialize a new chess game instance with the standard initial position. It is suitable for starting a new game of chess from the traditional starting setup. The function allocates memory for the chess game structure, and the caller is responsible for freeing this memory using `chessFree` when the game is no longer needed. This function does not require any parameters and will return a pointer to the initialized chess game structure. If the initialization fails, it will return NULL.
- **Inputs**: None
- **Output**: Returns a pointer to a newly created chess game instance, or NULL if initialization fails.
- **See also**: [`chessCreate`](../../src/chesslib/chess.c.driver.md#chessCreate)  (Implementation)


---
### chessCreateFen<!-- {{#callable_declaration:chessCreateFen}} -->
Creates and initializes a chess game from a FEN string.
- **Description**: This function allocates and initializes a new chess game structure based on the provided FEN (Forsyth-Edwards Notation) string, which describes a specific board position. It is useful for setting up a game from a known position. The function returns a pointer to the initialized chess game structure if the FEN string is valid. If the FEN string is invalid, the function returns NULL, indicating that the game could not be initialized. The caller is responsible for freeing the returned chess game structure using `chessFree` when it is no longer needed.
- **Inputs**:
    - `fen`: A null-terminated string representing the board position in Forsyth-Edwards Notation. The string must be valid FEN; otherwise, the function will return NULL. The caller retains ownership of this string, and it must not be null.
- **Output**: A pointer to a newly allocated and initialized chess game structure if the FEN is valid; otherwise, NULL if the FEN is invalid.
- **See also**: [`chessCreateFen`](../../src/chesslib/chess.c.driver.md#chessCreateFen)  (Implementation)


---
### chessInitInPlace<!-- {{#callable_declaration:chessInitInPlace}} -->
Initializes a chess game to the standard starting position.
- **Description**: Use this function to set up a chess game to the standard initial position. It should be called on a `chess` structure that has already been allocated. This function is useful when you want to start a new game from the standard starting position without creating a new `chess` object. Ensure that the `chess` structure is properly allocated before calling this function to avoid undefined behavior.
- **Inputs**:
    - `c`: A pointer to a `chess` structure that must be allocated before calling this function. The caller retains ownership and is responsible for managing the memory of this structure. The function assumes the pointer is valid and does not perform null checks.
- **Output**: None
- **See also**: [`chessInitInPlace`](../../src/chesslib/chess.c.driver.md#chessInitInPlace)  (Implementation)


---
### chessInitFenInPlace<!-- {{#callable_declaration:chessInitFenInPlace}} -->
Initializes a chess game state from a FEN string.
- **Description**: This function initializes a given chess game structure using a FEN (Forsyth-Edwards Notation) string, which describes a specific board position. It should be used when you want to set up a chess game to a specific state as described by the FEN string. The function must be called with a valid chess structure and a valid FEN string. If the FEN string is invalid, the function returns 1 and does not modify the chess structure. Otherwise, it returns 0 and initializes the chess structure with the board position, move history, and other relevant game state information.
- **Inputs**:
    - `c`: A pointer to a chess structure that will be initialized. Must not be null and should be a valid, allocated chess structure.
    - `fen`: A pointer to a null-terminated string containing the FEN representation of the chess board state. Must not be null. If the FEN is invalid, the function returns 1 and does not modify the chess structure.
- **Output**: Returns 0 if the FEN string is valid and the chess structure is successfully initialized; returns 1 if the FEN string is invalid.
- **See also**: [`chessInitFenInPlace`](../../src/chesslib/chess.c.driver.md#chessInitFenInPlace)  (Implementation)


---
### chessFree<!-- {{#callable_declaration:chessFree}} -->
Frees a chess game and all its components.
- **Description**: Use this function to release all resources associated with a chess game when it is no longer needed. It is essential to call this function to prevent memory leaks after you are done using a chess game object created with `chessCreate` or `chessCreateFen`. Ensure that the pointer `c` is not used after calling this function, as it will be invalidated. This function does not handle null pointers, so ensure that `c` is a valid pointer before calling.
- **Inputs**:
    - `c`: A pointer to a `chess` structure that represents the chess game to be freed. Must not be null. The caller loses ownership of the memory pointed to by `c` after this function is called.
- **Output**: None
- **See also**: [`chessFree`](../../src/chesslib/chess.c.driver.md#chessFree)  (Implementation)


---
### chessGetBoard<!-- {{#callable_declaration:chessGetBoard}} -->
Retrieves the current board state from a chess game.
- **Description**: Use this function to obtain the current board state of a chess game represented by the `chess` structure. This function is useful when you need to analyze or display the current position of pieces on the board. It is expected that the `chess` structure has been properly initialized and is in a valid state before calling this function. The function does not modify the state of the chess game or the board.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current game. Must not be null and should point to a valid, initialized chess game. If the `chess` structure is not properly initialized, the behavior is undefined.
- **Output**: A pointer to a `board` structure representing the current board state of the chess game. The caller does not own this pointer and should not attempt to free it.
- **See also**: [`chessGetBoard`](../../src/chesslib/chess.c.driver.md#chessGetBoard)  (Implementation)


---
### chessGetLegalMoves<!-- {{#callable_declaration:chessGetLegalMoves}} -->
Retrieves the list of legal moves for the current game state.
- **Description**: Use this function to obtain the current list of legal moves available in the ongoing chess game. This function is useful for determining the possible actions a player can take at any given point in the game. It is important to ensure that the chess game has been properly initialized before calling this function, as it relies on the current game state to provide accurate legal moves. The function does not modify the game state or the list of moves; it simply returns a reference to the existing list.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null, and the game should be properly initialized before calling this function.
- **Output**: A pointer to a moveList structure containing the legal moves for the current game state. The caller should not modify or free this list.
- **See also**: [`chessGetLegalMoves`](../../src/chesslib/chess.c.driver.md#chessGetLegalMoves)  (Implementation)


---
### chessGetTerminalState<!-- {{#callable_declaration:chessGetTerminalState}} -->
Retrieve the current terminal state of a chess game.
- **Description**: Use this function to determine the current terminal state of a chess game, which indicates whether the game is ongoing, in checkmate, or drawn under various conditions. This function is useful for checking the game's status after moves have been played. It should be called on a valid chess game object that has been properly initialized. The function does not modify the game state or any of its components.
- **Inputs**:
    - `c`: A pointer to a chess game object. Must not be null and should point to a valid, initialized chess game structure. If the pointer is invalid, the behavior is undefined.
- **Output**: Returns the current terminal state of the chess game, which is an enumeration value of type `terminalState`.
- **See also**: [`chessGetTerminalState`](../../src/chesslib/chess.c.driver.md#chessGetTerminalState)  (Implementation)


---
### chessGetBoardHistory<!-- {{#callable_declaration:chessGetBoardHistory}} -->
Retrieve the history of board states in a chess game.
- **Description**: Use this function to access the sequence of board states that have occurred throughout the game. It is useful for analyzing the progression of the game or for implementing features that require knowledge of past board configurations. This function should be called on a valid chess game object, and it assumes that the game has been properly initialized. The caller should not modify the returned board history directly.
- **Inputs**:
    - `c`: A pointer to a chess game object. Must not be null and should point to a valid, initialized chess game structure. The function does not modify the chess object.
- **Output**: A pointer to a boardList representing the history of board states in the game. The caller does not own this pointer and should not attempt to free or modify it.
- **See also**: [`chessGetBoardHistory`](../../src/chesslib/chess.c.driver.md#chessGetBoardHistory)  (Implementation)


---
### chessGetMoveHistory<!-- {{#callable_declaration:chessGetMoveHistory}} -->
Retrieves the history of moves made in the chess game.
- **Description**: This function is used to obtain the list of all moves that have been played in a given chess game instance. It is useful for analyzing the game's progression or for displaying the move history to users. The function should be called on a valid chess game object, and it does not modify the game state. The returned move list reflects the current state of the game's move history.
- **Inputs**:
    - `c`: A pointer to a chess game object. This must be a valid, initialized chess object, and must not be null. The caller retains ownership of the chess object.
- **Output**: A pointer to a moveList object representing the history of moves made in the game. The caller should not modify or free this list directly.
- **See also**: [`chessGetMoveHistory`](../../src/chesslib/chess.c.driver.md#chessGetMoveHistory)  (Implementation)


---
### chessGetRepetitions<!-- {{#callable_declaration:chessGetRepetitions}} -->
Retrieve the number of times the current board position has been repeated.
- **Description**: Use this function to determine how many times the current board position has occurred during the game, which can be useful for detecting potential draw conditions such as the threefold repetition rule. This function should be called on a valid `chess` object that has been properly initialized. It does not modify the state of the game or the `chess` object.
- **Inputs**:
    - `c`: A pointer to a `chess` object representing the current game state. Must not be null, and the game must be initialized before calling this function.
- **Output**: Returns the number of times the current board position has been repeated as an unsigned 8-bit integer.
- **See also**: [`chessGetRepetitions`](../../src/chesslib/chess.c.driver.md#chessGetRepetitions)  (Implementation)


---
### chessPlayMove<!-- {{#callable_declaration:chessPlayMove}} -->
Attempts to play a specified move in a chess game.
- **Description**: This function is used to attempt playing a move in an ongoing chess game. It should be called when you want to execute a move that is expected to be legal. The function checks if the game is still ongoing and if the move is among the current legal moves. If the move is legal and the game is ongoing, it updates the game state by applying the move, adding it to the move history, and recalculating the game fields. If the move is illegal or the game has already ended, the function returns an error code. This function should be used only when the game is in progress and the move is expected to be valid.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null and the game must be ongoing (i.e., terminal state is tsOngoing). The caller retains ownership.
    - `m`: A move structure representing the move to be played. It should be a valid move that is expected to be in the list of current legal moves.
- **Output**: Returns 0 if the move was successfully played, or 1 if the move was illegal or the game is not ongoing.
- **See also**: [`chessPlayMove`](../../src/chesslib/chess.c.driver.md#chessPlayMove)  (Implementation)


---
### chessUndo<!-- {{#callable_declaration:chessUndo}} -->
Undoes the last move or draw claim in a chess game.
- **Description**: Use this function to revert the most recent move or draw claim in a chess game, effectively stepping back one move in the game's history. This function is useful when implementing features like undo in a chess application. It must be called on a valid chess game instance that has at least one move in its history; otherwise, it will return an error. The function also resets the terminal state if a draw was claimed due to the threefold repetition or the 50-move rule. Ensure that the chess game instance is properly initialized and contains a valid move history before calling this function.
- **Inputs**:
    - `c`: A pointer to a chess game instance. This must be a valid, initialized chess game object with a non-empty move history. The caller retains ownership of this pointer. If the move history is empty, the function will return an error.
- **Output**: Returns 0 if the undo operation is successful, or 1 if unsuccessful (e.g., no moves left to undo).
- **See also**: [`chessUndo`](../../src/chesslib/chess.c.driver.md#chessUndo)  (Implementation)


---
### chessGetPiece<!-- {{#callable_declaration:chessGetPiece}} -->
Retrieves the piece located at a specific square on the chessboard.
- **Description**: Use this function to obtain the piece present at a given square in the current state of a chess game. This function is useful for querying the board to determine what piece, if any, occupies a specific location. It is important to ensure that the chess game has been properly initialized before calling this function. The function does not modify the state of the game or the board.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current state of the chess game. Must not be null, and the chess game should be initialized before use.
    - `s`: An identifier for the square on the chessboard from which to retrieve the piece. The square must be valid within the context of the chessboard.
- **Output**: The function returns the piece located at the specified square. If the square is empty, it returns a value indicating no piece is present.
- **See also**: [`chessGetPiece`](../../src/chesslib/chess.c.driver.md#chessGetPiece)  (Implementation)


---
### chessGetPlayer<!-- {{#callable_declaration:chessGetPlayer}} -->
Retrieve the current player's color in a chess game.
- **Description**: Use this function to determine which player's turn it is in the current state of a chess game. It is useful for game logic that depends on knowing whether it is the white or black player's turn. This function should be called on a valid chess game object that has been properly initialized. The function does not modify the game state and is safe to call at any point after initialization.
- **Inputs**:
    - `c`: A pointer to a chess game object. This must not be null and should point to a valid, initialized chess game structure. If the pointer is invalid, the behavior is undefined.
- **Output**: The function returns a value of type pieceColor, indicating the color of the player whose turn it is.
- **See also**: [`chessGetPlayer`](../../src/chesslib/chess.c.driver.md#chessGetPlayer)  (Implementation)


---
### chessGetCastleState<!-- {{#callable_declaration:chessGetCastleState}} -->
Retrieve the current castling rights state of the chess game.
- **Description**: Use this function to obtain the current castling rights state of a chess game represented by the `chess` structure. This function is useful when you need to check which castling moves are still available in the game. It should be called with a valid `chess` pointer that has been properly initialized. The function does not modify the state of the game or the input structure.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of a chess game. Must not be null and should be properly initialized before calling this function.
- **Output**: Returns an 8-bit unsigned integer representing the castling rights state of the game.
- **See also**: [`chessGetCastleState`](../../src/chesslib/chess.c.driver.md#chessGetCastleState)  (Implementation)


---
### chessGetEpTarget<!-- {{#callable_declaration:chessGetEpTarget}} -->
Retrieves the en passant target square for the current board state.
- **Description**: This function is used to obtain the en passant target square from the current state of a chess game. It is useful when determining if an en passant capture is possible in the current position. The function should be called when you need to check or display the en passant target square during a game. It assumes that the chess game has been properly initialized and is in a valid state. The function does not modify the game state or any of its components.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. It must not be null, and the chess game must be properly initialized before calling this function. If the pointer is invalid, the behavior is undefined.
- **Output**: The function returns the square that is the en passant target, which is relevant for determining en passant captures.
- **See also**: [`chessGetEpTarget`](../../src/chesslib/chess.c.driver.md#chessGetEpTarget)  (Implementation)


---
### chessGetHalfMoveClock<!-- {{#callable_declaration:chessGetHalfMoveClock}} -->
Retrieve the half-move clock from the chess game state.
- **Description**: Use this function to obtain the current half-move clock value from a chess game, which is a count of the number of half-moves (or ply) since the last capture or pawn advance. This value is used in determining draw conditions such as the fifty-move rule. The function should be called on a valid chess game object, and it assumes that the game has been properly initialized. The function does not modify the game state.
- **Inputs**:
    - `c`: A pointer to a chess game object. Must not be null and should point to a valid, initialized chess game structure. If the pointer is invalid, the behavior is undefined.
- **Output**: Returns the current half-move clock as an unsigned integer, representing the number of half-moves since the last capture or pawn move.
- **See also**: [`chessGetHalfMoveClock`](../../src/chesslib/chess.c.driver.md#chessGetHalfMoveClock)  (Implementation)


---
### chessGetMoveNumber<!-- {{#callable_declaration:chessGetMoveNumber}} -->
Retrieve the current move number in the chess game.
- **Description**: Use this function to obtain the current move number of an ongoing chess game. It is useful for tracking the progress of the game and is typically called after the game has been initialized. The function requires a valid pointer to a chess game structure, which must have been previously initialized using one of the provided initialization functions. The move number is incremented as moves are played in the game.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current state of the game. This pointer must not be null and should point to a properly initialized chess game. If the pointer is invalid, the behavior is undefined.
- **Output**: Returns the current move number as an unsigned integer, indicating how many moves have been played in the game so far.
- **See also**: [`chessGetMoveNumber`](../../src/chesslib/chess.c.driver.md#chessGetMoveNumber)  (Implementation)


---
### chessGetMoveHistoryUci<!-- {{#callable_declaration:chessGetMoveHistoryUci}} -->
Returns a string of all moves in the game's history in UCI format.
- **Description**: Use this function to obtain a string representation of all moves made in a chess game, formatted according to the Universal Chess Interface (UCI) standard. This function is useful for logging, analysis, or exporting the move history of a game. The returned string must be freed by the caller to avoid memory leaks. Ensure that the chess game object is properly initialized and contains a valid move history before calling this function.
- **Inputs**:
    - `c`: A pointer to a chess game object. Must not be null and should be a valid, initialized chess game instance. The function assumes that the move history within the chess object is correctly maintained.
- **Output**: A dynamically allocated string containing the UCI representation of the move history. The caller is responsible for freeing this string.
- **See also**: [`chessGetMoveHistoryUci`](../../src/chesslib/chess.c.driver.md#chessGetMoveHistoryUci)  (Implementation)


---
### chessIsInCheck<!-- {{#callable_declaration:chessIsInCheck}} -->
Checks if the current player's king is in check.
- **Description**: Use this function to determine if the current player's king is in check in a given chess game state. This function is useful for validating game states and ensuring that moves do not leave the king in check. It should be called when you need to verify the safety of the king after a move or during game analysis. The function requires a valid chess game object and assumes that the game has been properly initialized. It does not modify the game state.
- **Inputs**:
    - `c`: A pointer to a chess game object. Must not be null and should point to a valid, initialized chess game structure. The function does not modify the object.
- **Output**: Returns 1 if the current player's king is in check, otherwise returns 0.
- **See also**: [`chessIsInCheck`](../../src/chesslib/chess.c.driver.md#chessIsInCheck)  (Implementation)


---
### chessIsSquareAttacked<!-- {{#callable_declaration:chessIsSquareAttacked}} -->
Determines if a specific square is attacked by the opponent.
- **Description**: This function checks whether a given square on the chessboard is under attack by the opponent's pieces. It is useful for determining threats to specific squares, such as when evaluating the safety of a king or planning defensive strategies. The function should be called with a valid chess game state and a valid square identifier. It assumes that the chess game has been properly initialized and is in a valid state. The function does not modify the game state or any of its components.
- **Inputs**:
    - `c`: A pointer to a chess game structure. It must not be null and should represent a valid, initialized chess game state.
    - `s`: An identifier for the square to be checked. It should be a valid square within the bounds of the chessboard.
- **Output**: Returns 1 if the square is attacked by the opponent, otherwise returns 0.
- **See also**: [`chessIsSquareAttacked`](../../src/chesslib/chess.c.driver.md#chessIsSquareAttacked)  (Implementation)


---
### chessGetFen<!-- {{#callable_declaration:chessGetFen}} -->
Returns a string containing the current board position in FEN format.
- **Description**: This function provides the current state of the chess board in the Forsyth-Edwards Notation (FEN), which is a standard notation for describing a particular board position of a chess game. It is useful for saving the game state, analyzing positions, or sharing the current game setup. The returned string must be freed by the caller to avoid memory leaks. This function should be called when a snapshot of the current game state is needed in FEN format.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null, as passing a null pointer will result in undefined behavior.
- **Output**: A dynamically allocated string containing the FEN representation of the current board position. The caller is responsible for freeing this string.
- **See also**: [`chessGetFen`](../../src/chesslib/chess.c.driver.md#chessGetFen)  (Implementation)


---
### chessCanClaimDraw50<!-- {{#callable_declaration:chessCanClaimDraw50}} -->
Determines if a draw can be claimed under the 50-move rule.
- **Description**: Use this function to check if a draw can be claimed in a chess game due to the 50-move rule, which applies when no pawn has been moved and no capture has been made in the last 50 moves by each player. This function should be called when you need to verify if the conditions for claiming a draw under this rule are met. It is important to ensure that the game is ongoing before calling this function, as it only returns a valid result in that state.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current state of the game. Must not be null. The game must be in an ongoing state for the function to return a meaningful result.
- **Output**: Returns a non-zero value if a draw can be claimed under the 50-move rule, and zero otherwise.
- **See also**: [`chessCanClaimDraw50`](../../src/chesslib/chess.c.driver.md#chessCanClaimDraw50)  (Implementation)


---
### chessCanClaimDrawThreefold<!-- {{#callable_declaration:chessCanClaimDrawThreefold}} -->
Determines if a draw can be claimed due to threefold repetition.
- **Description**: This function checks whether the current state of a chess game allows a player to claim a draw based on the threefold repetition rule. It should be called when a player wants to verify if they can claim a draw due to the same board position occurring three times. The function requires that the game is ongoing and that the current position has been repeated at least three times. It does not modify the game state or any input parameters.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null, and the game must be initialized and ongoing for the function to return a valid result.
- **Output**: Returns a non-zero value if a draw can be claimed due to threefold repetition, otherwise returns zero.
- **See also**: [`chessCanClaimDrawThreefold`](../../src/chesslib/chess.c.driver.md#chessCanClaimDrawThreefold)  (Implementation)


---
### chessClaimDraw50<!-- {{#callable_declaration:chessClaimDraw50}} -->
Claims a draw under the 50-move rule if applicable.
- **Description**: This function is used to claim a draw in a chess game when the 50-move rule condition is met. The 50-move rule states that a player can claim a draw if no pawn has been moved and no capture has been made in the last 50 moves by each player. This function should be called when a player wishes to claim such a draw. It checks if the draw can be claimed using the `chessCanClaimDraw50` function and, if so, updates the game's terminal state to indicate that a draw has been claimed under the 50-move rule. This function must be called with a valid `chess` object that has been properly initialized.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current state of the chess game. Must not be null and must point to a valid, initialized chess game object. If the pointer is invalid, the behavior is undefined.
- **Output**: None
- **See also**: [`chessClaimDraw50`](../../src/chesslib/chess.c.driver.md#chessClaimDraw50)  (Implementation)


---
### chessClaimDrawThreefold<!-- {{#callable_declaration:chessClaimDrawThreefold}} -->
Claims a draw by threefold repetition if possible.
- **Description**: This function is used to claim a draw in a chess game when the same position has occurred three times, which is a condition for a draw by threefold repetition. It should be called when a player believes the current board position has been repeated three times during the game. The function checks if the draw can be claimed using the current game state and updates the game's terminal state to indicate a draw if the condition is met. It is important to ensure that the game state is correctly maintained and updated before calling this function to avoid incorrect claims.
- **Inputs**:
    - `c`: A pointer to a chess game structure. Must not be null. The game state should be valid and up-to-date, as the function relies on the current board history and repetition count to determine if a draw can be claimed.
- **Output**: None
- **See also**: [`chessClaimDrawThreefold`](../../src/chesslib/chess.c.driver.md#chessClaimDrawThreefold)  (Implementation)


---
### chessCalculateFields<!-- {{#callable_declaration:chessCalculateFields}} -->
Updates the chess game's legal moves, repetition count, and terminal state.
- **Description**: This function updates the state of a chess game by recalculating the list of legal moves, counting the number of times the current board position has been repeated, and determining the game's terminal state. It should be called internally after each move to ensure the game state is accurate. The function handles various terminal conditions such as checkmate, stalemate, and draw scenarios based on repetition, move count, or insufficient material. It assumes that the chess game structure is properly initialized and that the current board state is valid.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null and should be properly initialized before calling this function. The function will update the fields within this structure.
- **Output**: None
- **See also**: [`chessCalculateFields`](../../src/chesslib/chess.c.driver.md#chessCalculateFields)  (Implementation)


