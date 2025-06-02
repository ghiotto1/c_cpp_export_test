# Purpose
This code is a C++ executable, specifically the main entry point for a chess game application. It provides narrow functionality focused on initializing and managing the flow of a chess game. The code includes headers for "game.h" and "board.h," suggesting that it relies on external classes or functions defined in these files to handle game logic and board representation. The main function initializes the game, displays the initial board state, and enters a loop where players alternate making moves. It ensures that only valid moves are accepted, prompting the player to try again if an invalid move is attempted, and updates the board display after each move. This code is designed to be run as a standalone application, facilitating a text-based chess game experience.
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
    - Initialize a pointer to `Player` as `currentPlayer` to keep track of the current player.
    - Call `Game::initialize()` to set up the initial state of the chess game.
    - Display the initial state of the board using `Board::getBoard()->display(cout)`.
    - Enter an infinite loop to alternate between players making moves.
    - Within the loop, get the next player using `Game::getNextPlayer()` and assign it to `currentPlayer`.
    - Attempt to make a move with `currentPlayer->makeMove()`, and if the move is invalid, output an error message and prompt the player to try again.
    - After a valid move, display the updated state of the board using `Board::getBoard()->display(cout)`.
- **Output**:
    - The function returns an integer value of 0, indicating successful execution of the program.


