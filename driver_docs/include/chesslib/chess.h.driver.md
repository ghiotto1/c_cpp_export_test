# Purpose
This C source code file defines a set of functions and data structures for managing and interacting with a chess game. It provides a comprehensive interface for creating, initializing, and manipulating a chess game, including tracking the game's state, history, and legal moves. The code is structured around a `chess` struct, which encapsulates the current legal moves, terminal state, board history, move history, and repetition count. The file includes functions for creating a new chess game, either from scratch or from a specific FEN (Forsyth-Edwards Notation) string, and for freeing the resources associated with a game.

The file also defines a variety of utility functions for interacting with the chess game, such as retrieving the current board, legal moves, and terminal state, as well as playing and undoing moves. Additionally, it provides functions to check for specific game conditions, such as whether a draw can be claimed under certain rules. The code is designed to be used as part of a larger chess library, as indicated by the inclusion of headers like "chesslib/boardlist.h" and "chesslib/movelist.h". It does not define a main function, suggesting that it is intended to be used as a library rather than an executable. The file provides a public API for managing chess games, with functions that mirror those in the `board` struct for convenience, allowing for easy integration into other software components that require chess game functionality.
# Imports and Dependencies

---
- `chesslib/boardlist.h`
- `chesslib/movelist.h`
- `chesslib/squareset.h`


# Global Variables

---
### chessCreate
- **Type**: `function pointer`
- **Description**: The `chessCreate` function is a global function that returns a pointer to a `chess` structure, which represents a chess game. This function is responsible for creating and initializing a new chess game instance, which must be freed after use to prevent memory leaks.
- **Use**: The `chessCreate` function is used to instantiate a new chess game, setting up the initial state and allocating necessary resources.


---
### chessCreateFen
- **Type**: `function pointer`
- **Description**: The `chessCreateFen` is a function that creates and initializes a chess game from a given FEN (Forsyth-Edwards Notation) string. It returns a pointer to a `chess` structure, which represents the state of the chess game. If the provided FEN string is invalid, the function returns `NULL`. This function is part of a chess library that manages the state and rules of a chess game.
- **Use**: This function is used to initialize a chess game state from a FEN string, allowing users to start a game from a specific position.


---
### chessGetBoard
- **Type**: `function pointer`
- **Description**: `chessGetBoard` is a function that returns a pointer to a `board` structure, which represents the current state of the chess board in a given chess game. It takes a pointer to a `chess` structure as an argument, which contains the game's state and history.
- **Use**: This function is used to retrieve the current board state from a `chess` game instance.


---
### chessGetLegalMoves
- **Type**: `function`
- **Description**: The `chessGetLegalMoves` function is a global function that returns a pointer to a `moveList` structure, which contains all the legal moves available for the current state of a chess game. It takes a pointer to a `chess` structure as its parameter, which represents the current game state.
- **Use**: This function is used to retrieve the list of legal moves for the current position in a chess game, allowing the game logic to determine possible actions.


---
### chessGetBoardHistory
- **Type**: `function pointer`
- **Description**: `chessGetBoardHistory` is a function that returns a pointer to a `boardList`, which represents the history of board states in a chess game. It takes a pointer to a `chess` structure as an argument, allowing it to access the board history associated with that particular game instance.
- **Use**: This function is used to retrieve the sequence of board states that have occurred throughout the game, enabling analysis or review of the game's progression.


---
### chessGetMoveHistory
- **Type**: `function`
- **Description**: The `chessGetMoveHistory` function is a global function that returns a pointer to a `moveList` structure, which represents the history of moves made in a chess game. It takes a pointer to a `chess` structure as its parameter, allowing it to access the move history of the specific game instance.
- **Use**: This function is used to retrieve the list of moves that have been played in a given chess game.


---
### chessGetMoveHistoryUci
- **Type**: `function`
- **Description**: The `chessGetMoveHistoryUci` function returns a string that represents the history of all moves made in a chess game in the Universal Chess Interface (UCI) format. This function is part of a chess game management system and is used to retrieve the move history for analysis or display purposes.
- **Use**: This function is used to obtain a UCI-formatted string of the move history from a chess game instance.


---
### chessGetFen
- **Type**: `function`
- **Description**: The `chessGetFen` function is a global function that returns a string representing the current state of a chess game in Forsyth-Edwards Notation (FEN). This string must be freed by the caller to avoid memory leaks.
- **Use**: This function is used to obtain a FEN string that describes the current position of the chess game, which can be useful for saving the game state or for analysis purposes.


