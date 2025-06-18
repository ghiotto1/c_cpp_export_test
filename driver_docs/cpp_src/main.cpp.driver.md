# Purpose
This C++ source code file serves as the main entry point for a chess game application. It is designed to initialize and manage the flow of a chess game by interacting with other components, specifically the `Game` and `Board` classes, which are likely defined in the included headers "game.h" and "board.h". The code initializes the game state and enters a loop where players alternate turns to make moves. The `Game::initialize()` function is called to set up the initial game state, and the `Board::getBoard()->display(cout)` function is used to display the current state of the chessboard to the standard output.

The main technical components of this file include the game loop, which continuously prompts players to make moves, and the error handling mechanism that ensures only valid moves are accepted. The `currentPlayer` pointer is used to track the player whose turn it is, and the `Game::getNextPlayer()` function is called to switch turns between players. The file does not define public APIs or external interfaces but rather orchestrates the interaction between the game logic and the user interface. This code is intended to be compiled into an executable that runs the chess game, leveraging the functionality provided by the `Game` and `Board` classes.
# Imports and Dependencies

---
- `iostream`
- `game.h`
- `board.h`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes and runs a continuous loop for a chess game where players alternate making moves until a valid move is made.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a pointer `currentPlayer` to `NULL`.
    - Call `Game::initialize()` to set up the chess game.
    - Display the initial state of the board using `Board::getBoard()->display(cout)`.
    - Enter an infinite loop to alternate player turns.
    - Within the loop, get the next player using `Game::getNextPlayer()`.
    - Attempt to make a move with `currentPlayer->makeMove()`, repeating until a valid move is made.
    - If a move is invalid, output an error message to `cerr`.
    - After a valid move, display the updated board state with `Board::getBoard()->display(cout)`.
- **Output**: The function returns an integer `0`, indicating successful execution.


