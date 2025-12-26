# Purpose
The `game.cpp` file is a core component of a chess application, responsible for managing the overall game state and the interactions between players and pieces. It defines the [`Game`](#GameGame) class, which encapsulates the initialization and management of chess pieces and players. The file includes headers for various chess piece classes such as `queen.h`, `bishop.h`, `knight.h`, `rook.h`, `pawn.h`, and `king.h`, indicating that it relies on these classes to represent the different types of chess pieces. The [`Game`](#GameGame) class contains methods for initializing the game board with pieces in their starting positions, managing the lifecycle of the pieces and players, and determining the next player to move.

The [`Game`](#GameGame) class provides a structured approach to setting up a chess game by creating and positioning pieces on the board, associating them with players, and managing the turn-based nature of the game. It uses sets to store the white and black pieces, ensuring efficient management and cleanup of resources. The class also includes methods like `getNextPlayer()` and `opponentOf()` to facilitate player interactions and determine the flow of the game. This file is not an executable on its own but is intended to be part of a larger chess application, serving as a central component that coordinates the game's logic and state.
# Imports and Dependencies

---
- `game.h`
- `queen.h`
- `bishop.h`
- `knight.h`
- `rook.h`
- `pawn.h`
- `king.h`
- `square.h`


# Global Variables

---
### player1
- **Type**: `Player*`
- **Description**: The `player1` variable is a global pointer to a `Player` object within the `Game` class. It is used to represent the first player in the chess game, typically the player controlling the white pieces.
- **Use**: This variable is used to store and manage the state and actions of the first player in the game, including their pieces and moves.


---
### player2
- **Type**: `Player*`
- **Description**: The `player2` variable is a global pointer to a `Player` object representing the second player in the game, typically the player controlling the black pieces in a chess game. It is initialized to `NULL` and later assigned a `Player` object in the `initialize` method of the `Game` class.
- **Use**: `player2` is used to store and manage the state and actions of the second player in the chess game.


---
### nextPlayer
- **Type**: `Player*`
- **Description**: `nextPlayer` is a global pointer variable of type `Player*` that is part of the `Game` class. It is initialized to `NULL` and is used to keep track of the player whose turn it is to play next in the game.
- **Use**: This variable is used to determine and update the current player in the game flow, switching between players after each turn.


# Data Structures

---
### Game<!-- {{#data_structure:Game}} -->
- **Description**: [See definition](game.h.driver.md#Game)
- **Member Functions**:
    - [`Game::Game`](#GameGame)
    - [`Game::~Game`](#GameGame)
    - [`Game::initialize`](#Gameinitialize)
    - [`Game::getNextPlayer`](#GamegetNextPlayer)
    - [`Game::opponentOf`](#GameopponentOf)

**Methods**

---
#### Game::Game<!-- {{#callable:Game::Game}} -->
The `Game` constructor initializes a new instance of the `Game` class without performing any specific actions.
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined but does not contain any code or logic, indicating it performs no operations when a `Game` object is instantiated.
- **Output**: There is no output from this constructor as it does not perform any operations.
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)


---
#### Game::\~Game<!-- {{#callable:Game::~Game}} -->
The `~Game` destructor deallocates memory for all chess pieces and players associated with a game instance.
- **Inputs**: None
- **Control Flow**:
    - Iterates over the `whitePieces` set, deleting each `Piece` pointer and then clears the set.
    - Iterates over the `blackPieces` set, deleting each `Piece` pointer and then clears the set.
    - Deletes the `player1` and `player2` objects.
- **Output**: This function does not return any value as it is a destructor.
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)


---
#### Game::initialize<!-- {{#callable:Game::initialize}} -->
The `initialize` function sets up a new chess game by creating and positioning all pieces on the board, assigning them to players, and determining the starting player.
- **Inputs**: None
- **Control Flow**:
    - Initialize local pointers for Piece, King, and Square objects.
    - Create sets for white and black pieces.
    - Instantiate and position a white Queen at (3, 0) and a black Queen at (3, 7), then add them to their respective sets.
    - Instantiate and position two white Bishops at (2, 0) and (5, 0) and two black Bishops at (2, 7) and (5, 7), then add them to their respective sets.
    - Instantiate and position two white Knights at (1, 0) and (6, 0) and two black Knights at (1, 7) and (6, 7), then add them to their respective sets.
    - Instantiate and position two white Rooks at (0, 0) and (7, 0) and two black Rooks at (0, 7) and (7, 7), then add them to their respective sets.
    - Use a loop to instantiate and position eight white Pawns at row 1 and eight black Pawns at row 6, then add them to their respective sets.
    - Instantiate and position a white King at (4, 0) and a black King at (4, 7), then add them to their respective sets.
    - Create a Player object for the white player with their pieces and King, and assign it to `player1`.
    - Create a Player object for the black player with their pieces and King, and assign it to `player2`.
    - Set `nextPlayer` to `player2`, indicating the black player starts.
- **Output**: The function does not return any value; it initializes the game state by setting up the board and players.
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)


---
#### Game::getNextPlayer<!-- {{#callable:Game::getNextPlayer}} -->
The `getNextPlayer` function updates and returns the player whose turn is next in the game.
- **Inputs**: None
- **Control Flow**:
    - The function calls [`opponentOf`](#GameopponentOf) with the current `nextPlayer` to determine the opponent player.
    - It updates `nextPlayer` to the opponent player returned by [`opponentOf`](#GameopponentOf).
    - The function returns the updated `nextPlayer`.
- **Output**: A pointer to the `Player` object representing the next player to take a turn.
- **Functions called**:
    - [`Game::opponentOf`](#GameopponentOf)
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)


---
#### Game::opponentOf<!-- {{#callable:Game::opponentOf}} -->
The `opponentOf` function returns the opponent player of the given player in a chess game.
- **Inputs**:
    - `player`: A reference to a `Player` object for whom the opponent is to be determined.
- **Control Flow**:
    - Declare a pointer `opponent` to hold the opponent player.
    - Check if the given player's name matches `player1`'s name.
    - If it matches, set `opponent` to `player2`.
    - If it does not match, set `opponent` to `player1`.
    - Return the `opponent` pointer.
- **Output**: A pointer to the `Player` object representing the opponent of the given player.
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)