# Data Structures

---
### terminalState
- **Type**: `enum`
- **Members**:
    - `tsOngoing`: Represents a game state where the game is still in progress.
    - `tsCheckmate`: Indicates that the game has ended in checkmate.
    - `tsDrawStalemate`: Represents a draw due to stalemate.
    - `tsDrawClaimed50MoveRule`: Indicates a draw claimed by the 50-move rule.
    - `tsDraw75MoveRule`: Represents a draw automatically enforced by the 75-move rule.
    - `tsDrawClaimedThreefold`: Indicates a draw claimed by threefold repetition.
    - `tsDrawFivefold`: Represents a draw automatically enforced by fivefold repetition.
    - `tsDrawInsufficient`: Indicates a draw due to insufficient material to checkmate.
- **Description**: The `terminalState` enum defines the possible end states of a chess game, including ongoing play, checkmate, and various types of draws such as stalemate, 50-move rule, threefold repetition, and insufficient material. Each enumerator represents a specific condition under which a chess game can be concluded, providing a comprehensive set of outcomes for game termination.


---
### chess
- **Type**: `struct`
- **Members**:
    - `currentLegalMoves`: A pointer to a moveList structure containing the current legal moves available in the game.
    - `terminal`: An enum value representing the terminal state of the game, such as ongoing, checkmate, or various draw conditions.
    - `boardHistory`: A pointer to a boardList structure that keeps track of the history of board states throughout the game.
    - `moveHistory`: A pointer to a moveList structure that records the history of moves made during the game.
    - `repetitions`: A uint8_t value indicating how many times the current board position has been repeated.
- **Description**: The 'chess' structure is a comprehensive representation of a chess game state, encapsulating the current legal moves, the terminal state of the game, the history of board states and moves, and the number of repetitions of the current position. It is designed to manage and track the progression of a chess game, providing functionality to initialize, update, and query the game state, as well as to handle special conditions like draw claims and move legality.


# Function Declarations (Public API)

---
### chessCreate<!-- {{#callable_declaration:chessCreate}} -->
Creates and initializes a new chess game instance.
- **Description**: This function is used to create and initialize a new chess game instance with the standard initial position. It is suitable for starting a new game of chess from the default setup. The function allocates memory for the chess game structure, and the caller is responsible for freeing this memory using `chessFree` when the game is no longer needed. This function does not require any parameters and will return a pointer to the initialized chess game structure. If the initialization fails, it will return NULL.
- **Inputs**:
    - None
- **Output**: Returns a pointer to a newly created chess game instance, or NULL if initialization fails.
- **See also**: [`chessCreate`](../../src/chesslib/chess.c.driver.md#chessCreate)  (Implementation)


---
### chessCreateFen<!-- {{#callable_declaration:chessCreateFen}} -->
Creates and initializes a chess game from a FEN string.
- **Description**: This function allocates and initializes a new chess game structure based on the provided FEN (Forsyth-Edwards Notation) string, which describes a specific board position. It is useful for setting up a game from a known position. The function returns a pointer to the initialized chess game structure if the FEN string is valid. If the FEN string is invalid, the function returns NULL, and no memory is allocated for the chess game. The caller is responsible for freeing the returned chess game structure using `chessFree` when it is no longer needed.
- **Inputs**:
    - `fen`: A null-terminated string representing the board position in Forsyth-Edwards Notation. The string must be valid FEN; otherwise, the function will return NULL. The caller retains ownership of this string, and it must not be null.
- **Output**: A pointer to a newly allocated and initialized chess game structure if the FEN is valid, or NULL if the FEN is invalid.
- **See also**: [`chessCreateFen`](../../src/chesslib/chess.c.driver.md#chessCreateFen)  (Implementation)


---
### chessInitInPlace<!-- {{#callable_declaration:chessInitInPlace}} -->
Initializes a chess game to the standard starting position.
- **Description**: This function sets up a chess game represented by the `chess` structure to the standard initial position, ready for play. It should be used when you want to start a new game from the traditional starting setup. The function must be called with a valid `chess` structure that has been properly allocated. It does not return any value and assumes that the input structure is not null. This function is typically used when resetting a game or starting a new one without needing to specify a custom position using FEN notation.
- **Inputs**:
    - `c`: A pointer to a `chess` structure that will be initialized to the standard starting position. The structure must be allocated before calling this function and must not be null. The caller retains ownership of the structure.
- **Output**: None
- **See also**: [`chessInitInPlace`](../../src/chesslib/chess.c.driver.md#chessInitInPlace)  (Implementation)


---
### chessInitFenInPlace<!-- {{#callable_declaration:chessInitFenInPlace}} -->
Initializes a chess game state from a FEN string in place.
- **Description**: This function initializes an existing chess game structure using a given FEN (Forsyth-Edwards Notation) string, which describes a specific board position. It should be used when you want to set up a chess game to a specific state as described by the FEN string. The function must be called with a valid chess structure that has been properly allocated. If the FEN string is invalid, the function will not modify the chess structure and will return an error code. This function is useful for setting up specific board positions for analysis or testing.
- **Inputs**:
    - `c`: A pointer to a chess structure that must be pre-allocated and will be initialized to the state described by the FEN string. The caller retains ownership and must ensure it is not null.
    - `fen`: A pointer to a null-terminated string containing the FEN representation of the desired board state. The string must be valid and correctly formatted; otherwise, the function will return an error code.
- **Output**: Returns 0 if the initialization is successful, or 1 if the FEN string is invalid, in which case the chess structure remains unmodified.
- **See also**: [`chessInitFenInPlace`](../../src/chesslib/chess.c.driver.md#chessInitFenInPlace)  (Implementation)


---
### chessFree<!-- {{#callable_declaration:chessFree}} -->
Frees a chess game and all its components.
- **Description**: Use this function to release all memory associated with a chess game when it is no longer needed. It should be called to prevent memory leaks after a chess game has been created using `chessCreate` or `chessCreateFen`. Ensure that the pointer `c` is valid and was previously allocated by one of the creation functions. After calling this function, the pointer `c` should not be used again unless it is reinitialized.
- **Inputs**:
    - `c`: A pointer to a `chess` structure that must have been previously allocated by `chessCreate` or `chessCreateFen`. The pointer must not be null, and the function will free all associated resources. Passing an invalid or null pointer results in undefined behavior.
- **Output**: None
- **See also**: [`chessFree`](../../src/chesslib/chess.c.driver.md#chessFree)  (Implementation)


---
### chessGetBoard<!-- {{#callable_declaration:chessGetBoard}} -->
Retrieves the current board state from a chess game.
- **Description**: Use this function to obtain the current board state of a chess game represented by the `chess` structure. This function is useful when you need to analyze or display the current position of pieces on the board. It is expected that the `chess` structure has been properly initialized and is in a valid state before calling this function. The function does not modify the state of the game or the board.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current game. Must not be null and should point to a valid, initialized chess game. If the pointer is invalid, the behavior is undefined.
- **Output**: A pointer to a `board` structure representing the current board state. The caller should not modify the returned board directly.
- **See also**: [`chessGetBoard`](../../src/chesslib/chess.c.driver.md#chessGetBoard)  (Implementation)


---
### chessGetLegalMoves<!-- {{#callable_declaration:chessGetLegalMoves}} -->
Retrieves the list of legal moves for the current game state.
- **Description**: Use this function to obtain the current list of legal moves available in the ongoing chess game. This function is useful for determining the possible actions a player can take at any given point in the game. It is important to ensure that the chess game has been properly initialized and is in a valid state before calling this function. The returned list reflects the legal moves based on the current board configuration and game rules.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null. The chess game should be initialized and in a valid state before calling this function.
- **Output**: A pointer to a moveList structure containing the legal moves for the current game state. The caller should not modify or free this list directly.
- **See also**: [`chessGetLegalMoves`](../../src/chesslib/chess.c.driver.md#chessGetLegalMoves)  (Implementation)


---
### chessGetTerminalState<!-- {{#callable_declaration:chessGetTerminalState}} -->
Retrieves the current terminal state of a chess game.
- **Description**: Use this function to determine the current terminal state of a chess game, which indicates whether the game is ongoing, in checkmate, or drawn under various conditions. This function is useful for checking the game's status after moves have been played. It should be called on a valid chess game object that has been properly initialized. The function does not modify the game state and is safe to call at any time after initialization.
- **Inputs**:
    - `c`: A pointer to a chess game object. Must not be null and should point to a valid, initialized chess game structure. The function does not modify the object.
- **Output**: The function returns the current terminal state of the chess game, which is an enumeration value of type `terminalState`.
- **See also**: [`chessGetTerminalState`](../../src/chesslib/chess.c.driver.md#chessGetTerminalState)  (Implementation)


---
### chessGetBoardHistory<!-- {{#callable_declaration:chessGetBoardHistory}} -->
Retrieve the history of board states in a chess game.
- **Description**: Use this function to access the sequence of board states that have occurred throughout the course of a chess game. This can be useful for analyzing the progression of the game or for implementing features that require knowledge of past board configurations. The function should be called on a valid `chess` object that has been properly initialized. It does not modify the state of the game or the `chess` object.
- **Inputs**:
    - `c`: A pointer to a `chess` object representing the current game state. Must not be null and should point to a valid, initialized `chess` structure. If the pointer is invalid, behavior is undefined.
- **Output**: Returns a pointer to a `boardList` object representing the history of board states. The caller should not modify or free this list directly.
- **See also**: [`chessGetBoardHistory`](../../src/chesslib/chess.c.driver.md#chessGetBoardHistory)  (Implementation)


---
### chessGetMoveHistory<!-- {{#callable_declaration:chessGetMoveHistory}} -->
Retrieves the history of moves made in a chess game.
- **Description**: This function is used to obtain the list of all moves that have been played in a given chess game. It is useful for analyzing the progression of the game or for displaying the move history to users. The function should be called on a valid chess game object, and it assumes that the game has been properly initialized. The returned move list reflects the current state of the game's move history and should not be modified by the caller.
- **Inputs**:
    - `c`: A pointer to a chess game object. It must not be null and should point to a valid, initialized chess game structure. If the pointer is invalid, the behavior is undefined.
- **Output**: A pointer to a moveList structure representing the history of moves made in the game. The caller should not modify this list.
- **See also**: [`chessGetMoveHistory`](../../src/chesslib/chess.c.driver.md#chessGetMoveHistory)  (Implementation)


---
### chessGetRepetitions<!-- {{#callable_declaration:chessGetRepetitions}} -->
Retrieve the number of times the current board position has been repeated.
- **Description**: Use this function to determine how many times the current board position has been encountered during the game. This information is useful for detecting draw conditions such as the threefold repetition rule. The function should be called on a valid `chess` object that has been properly initialized. It does not modify the state of the game or the `chess` object.
- **Inputs**:
    - `c`: A pointer to a `chess` object representing the current game state. Must not be null and should be a valid, initialized `chess` object.
- **Output**: Returns the number of times the current board position has been repeated as a `uint8_t` value.
- **See also**: [`chessGetRepetitions`](../../src/chesslib/chess.c.driver.md#chessGetRepetitions)  (Implementation)


---
### chessPlayMove<!-- {{#callable_declaration:chessPlayMove}} -->
Attempts to play a specified move in a chess game.
- **Description**: This function attempts to play a given move in the context of an ongoing chess game. It should be called when you want to execute a move that has been determined to be legal. The function checks if the game is still ongoing and if the move is among the current legal moves. If the move is valid and the game is ongoing, it updates the game state by applying the move, adding it to the move history, and recalculating the game's fields. If the move is illegal or the game is not ongoing, the function returns an error code. This function should be used only when the game is in progress and the move is expected to be legal.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null and the game must be ongoing (i.e., terminal state is tsOngoing).
    - `m`: A move structure representing the move to be played. It should be a legal move within the current game state.
- **Output**: Returns 0 if the move was successfully played, or 1 if the move was illegal or the game is not ongoing.
- **See also**: [`chessPlayMove`](../../src/chesslib/chess.c.driver.md#chessPlayMove)  (Implementation)


---
### chessUndo<!-- {{#callable_declaration:chessUndo}} -->
Undoes the last move or draw claim in a chess game.
- **Description**: Use this function to revert the most recent move or draw claim in a chess game, effectively stepping back one turn. It is useful for implementing undo functionality in a chess application. The function must be called on a valid chess game object that has been initialized and has at least one move in its history. If there are no moves to undo, the function will return an error code. Additionally, if the game is in a draw state due to a claimed draw, the draw state will be reset to ongoing.
- **Inputs**:
    - `c`: A pointer to a chess game object. This object must be initialized and must not be null. The function will fail if there are no moves in the game's history to undo.
- **Output**: Returns 0 if the undo operation is successful, or 1 if unsuccessful (e.g., no moves left to undo).
- **See also**: [`chessUndo`](../../src/chesslib/chess.c.driver.md#chessUndo)  (Implementation)


---
### chessGetPiece<!-- {{#callable_declaration:chessGetPiece}} -->
Retrieves the piece located at a specific square on the chessboard.
- **Description**: This function is used to obtain the piece present at a given square on the chessboard within a chess game. It is useful for checking the current state of the board, such as determining which piece occupies a particular position. The function should be called with a valid chess game instance and a valid square identifier. It is important to ensure that the chess game has been properly initialized before calling this function to avoid undefined behavior.
- **Inputs**:
    - `c`: A pointer to a chess game instance. Must not be null and should point to a valid, initialized chess game structure.
    - `s`: An identifier for a square on the chessboard. Must be a valid square within the board's range.
- **Output**: The function returns the piece located at the specified square. If the square is empty, it returns a value indicating no piece is present.
- **See also**: [`chessGetPiece`](../../src/chesslib/chess.c.driver.md#chessGetPiece)  (Implementation)


---
### chessGetPlayer<!-- {{#callable_declaration:chessGetPlayer}} -->
Returns the current player's color in the chess game.
- **Description**: Use this function to determine which player's turn it is in the current state of the chess game. This function is useful for game logic that depends on knowing the active player, such as determining legal moves or enforcing turn-based rules. It must be called with a valid pointer to a chess game structure that has been properly initialized. The function does not modify the game state or any input parameters.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null and should point to a valid, initialized chess game.
- **Output**: The function returns a value of type pieceColor, indicating the color of the player whose turn it is.
- **See also**: [`chessGetPlayer`](../../src/chesslib/chess.c.driver.md#chessGetPlayer)  (Implementation)


---
### chessGetCastleState<!-- {{#callable_declaration:chessGetCastleState}} -->
Retrieve the current castling rights state of the chess game.
- **Description**: This function is used to obtain the current castling rights state from a chess game instance. It is useful for determining which castling moves are still available in the ongoing game. The function should be called with a valid pointer to a chess game structure that has been properly initialized. The castling state is represented as an 8-bit unsigned integer, where each bit may represent a specific castling right. Ensure that the chess game instance is not null before calling this function to avoid undefined behavior.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current state of the game. Must not be null and should be properly initialized before calling this function.
- **Output**: An 8-bit unsigned integer representing the current castling rights state of the game.
- **See also**: [`chessGetCastleState`](../../src/chesslib/chess.c.driver.md#chessGetCastleState)  (Implementation)


---
### chessGetEpTarget<!-- {{#callable_declaration:chessGetEpTarget}} -->
Retrieves the en passant target square from the chess game state.
- **Description**: This function is used to obtain the en passant target square from the current state of a chess game. It is useful when you need to determine if an en passant capture is possible in the current position. The function should be called on a valid chess game object that has been properly initialized. It does not modify the state of the game or any of its components.
- **Inputs**:
    - `c`: A pointer to a chess game object. It must not be null and should point to a valid, initialized chess game structure. If the pointer is invalid, the behavior is undefined.
- **Output**: The function returns the en passant target square as a value of type 'sq'. If there is no en passant target, the return value will indicate this (typically as a special value or null square, depending on the 'sq' type definition).
- **See also**: [`chessGetEpTarget`](../../src/chesslib/chess.c.driver.md#chessGetEpTarget)  (Implementation)


---
### chessGetHalfMoveClock<!-- {{#callable_declaration:chessGetHalfMoveClock}} -->
Retrieve the half-move clock from the chess game state.
- **Description**: This function is used to obtain the current half-move clock value from a chess game, which is part of the game's state. The half-move clock counts the number of half-moves (or ply) since the last capture or pawn advance, and is used in determining draw conditions such as the fifty-move rule. This function should be called when you need to check the progress towards a draw by the fifty-move rule. It is expected that the chess game has been properly initialized before calling this function.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current state of the chess game. Must not be null, and the chess game should be properly initialized before calling this function.
- **Output**: Returns the current half-move clock as an unsigned integer, indicating the number of half-moves since the last capture or pawn move.
- **See also**: [`chessGetHalfMoveClock`](../../src/chesslib/chess.c.driver.md#chessGetHalfMoveClock)  (Implementation)


---
### chessGetMoveNumber<!-- {{#callable_declaration:chessGetMoveNumber}} -->
Retrieve the current move number of the chess game.
- **Description**: Use this function to obtain the current move number in a chess game, which is useful for tracking the progress of the game or for display purposes. This function should be called on a valid chess game object that has been properly initialized. It is important to ensure that the chess game object is not null before calling this function to avoid undefined behavior.
- **Inputs**:
    - `c`: A pointer to a chess game object. This must be a valid, non-null pointer to a chess structure that has been initialized using one of the provided initialization functions. If the pointer is null, the behavior is undefined.
- **Output**: Returns the current move number as an unsigned integer, representing the number of moves made in the game so far.
- **See also**: [`chessGetMoveNumber`](../../src/chesslib/chess.c.driver.md#chessGetMoveNumber)  (Implementation)


---
### chessGetMoveHistoryUci<!-- {{#callable_declaration:chessGetMoveHistoryUci}} -->
Returns a string of all moves in the game's history in UCI format.
- **Description**: Use this function to obtain a string representation of all moves made in a chess game, formatted according to the Universal Chess Interface (UCI) standard. This is useful for logging, analysis, or exporting the game's move history. The returned string must be freed by the caller to avoid memory leaks. Ensure that the chess game object is properly initialized and contains a valid move history before calling this function.
- **Inputs**:
    - `c`: A pointer to a chess game object. Must not be null and should be a valid, initialized chess game instance. The function assumes that the game has a move history to convert to UCI format.
- **Output**: A dynamically allocated string containing the UCI representation of the game's move history. The caller is responsible for freeing this string.
- **See also**: [`chessGetMoveHistoryUci`](../../src/chesslib/chess.c.driver.md#chessGetMoveHistoryUci)  (Implementation)


---
### chessIsInCheck<!-- {{#callable_declaration:chessIsInCheck}} -->
Checks if the current player is in check.
- **Description**: This function determines whether the current player in a chess game is in a state of check, meaning their king is under threat of capture on the next move. It should be called when you need to verify the check status of the game, typically after a move has been made. The function requires a valid chess game object that has been properly initialized. It does not modify the game state or any of its components.
- **Inputs**:
    - `c`: A pointer to a chess game object. This must be a valid, initialized chess object and must not be null. If the pointer is invalid or null, the behavior is undefined.
- **Output**: Returns 1 if the current player is in check, and 0 otherwise.
- **See also**: [`chessIsInCheck`](../../src/chesslib/chess.c.driver.md#chessIsInCheck)  (Implementation)


---
### chessIsSquareAttacked<!-- {{#callable_declaration:chessIsSquareAttacked}} -->
Determines if a specific square is attacked by the opponent.
- **Description**: This function checks whether a given square on the chessboard is under attack by the opponent's pieces. It is useful for determining threats to specific squares, which can be critical for making strategic decisions in a chess game. The function should be called with a valid chess game state and a valid square identifier. It assumes that the chess game has been properly initialized and is in a valid state. The function does not modify the game state or any of its components.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current state of the chess game. Must not be null and should point to a valid, initialized chess game.
    - `s`: An identifier for the square to be checked. It should be a valid square within the bounds of the chessboard.
- **Output**: Returns 1 if the square is attacked by the opponent, otherwise returns 0.
- **See also**: [`chessIsSquareAttacked`](../../src/chesslib/chess.c.driver.md#chessIsSquareAttacked)  (Implementation)


---
### chessGetFen<!-- {{#callable_declaration:chessGetFen}} -->
Returns a string containing the current board position in FEN format.
- **Description**: This function provides the current state of the chess board in the Forsyth-Edwards Notation (FEN) format, which is useful for saving the game state or for interoperability with other chess software. It must be called with a valid `chess` object that has been properly initialized. The returned string must be freed by the caller to avoid memory leaks. This function is typically used when you need to export the current game state or analyze it using external tools that accept FEN strings.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current game state. It must not be null and should be properly initialized before calling this function. If the pointer is invalid, the behavior is undefined.
- **Output**: A dynamically allocated string containing the FEN representation of the current board state. The caller is responsible for freeing this string.
- **See also**: [`chessGetFen`](../../src/chesslib/chess.c.driver.md#chessGetFen)  (Implementation)


---
### chessCanClaimDraw50<!-- {{#callable_declaration:chessCanClaimDraw50}} -->
Determines if a draw can be claimed under the 50-move rule.
- **Description**: This function checks whether a draw can be claimed in a chess game based on the 50-move rule, which allows a player to claim a draw if no pawn has been moved and no capture has been made in the last 50 moves by each player. It should be called when a player wants to verify if they can claim a draw under this rule. The function requires that the game is ongoing and will return a positive result if the conditions for the 50-move rule are met.
- **Inputs**:
    - `c`: A pointer to a chess game structure. Must not be null. The game must be in an ongoing state for the function to return a meaningful result.
- **Output**: Returns 1 if a draw can be claimed under the 50-move rule, otherwise returns 0.
- **See also**: [`chessCanClaimDraw50`](../../src/chesslib/chess.c.driver.md#chessCanClaimDraw50)  (Implementation)


---
### chessCanClaimDrawThreefold<!-- {{#callable_declaration:chessCanClaimDrawThreefold}} -->
Determines if a draw can be claimed due to threefold repetition.
- **Description**: Use this function to check if the current game state allows a player to claim a draw based on the threefold repetition rule. This function should be called when you want to verify if the same board position has occurred at least three times during the game, which is a condition for claiming a draw in chess. The function requires that the game is still ongoing and will return a non-zero value if the draw can be claimed. Ensure that the chess game structure is properly initialized and represents an ongoing game before calling this function.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null and should be properly initialized. The game must be ongoing for the function to return a meaningful result.
- **Output**: Returns a non-zero value if a draw can be claimed due to threefold repetition, otherwise returns zero.
- **See also**: [`chessCanClaimDrawThreefold`](../../src/chesslib/chess.c.driver.md#chessCanClaimDrawThreefold)  (Implementation)


---
### chessClaimDraw50<!-- {{#callable_declaration:chessClaimDraw50}} -->
Claims a draw under the 50-move rule if applicable.
- **Description**: This function is used to claim a draw in a chess game when the 50-move rule condition is met. The 50-move rule states that a player can claim a draw if no pawn has been moved and no capture has been made in the last 50 moves by each player. This function should be called when a player wishes to claim such a draw. It checks if the draw can be claimed and, if so, updates the game's terminal state to reflect the draw claim. It is important to ensure that the game state is correctly initialized and that the function `chessCanClaimDraw50` returns true before calling this function.
- **Inputs**:
    - `c`: A pointer to a `chess` structure representing the current game state. Must not be null. The function assumes that the game state is valid and properly initialized. If the draw cannot be claimed, the game state remains unchanged.
- **Output**: None
- **See also**: [`chessClaimDraw50`](../../src/chesslib/chess.c.driver.md#chessClaimDraw50)  (Implementation)


---
### chessClaimDrawThreefold<!-- {{#callable_declaration:chessClaimDrawThreefold}} -->
Claims a draw by threefold repetition if possible.
- **Description**: This function is used to claim a draw in a chess game when the same board position has occurred three times, which is a condition for a draw by threefold repetition. It should be called when a player believes the current position has been repeated three times during the game. The function checks if the draw can be claimed using the current game state and updates the game's terminal state to indicate a draw if the condition is met. It is important to ensure that the game state is up-to-date before calling this function, as it relies on the current board history to determine eligibility for the draw claim.
- **Inputs**:
    - `c`: A pointer to a chess game structure. Must not be null. The function assumes that the game state is correctly maintained and up-to-date, as it uses the board history to determine if a draw can be claimed.
- **Output**: None
- **See also**: [`chessClaimDrawThreefold`](../../src/chesslib/chess.c.driver.md#chessClaimDrawThreefold)  (Implementation)


---
### chessCalculateFields<!-- {{#callable_declaration:chessCalculateFields}} -->
Updates the legal moves, repetition count, and terminal state of a chess game.
- **Description**: This function updates the state of a chess game by recalculating the list of legal moves, counting the number of times the current board position has been repeated, and determining the terminal state of the game. It should be called internally after each move to ensure the game state is accurate. The function handles various terminal conditions such as checkmate, stalemate, and draw scenarios based on repetition, move count, or insufficient material. It assumes that the chess game structure is properly initialized and that the current board state is valid.
- **Inputs**:
    - `c`: A pointer to a chess structure representing the current game state. Must not be null and should be properly initialized before calling this function. The function will update the fields within this structure.
- **Output**: None
- **See also**: [`chessCalculateFields`](../../src/chesslib/chess.c.driver.md#chessCalculateFields)  (Implementation)


